=============
python-zstd
=============

.. image:: https://travis-ci.org/sergey-dryabzhinsky/python-zstd.svg?branch=master
    :target: https://travis-ci.org/sergey-dryabzhinsky/python-zstd

Simple python bindings to Yann Collet ZSTD compression library

**Zstd**, short for Zstandard, is a new lossless compression algorithm,
 which provides both good compression ratio *and* speed for your standard compression needs.
 "Standard" translates into everyday situations which neither look for highest possible ratio
 (which LZMA and ZPAQ cover) nor extreme speeds (which LZ4 covers).

It is provided as a BSD-license package, hosted on GitHub_.

.. _GitHub: https://github.com/facebook/zstd


WARNING!!!
----------

If you setup 1.0.0.99.1 version - remove it manualy to able to update.
PIP matching version strings not tuple of numbers.

Result generated by versions prior to 1.0.0.99.1 is not compatible with orignial Zstd
by any means. It generates custom header and can be read only by zstd python module.

As of 1.0.0.99.1 version it uses standard Zstd output, not modified.

To prevent data loss there is two functions now: ```compress_old``` and ```decompress_old```.
They are works just like in old versions prior to 1.0.0.99.1.

As of 1.1.4 version module build without them by default.

As of 1.3.4 version these functions are deprecated and will be removed in future releases.


DISCLAIMER
__________

These python bindings are kept simple and blunt.

Support of dictionaries is not planned.


LINKS
-----

* Zstandard: https://github.com/facebook/zstd
* More full-featured and compatible with Zstandard python bindings by Gregory Szorc: https://pypi.python.org/pypi/zstandard


Build from source
-----------------

   >>> $ git clone https://github.com/sergey-dryabzhinsky/python-zstd
   >>> $ git submodule update --init
   >>> $ apt-get install python-dev python3-dev python-setuptools python3-setuptools
   >>> $ python setup.py build_ext clean
   >>> $ python3 setup.py build_ext clean

Note: legacy format support disabled by default.
To build with Zstd legacy versions support - pass ``--legacy`` option to setup.py script:

   >>> $ python setup.py build_ext --legacy clean

Note: PyZstd legacy format support disabled by default.
To build with python-zstd legacy format support (pre 1.1.2) - pass ``--pyzstd-legacy`` option to setup.py script:

   >>> $ python setup.py build_ext --pyzstd-legacy clean

If you want to build with existing distribution of libzstd just add ``--external`` option.
But beware! Legacy formats support is unknown in this case.
And if your version not equal with python-zstd - tests may not pass.

   >>> $ python setup.py build_ext --external clean

If paths to header file ``zstd.h`` and libraries is uncommon - use common ``build`` params:
--libraries --include-dirs --library-dirs.

   >>> $ python setup.py build_ext --external --include-dirs /opt/zstd/usr/include --libraries zstd --library-dirs /opt/zstd/lib clean


Install from pypi
-----------------

   >>> # for Python 2.6+
   >>> $ pip install zstd
   >>> # or for Python 3.2+
   >>> $ pip3 install zstd


Use
___

Module has simple API:

   >>> import zstd
   >>> dir(zstd)
   ['Error', 'ZSTD_compress', 'ZSTD_uncompress', 'ZSTD_version', 'ZSTD_version_number', '__doc__', '__file__', '__name__', '__package__', 'compress', 'decompress', 'dumps', 'loads', 'uncompress', 'version']
   >>> zstd.version()
   '1.3.8.0'
   >>> zstd.ZSTD_version()
   '1.3.8'
   >>> zstd.ZSTD_version_number()
   10308
   >>> data = "123456qwert"
   >>> cdata = zstd.compress(data, 1)
   >>> data == zstd.decompress(cdata)
   True


Note: these functions are aliases:

* dumps - to compress
* loads, uncompress - to decompress
