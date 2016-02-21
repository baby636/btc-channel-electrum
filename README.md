BTC Channel Electrum
====================

This package contains the system gateway for assigning and making requests to the system default payment channel.

Notes
-----

Upon release, this package and the uses described below conform to v0.1 of the Bitcoin Computer Project API. This version of the API is extremely preliminary.

Installation
------------

1. [Download and install Electrum](https://electrum.org/#download)
2. Install jsonrpclib: `#> pip install jsonrpclib`
2. [Download and install btc-channel](https://github.com/BitcoinComputer/btc-channel)
3. Download and install btc-channel-electrum:
  ```
    $> wget FILL_ME_IN
    $> tar -xvf FILL_ME_IN
    $> cd FILL_ME_IN
    $> ./configure
    $> make
    #> make install
  ```
  
Configuration
-------------

If you haven't alreadly initialized Electrum with a wallet, do so.
```
$> electrum create
```

Assign a JSON-RPC port to Electrum and set that port in electrum-btc-channel.
```
$> electrum setconfig rpcport 7777
#> btc-channel-electrum --configure --port=7777
```

Assign the Electrum channel as the system default btc-channel.
```
#> btc-channel --configure --channel=btc-channel-electrum
```

Use
---

Electrum must be running for you to use btc-channel-electrum. You can start Electrum as a daemon service by typing:
```
$> nohup electrum -g jsonrpc &
```

Create a payment request for 0.258 Bitcoin. Amount must be given in Satoshi. Provides a payment request id to stdout, eg: `543df896f34321e985fec37ea0de69d5`.
```
$> btc-channel --create -amount 25800000
```

Generate a payment request body for request `543df896f34321e985fec37ea0de69d5`. Request body shall be in Bitcoin URI formatted BIP21.
```
btc-channel 543df896f34321e985fec37ea0de69d5 --body
```

Query whether payment request `543df896f34321e985fec37ea0de69d5` has been paid. Will stdout a -1 if unfulfilled, 0 if fulfilled.
```
btc-channel 543df896f34321e985fec37ea0de69d5 --verify-payment
```
