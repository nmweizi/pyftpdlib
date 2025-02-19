|  |downloads| |stars| |forks| |contributors| |coverage|
|  |version| |packages| |license|
|  |github-actions| |appveyor| |doc| |twitter|

.. |downloads| image:: https://img.shields.io/pypi/dm/pyftpdlib.svg
    :target: https://pepy.tech/project/pyftpdlib
    :alt: Downloads

.. |stars| image:: https://img.shields.io/github/stars/giampaolo/pyftpdlib.svg
    :target: https://github.com/giampaolo/pyftpdlib/stargazers
    :alt: Github stars

.. |forks| image:: https://img.shields.io/github/forks/giampaolo/pyftpdlib.svg
    :target: https://github.com/giampaolo/pyftpdlib/network/members
    :alt: Github forks

.. |contributors| image:: https://img.shields.io/github/contributors/giampaolo/pyftpdlib.svg
    :target: https://github.com/giampaolo/pyftpdlib/graphs/contributors
    :alt: Contributors

.. |github-actions| image:: https://github.com/giampaolo/pyftpdlib/actions/workflows/tests.yml/badge.svg
    :target: https://github.com/giampaolo/pyftpdlib/actions/workflows/tests.yml
    :alt: Linux, macOS, Windows tests

.. |appveyor| image:: https://img.shields.io/appveyor/build/giampaolo/pyftpdlib/master.svg?label=windows%20tests
    :target: https://ci.appveyor.com/project/giampaolo/pyftpdlib
    :alt: Windows tests (Appveyor)

.. |coverage| image:: https://coveralls.io/repos/github/giampaolo/pyftpdlib/badge.svg?branch=master
    :target: https://coveralls.io/github/giampaolo/pyftpdlib?branch=master
    :alt: Test coverage (coverall.io)

.. |doc| image:: https://readthedocs.org/projects/pyftpdlib/badge/?version=latest
    :target: https://pyftpdlib.readthedocs.io/en/latest/
    :alt: Documentation Status

.. |version| image:: https://img.shields.io/pypi/v/pyftpdlib.svg?label=pypi
    :target: https://pypi.org/project/pyftpdlib
    :alt: Latest version

.. |packages| image:: https://repology.org/badge/tiny-repos/python:pyftpdlib.svg
    :target: https://repology.org/metapackage/python:pyftpdlib/versions
    :alt: Binary packages

.. |license| image:: https://img.shields.io/pypi/l/pyftpdlib.svg
    :target: https://github.com/giampaolo/pyftpdlib/blob/master/LICENSE
    :alt: License

.. |twitter| image:: https://img.shields.io/twitter/follow/grodola.svg?label=follow&style=flat&logo=twitter&logoColor=4FADFF
    :target: https://twitter.com/grodola
    :alt: Twitter Follow

Quick links
===========

- `Home <https://github.com/giampaolo/pyftpdlib>`__
- `Documentation <http://pyftpdlib.readthedocs.io>`__
- `Download <https://pypi.python.org/pypi/pyftpdlib/>`__
- `Blog <http://grodola.blogspot.com/search/label/pyftpdlib>`__
- `Mailing list <http://groups.google.com/group/pyftpdlib/topics>`__
- `What's new <https://github.com/giampaolo/pyftpdlib/blob/master/HISTORY.rst>`__

About
=====

Python FTP server library provides a high-level portable interface to easily
write very efficient, scalable and asynchronous FTP servers with Python. It is
the most complete `RFC-959 <http://www.faqs.org/rfcs/rfc959.html>`__ FTP server
implementation available for `Python <http://www.python.org/>`__ programming
language.

Features
========

- Extremely **lightweight**, **fast** and **scalable** (see
  `why <https://github.com/giampaolo/pyftpdlib/issues/203>`__ and
  `benchmarks <http://pyftpdlib.readthedocs.io/en/latest/benchmarks.html>`__).
- Uses **sendfile(2)** (see `pysendfile <https://github.com/giampaolo/pysendfile>`__)
  system call for uploads.
