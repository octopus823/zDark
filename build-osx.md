Copyright (c) 2009-2012 Bitcoin Developers
Distributed under the MIT/X11 software license, see the accompanying
file license.txt or http://www.opensource.org/licenses/mit-license.php.
This product includes software developed by the OpenSSL Project for use in
the OpenSSL Toolkit (http://www.openssl.org/).  This product includes
cryptographic software written by Eric Young (eay@cryptsoft.com) and UPnP
software written by Thomas Bernard.


OSX BUILD NOTES
================

System requirements
--------------------

Mac OS X, Mac OS Sierra or Mac OS High Sierra

It would be better to use Mac OS X on VMWare Fusion for version compatibility.



Preparation
---------------

Installing QT on Mac OS

 Download QT from [http://download.qt.io/archive/qt/5.10/5.10.1/qt-opensource-mac-x64-5.10.1.dmg](http://download.qt.io/archive/qt/5.10/5.10.1/qt-opensource-mac-x64-5.10.1.dmg) and install it.


Dependency Build Instructions:
----------------------------------------------

#### Install Homebrew if not.

    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

#### Install dependencies using Homebrew

    brew install boost miniupnpc openssl berkeley-db@4

Link dependecies:

    brew link boost --force
    brew link berkeley-db@4 --force
    brew link openssl --force
    brew link miniupnpc --force


### Compiling Linda QT wallet

Clone the Lindacoin repository
```
git clone https://github.com/Lindacoin/Linda.git
```

#### Use Qt Creator as IDE

Open Linda-qt.pro with Qt Creator.
Select the default "Desktop" kit and select "Clang (x86 64bit in /usr/bin)" as compiler.
Edit Linda-qt.pro like this.


    # platform specific defaults, if not overridden on command line
    isEmpty(BOOST_LIB_SUFFIX) {
        macx:BOOST_LIB_SUFFIX = -mt
        windows:BOOST_LIB_SUFFIX = -mt
    }

    isEmpty(BOOST_THREAD_LIB_SUFFIX) {
        BOOST_THREAD_LIB_SUFFIX = $$BOOST_LIB_SUFFIX
    }

    isEmpty(BDB_LIB_PATH) {
        macx:BDB_LIB_PATH = /usr/local/opt/berkeley-db@4/lib
    }

    isEmpty(BDB_LIB_SUFFIX) {   
        macx:BDB_LIB_SUFFIX = -4.8
    }

    isEmpty(BDB_INCLUDE_PATH) {
        macx:BDB_INCLUDE_PATH = /usr/local/opt/berkeley-db@4/include
    }

    isEmpty(BOOST_LIB_PATH) {
        macx:BOOST_LIB_PATH = /usr/local/opt/boost@1.60/lib
    }

    isEmpty(BOOST_INCLUDE_PATH) {   
        macx:BOOST_INCLUDE_PATH = /usr/local/opt/boost@1.60/include
    }

    isEmpty(OPENSSL_LIB_PATH) {
        macx:OPENSSL_LIB_PATH = /usr/local/opt/openssl/lib
    }

    isEmpty(OPENSSL_INCLUDE_PATH) {
        macx:OPENSSL_INCLUDE_PATH = /usr/local/opt/openssl/include
    }



    isEmpty(MINIUPNPC_LIB_PATH) {
        macx:MINIUPNPC_LIB_PATH = /usr/local/opt/miniupnpc/lib
    }

    isEmpty(MINIUPNPC_INCLUDE_PATH) {
        macx:MINIUPNPC_INCLUDE_PATH = /usr/local/opt/miniupnpc/include
    }

Build/Run qmake
Build/Build Project "Linda-qt" or Build/Run

It will generate Linda-Qt.app in build-Linda-qt-Desktop_Qt_{QT_VERSION}_clang_64bit-{Release|Debug}.


