This is a small script that enables you to transfer/claim various coins in Bitcoin forks
without downloading the full blockchains or messing with the official clients.

Requires Python 2.7

The following coins are recognized, although may not be fully tested:

*  B2X - [Segwit 2X](https://b2x-segwit.io/)
*  BCD - [Bitcoin Diamond](http://www.btcd.io/)
*  BCX - [Bitcoin X](https://bcx.org/)
*  BPA - [Bitcoin Pizza](http://p.top/en/index.html)
*  BTF - [Bitcoin Faith](http://bitcoinfaith.org/)
*  BTG - [Bitcoin Gold](https://bitcoingold.org/)
*  BTH - [Bitcoin Hot](https://www.bithot.org/)
*  BTN - [Bitcoin New](http://btn.kim/)
*  BTT - [Bitcoin Top](https://bitcointop.org/)
*  BTV - [Bitcoin Vote](https://bitvote.one/)
*  BTW - [Bitcoin World](http://www.btw.one/)
*  SBTC - [Super Bitcoin](http://superbtc.org/)
*  UBTC - [United Bitcoin](https://www.ub.com/)

At the moment it supports standard P2PKH and Segwit P2SH-P2WPKH addresses. Segwit mode has been verified to work with these coins: BTG, BCX, B2X, UBTC, BTF, BTW, SBTC, BCD, BPA, BTN, BTH, BTV, BTT

It also has experimental support for bech32 P2WPKH, but this has only been tested on the BTG, BTN, BCD, BTH, BTV, BTT networks so far.

It should support old-style Pay-2-Public-Key that were in use in 2009-2010 (use command line switch --p2pk) but this is UNTESTED at the moment.

USAGE OF THIS SCRIPT IS RISKY AND IF YOU MISTYPE ANYTHING YOU CAN LOSE ALL YOUR COINS

It has two modes of operation - blockchain.info assisted mode and standalone mode.
* In blockchain.info mode it uses the blockchain.info API to query and validate information about the transaction you're spending from.
This only works for transferring/claiming coins that existed on the BTC main chain pre-fork.
* In standalone mode the user provides all the information including transaction source output index and the number of satoshis in the source output - there is no verification done, but this mode allows you to transfer coins that are entirely on-fork.

blockchain.info mode:

    claimer.py <cointype> <source transaction ID> <source private key> <source address> <destination address>
    claimer.py BTG 4adc427d330497992710feaa32f85c389ef5106f74e7006878bd14b54500dfff 5K2YUVmWfxbmvsNxCsfvArXdGXm7d5DC9pn4yD75k2UaSYgkXTh 1HKqKTMpBTZZ8H5zcqYEWYBaaWELrDEXeE 1aa5cmqmvQq8YQTEqcTmW7dfBNuFwgdCD
    
Standalone mode:

    claimer.py <cointype> <source transaction ID> <source private key> <source address> <destination address> --txindex <output index in transaction> --satoshis <number of satoshis on the source transaction output>
    claimer.py BTG 4adc427d330497992710feaa32f85c389ef5106f74e7006878bd14b54500dfff 5K2YUVmWfxbmvsNxCsfvArXdGXm7d5DC9pn4yD75k2UaSYgkXTh 1HKqKTMpBTZZ8H5zcqYEWYBaaWELrDEXeE 1aa5cmqmvQq8YQTEqcTmW7dfBNuFwgdCD --txindex 0 --satoshis 3053

Default fee is set to 1000 satoshis, but can be changed with the `--fee` option.

USAGE OF THIS SCRIPT IS RISKY AND IF YOU MISTYPE ANYTHING YOU CAN LOSE ALL YOUR COINS

---

There is another python script for claiming FBTC (Fast Bitcoin). The FBTC network is based on the BitShares codebase, so it does not support Segwit. There are no TXIDs or change addresses,
and you can transfer arbitrary amounts from an address multiple times.

Usage:
    
    fbtcclaimer.py <private key in WIF format> <public source address> <destination address> <number of satoshis to send, including fee>
    fbtcclaimer.py 5K2YUVmWfxbmvsNxCsfvArXdGXm7d5DC9pn4yD75k2UaSYgkXTh 1HKqKTMpBTZZ8H5zcqYEWYBaaWELrDEXeE 1aa5cmqmvQq8YQTEqcTmW7dfBNuFwgdCD 3053
    
fbtcclaimer.py also requires aes.py to be in the same folder as the script. Thanks to https://github.com/ricmoo/pyaes for the implementation.

---

Any donations can be sent to BTC address `1HDW5sy8trGE8mEKUtNacLPGCx1WRtebnp`