- Uses epoll() / kqueue() / select() to handle concurrency asynchronously.
- ...But can optionally skip to a
  `multiple thread / process <http://pyftpdlib.readthedocs.io/en/latest/tutorial.html#changing-the-concurrency-model>`__
  model (as in: you'll be free to block or use slow filesystems).
- Portable: entirely written in pure Python; works with Python from **2.6** to
  **3.5** by using a single code base.
- Supports **FTPS** (`RFC-4217 <http://tools.ietf.org/html/rfc4217>`__),
  **IPv6** (`RFC-2428 <ftp://ftp.rfc-editor.org/in-notes/rfc2428.txt>`__),
  **Unicode** file names (`RFC-2640 <http://tools.ietf.org/html/rfc2640>`__),
  **MLSD/MLST** commands (`RFC-3659 <ftp://ftp.rfc-editor.org/in-notes/rfc3659.txt>`__).
- Support for virtual users and virtual filesystem.
- Extremely flexible system of "authorizers" able to manage both "virtual" and
  "real" users on on both
  `UNIX <http://pyftpdlib.readthedocs.io/en/latest/tutorial.html#unix-ftp-server>`__
  and
  `Windows <http://pyftpdlib.readthedocs.io/en/latest/tutorial.html#windows-ftp-server>`__.
- `Test coverage <https://github.com/giampaolo/pyftpdlib/blob/master/pyftpdlib/test/>`__
  close to 100%.

Performances
============

Despite being written in an interpreted language, pyftpdlib has transfer rates
comparable or superior to common UNIX FTP servers written in C. It usually tends
to scale better (see `benchmarks <https://pyftpdlib.readthedocs.io/en/latest/benchmarks.html>`__)
because whereas vsftpd and proftpd use multiple processes to
achieve concurrency, pyftpdlib only uses one (see `the C10K problem <http://www.kegel.com/c10k.html>`__).

pyftpdlib vs. proftpd 1.3.4
---------------------------

+-----------------------------------------+----------------+----------------+-------------+
| **benchmark type**                      | **pyftpdlib**  | **proftpd**    | **speedup** |
+-----------------------------------------+----------------+----------------+-------------+
| STOR (client -> server)                 |  585.90 MB/sec | 600.49 MB/sec  | -0.02x      |
+-----------------------------------------+----------------+----------------+-------------+
| RETR (server -> client)                 | 1652.72 MB/sec | 1524.05 MB/sec | **+0.08**   |
+-----------------------------------------+----------------+----------------+-------------+
| 300 concurrent clients (connect, login) |    0.19 secs   | 9.98 secs      | **+51x**    |
+-----------------------------------------+----------------+----------------+-------------+
| STOR (1 file with 300 idle clients)     |  585.59 MB/sec | 518.55 MB/sec  | **+0.1x**   |
+-----------------------------------------+----------------+----------------+-------------+
| RETR (1 file with 300 idle clients)     | 1497.58 MB/sec | 1478.19 MB/sec | 0x          |
+-----------------------------------------+----------------+----------------+-------------+
| 300 concurrent clients (RETR 10M file)  |    3.41 secs   | 3.60 secs      | **+0.05x**  |
+-----------------------------------------+----------------+----------------+-------------+
| 300 concurrent clients (STOR 10M file)  |    8.60 secs   | 11.56 secs     | **+0.3x**   |
+-----------------------------------------+----------------+----------------+-------------+
| 300 concurrent clients (QUIT)           |    0.03 secs   | 0.39 secs      | **+12x**    |
+-----------------------------------------+----------------+----------------+-------------+

pyftpdlib vs. vsftpd 2.3.5
--------------------------

+-----------------------------------------+----------------+----------------+-------------+
| **benchmark type**                      | **pyftpdlib**  | **vsftpd**     | **speedup** |
+-----------------------------------------+----------------+----------------+-------------+
| STOR (client -> server)                 |  585.90 MB/sec | 611.73 MB/sec  | -0.04x      |
+-----------------------------------------+----------------+----------------+-------------+
| RETR (server -> client)                 | 1652.72 MB/sec | 1512.92 MB/sec | **+0.09**   |
+-----------------------------------------+----------------+----------------+-------------+
| 300 concurrent clients (connect, login) |    0.19 secs   | 20.39 secs     | **+106x**   |
+-----------------------------------------+----------------+----------------+-------------+
| STOR (1 file with 300 idle clients)     |  585.59 MB/sec | 610.23 MB/sec  | -0.04x      |
+-----------------------------------------+----------------+----------------+-------------+
| RETR (1 file with 300 idle clients)     | 1497.58 MB/sec | 1493.01 MB/sec | 0x          |
+-----------------------------------------+----------------+----------------+-------------+
| 300 concurrent clients (RETR 10M file)  |    3.41 secs   | 3.67 secs      | **+0.07x**  |
+-----------------------------------------+----------------+----------------+-------------+
| 300 concurrent clients (STOR 10M file)  |    8.60 secs   | 9.82 secs      | **+0.07x**  |
+-----------------------------------------+----------------+----------------+-------------+
| 300 concurrent clients (QUIT)           |    0.03 secs   | 0.01 secs      | +0.14x      |
+-----------------------------------------+----------------+----------------+-------------+

For more benchmarks see `here <http://pyftpdlib.readthedocs.io/en/latest/benchmarks.html>`__.

Quick start
===========

.. code-block:: python

    >>> from pyftpdlib.authorizers import DummyAuthorizer
    >>> from pyftpdlib.handlers import FTPHandler
    >>> from pyftpdlib.servers import FTPServer
    >>>
    >>> authorizer = DummyAuthorizer()
    >>> authorizer.add_user("user", "12345", "/home/giampaolo", perm="elradfmwMT")
    >>> authorizer.add_anonymous("/home/nobody")
    >>>
    >>> handler = FTPHandler
    >>> handler.authorizer = authorizer
    >>>
    >>> server = FTPServer(("127.0.0.1", 21), handler)
    >>> server.serve_forever()
    [I 13-02-19 10:55:42] >>> starting FTP server on 127.0.0.1:21 <<<
    [I 13-02-19 10:55:42] poller: <class 'pyftpdlib.ioloop.Epoll'>
    [I 13-02-19 10:55:42] masquerade (NAT) address: None
    [I 13-02-19 10:55:42] passive ports: None
    [I 13-02-19 10:55:42] use sendfile(2): True
    [I 13-02-19 10:55:45] 127.0.0.1:34178-[] FTP session opened (connect)
    [I 13-02-19 10:55:48] 127.0.0.1:34178-[user] USER 'user' logged in.
    [I 13-02-19 10:56:27] 127.0.0.1:34179-[user] RETR /home/giampaolo/.vimrc completed=1 bytes=1700 seconds=0.001
    [I 13-02-19 10:56:39] 127.0.0.1:34179-[user] FTP session closed (disconnect).

`other code samples <http://pyftpdlib.readthedocs.io/en/latest/tutorial.html>`__

Donate
======

A lot of time and effort went into making pyftpdlib as it is right now.
If you feel pyftpdlib is useful to you or your business and want to support its
future development please consider `donating <https://gmpy.dev/donate>`__ me some money.
