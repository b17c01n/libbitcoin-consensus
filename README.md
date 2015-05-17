[![Build Status](https://travis-ci.org/libbitcoin/libbitcoin-consensus.svg?branch=master)](https://travis-ci.org/libbitcoin/libbitcoin-consensus)

[![Coverage Status](https://coveralls.io/repos/libbitcoin/libbitcoin-consensus/badge.svg)](https://coveralls.io/r/libbitcoin/libbitcoin-consensus)

# Libbitcoin Consensus

*Bitcoin consensus library*

## Installation

```sh
$ ./autogen.sh
$ ./configure
$ make
$ sudo make install
$ sudo ldconfig
```

`libbitcoin-consensus` is now installed in `/usr/local/`.

## Dependencies

By default consensus has a dependency on openssl (libcrypto) and a test dependency on boost.

## Configure Options

The `--with-secp256k1` option is experimental. When this option selected there is a dependency on [libsecp256k1](https://github.com/bitcoin/secp256k1) in place of openssl. The `--without-openssl` option may be used to concurrently eliminate the openssl dependency.

There is a dependency on [boost test](http://www.boost.org/doc/libs/1_50_0/libs/test/doc/html/index.html) for `make check` builds (tests). The `--without-tests` option disables test builds and eliminates the boost dependency.

## Supported Platforms

**Ubuntu** (gcc and clang) and **OSX** (clang) are regularly tested via a [travis build matrix](https://travis-ci.org/libbitcoin/libbitcoin-consensus). There is also a Visual Studio 2013 solution for **Windows** builds (vc12). Unlike other libbitcoin libraries, consensus does not require a c++11 compiler.

## Language Bindings

Java and python bindings are automatically generated by maintainers using [SWIG](http://www.swig.org). To compile and install these bindings use the `--with-java` and `--with-python` options respectively.

The java option installs the jar file `org.libbitcoin.consensus-${VERSION}.jar`and the library `bitcoin-consensus-jni`. The python option installs the python file `consensus.py` and the library `_bitcoin-consensus`.

# About

This library includes the following 34 files considered to be bitcoin consensus-critical. These files are identical to those used in version 0.10.2 (and 0.10.1) of the Satoshi client with two exceptions. The file `pubkey.cpp` has conditionally-included sections for support of experimental [libsecp256k1](https://github.com/bitcoin/secp256k1) builds against the current library. The file `ecwrapper.cpp` has conditional exclusion of the entire file when `secp256k1` is in use. These changes are excluded in OpenSSL (consensus) builds.

```
amount.h
eccryptoverify.cpp
eccryptoverify.h
ecwrapper.cpp
ecwrapper.h
hash.cpp
hash.h
pubkey.cpp
pubkey.h
serialize.h
tinyformat.h
uint256.cpp
uint256.h
utilstrencodings.cpp
utilstrencodings.h
version.h
crypto/common.h
crypto/hmac_sha512.cpp
crypto/hmac_sha512.h
crypto/ripemd160.cpp
crypto/ripemd160.h
crypto/sha1.cpp
crypto/sha1.h
crypto/sha256.cpp
crypto/sha256.h
crypto/sha512.cpp
crypto/sha512.h
primitives/transaction.cpp
primitives/transaction.h
script/interpreter.cpp
script/interpreter.h
script/script.cpp
script/script.h
script/script_error.h
```

# Libbitcoin Integration

Libbitcoin natively implements consensus checks that are redundant with `libbitcoin-consensus`. Libbitcoin includes a full bitcoin client and server SDK. This includes the full node implementation [libbitcoin-node](https://github.com/libbitcoin/libbitcoin-node), which builds on [libbitcoin](https://github.com/libbitcoin/libbitcoin) and [libbitcoin-blockchain](https://github.com/libbitcoin/libbitcoin-blockchain).

The `libbitcoin-blockchain` configuration now provides the `--with-consensus` option. This allows the developer to select either `libbitcoin` native or `libbitcoin-consensus` checks. The option now defaults to `yes` so that by default all `libbitcoin-node` and `libbitcoin-server` builds use the same consensus checks as a Satoshi node.
