*   [Docs](index.html) »
*   Usage
*   [Edit on GitHub](https://github.com/BoboTiG/python-mss/blob/master/docs/source/usage.rst)

* * *

Usage[¶](#usage "Permalink to this headline")
=============================================

Import[¶](#import "Permalink to this headline")
-----------------------------------------------

So MSS can be used as simply as:

from mss import mss

Or import the good one based on your operating system:

\# MacOS X
from mss.darwin import MSS as mss

\# GNU/Linux
from mss.linux import MSS as mss

\# Microsoft Windows
from mss.windows import MSS as mss

Instance[¶](#instance "Permalink to this headline")
---------------------------------------------------

So the module can be used as simply as:

with mss() as sct:
    \# ...

Intensive Use[¶](#intensive-use "Permalink to this headline")
-------------------------------------------------------------

If you plan to integrate MSS inside your own module or software, pay attention to using it wisely.

This is a bad usage:

for \_ in range(100):
    with mss() as sct:
        sct.shot()

This is a much better usage, memory efficient:

with mss() as sct:
    for \_ in range(100):
        sct.shot()

Also, it is a good thing to save the MSS instance inside an attribute of your class and calling it when needed.

### GNU/Linux[¶](#gnu-linux "Permalink to this headline")

On GNU/Linux, you can specify which display to use (useful for distant screenshots via SSH):

with mss(display\=":0.0") as sct:
    \# ...

A more specific example (only valid on GNU/Linux):

with mss.mss(display\=":0.0") as sct:
    for filename in sct.save():
        print(filename)

Command Line[¶](#command-line "Permalink to this headline")
-----------------------------------------------------------

You can use `mss` via the CLI:

mss \--help

Or via direct call from Python:

$ python -m mss --help
usage: \_\_main\_\_.py \[-h\] \[-c COORDINATES\] \[-l {0,1,2,3,4,5,6,7,8,9}\]
                \[-m MONITOR\] \[-o OUTPUT\] \[-q\] \[-v\] \[--with-cursor\]

options:
-h, --help            show this help message and exit
-c COORDINATES, --coordinates COORDINATES
                      the part of the screen to capture: top, left, width, height
-l {0,1,2,3,4,5,6,7,8,9}, --level {0,1,2,3,4,5,6,7,8,9}
                      the PNG compression level
-m MONITOR, --monitor MONITOR
                      the monitor to screen shot
-o OUTPUT, --output OUTPUT
                      the output file name
--with-cursor         include the cursor
-q, --quiet           do not print created files
-v, --version         show program's version number and exit

New in version 3.1.1.

New in version 8.0.0: `--with-cursor` to include the cursor in screenshots.

[Next](examples.html "Examples") [Previous](installation.html "Installation")

* * *

© Copyright 2013-2023, Mickaël 'Tiger-222' Schoentgen & contributors Revision `a8635053`.

Built with [Sphinx](http://sphinx-doc.org/) using a [theme](https://github.com/rtfd/sphinx_rtd_theme) provided by [Read the Docs](https://readthedocs.org).
