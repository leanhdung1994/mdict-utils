This fork increses significantly the speed of generating MDX from TXTs by

- replacing `zlib <https://docs.python.org/3/library/zlib.html>`_ with `deflate <https://github.com/dcwatson/deflate>`_.

- employing the paradigm *compress blocks in parallel and write them sequentially in batch*.

For testing, I generate MDX from a 8.77GB TXT file containing 1.992.410 entries (the French Wiktionary):

.. code-block:: console

      Running fork: liuyug
      URL         : https://codeload.github.com/liuyug/mdict-utils/zip/refs/heads/master
    ==============================
    Creating virtual environment...
    Installing package from https://codeload.github.com/liuyug/mdict-utils/zip/refs/heads/master ...
    Running tests (mdx_test.py) ...
    Scan "D:\result\bin_0_frwiktionary.txt": 1992410

    Pack to "E:\tmp\bin_0_frwiktionary.mdx"
    100%|████████████████████████████████████████████████████████████████████| 1992410/1992410 [01:38<00:00, 20135.71rec/s]
                        --- Elapsed time: 226.030665 seconds ---
    Removing virtual environment...
    Finished cleanup for liuyug
    ==============================


      Running fork: leanhdung1994
      URL         : https://codeload.github.com/leanhdung1994/mdict-utils/zip/refs/heads/master
    ==============================
    Creating virtual environment...
    Installing package from https://codeload.github.com/leanhdung1994/mdict-utils/zip/refs/heads/master ...
    Running tests (mdx_test.py) ...
    Scan "D:\result\bin_0_frwiktionary.txt": 1992410

    Pack to "E:\tmp\bin_0_frwiktionary.mdx"
    100%|███████████████████████████████████████████████████████████████████| 1992410/1992410 [00:10<00:00, 188208.58rec/s]
                        --- Elapsed time: 129.658956 seconds ---
    Removing virtual environment...
    Finished cleanup for leanhdung1994
    ==============================

The compression throughput is increased from ``20135.71rec/s`` to ``188208.58rec/s``. As such, the compression time is reduced from ``1m38s`` to ``10s``.

==========

MDict Tool
==========

MDict pack/unpack tool

.. NOTE::

    Support Reading with MDict Version 3.0

    Support Reading and Writing with MDict Version 2.0

    All files must be UTF-8 encoding, include HTML and TXT


Install
=======
::

    pip install mdict-utils

Usage
=====
Meta information::

    mdict -m dict.mdx

All key list::

    mdict -k dict.mdx

Query key::

    mdict -q <word> dict.mdx

.. note::

    只用于测试词典打包是否正确。

Unpack
------
Unpack MDX::

    mdict -x dict.mdx -d ./mdx

Unpack MDX/MDD and split into 5 files::

    mdict -x dict.mdx -d ./mdx --split-n 5

Unpack MDX/MDD and split into a...z files::

    mdict -x dict.mdx -d ./mdx --split-az

Unpack MDD::

    mdict -x dict.mdd -d ./mdd

Unpack MDX/MDD to sqlite3 DB::

    mdict -x dict.mdx --exdb
    mdict -x dict.mdd --exdb

Unpack MDX/MDD to sqlite3 DB with zip compress::

    mdict -x dict.mdx --exdb-zip

Pack
----
Pack MDX::

    mdict --title title.html --description description.html -a dict.txt dict.mdx

Pack MDX with many TXT files::

    mdict --title title.html --description description.html -a dict.part1.txt -a dict.part2.txt dict.mdx

or::

    mdict --title title.html --description description.html -a txt_dir dict.mdx

Pack MDD::

    mdict --title title.html --description description.html -a mdd_dir dict.mdd

Other
-----
Convert TXT to sqlite3 DB::

    mdict --txt-db dict.txt

Convert sqlite3 DB to TXT::

    mdict --db-txt dict.db


Reference
=========

+   https://bitbucket.org/xwang/mdict-analysis
+   https://github.com/zhansliu/writemdict

Donate 捐赠
=============
请捐赠者在 issue 里留下捐赠信息，如交易流水号等，否则无法在支付系统里查找。再次感谢。

.. image:: alipay_pay.jpg
    :width: 45%
.. image:: wx_pay.png
    :width: 45%
