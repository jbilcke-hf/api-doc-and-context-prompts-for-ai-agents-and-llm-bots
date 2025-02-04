*   [Docs](index.html) »
*   Examples
*   [Edit on GitHub](https://github.com/BoboTiG/python-mss/blob/master/docs/source/examples.rst)

* * *

Examples[¶](#examples "Permalink to this headline")
===================================================

Basics[¶](#basics "Permalink to this headline")
-----------------------------------------------

### One screen shot per monitor[¶](#one-screen-shot-per-monitor "Permalink to this headline")

for filename in sct.save():
    print(filename)

### Screen shot of the monitor 1[¶](#screen-shot-of-the-monitor-1 "Permalink to this headline")

filename \= sct.shot()
print(filename)

### A screen shot to grab them all[¶](#a-screen-shot-to-grab-them-all "Permalink to this headline")

filename \= sct.shot(mon\=-1, output\='fullscreen.png')
print(filename)

### Callback[¶](#callback "Permalink to this headline")

Screen shot of the monitor 1 with a callback:

import os.path

import mss

def on\_exists(fname: str) \-> None:
    """
    Callback example when we try to overwrite an existing screenshot.
    """

    if os.path.isfile(fname):
        newfile \= f"{fname}.old"
        print(f"{fname} -> {newfile}")
        os.rename(fname, newfile)

with mss.mss() as sct:
    filename \= sct.shot(output\="mon-{mon}.png", callback\=on\_exists)
    print(filename)

### Part of the screen[¶](#part-of-the-screen "Permalink to this headline")

You can capture only a part of the screen:

import mss.tools

with mss.mss() as sct:
    \# The screen part to capture
    monitor \= {"top": 160, "left": 160, "width": 160, "height": 135}
    output \= "sct-{top}x{left}\_{width}x{height}.png".format(\*\*monitor)

    \# Grab the data
    sct\_img \= sct.grab(monitor)

    \# Save to the picture file
    mss.tools.to\_png(sct\_img.rgb, sct\_img.size, output\=output)
    print(output)

New in version 3.0.0.

### Part of the screen of the 2nd monitor[¶](#part-of-the-screen-of-the-2nd-monitor "Permalink to this headline")

This is an example of capturing some part of the screen of the monitor 2:

import mss.tools

with mss.mss() as sct:
    \# Get information of monitor 2
    monitor\_number \= 2
    mon \= sct.monitors\[monitor\_number\]

    \# The screen part to capture
    monitor \= {
        "top": mon\["top"\] + 100,  \# 100px from the top
        "left": mon\["left"\] + 100,  \# 100px from the left
        "width": 160,
        "height": 135,
        "mon": monitor\_number,
    }
    output \= "sct-mon{mon}\_{top}x{left}\_{width}x{height}.png".format(\*\*monitor)

    \# Grab the data
    sct\_img \= sct.grab(monitor)

    \# Save to the picture file
    mss.tools.to\_png(sct\_img.rgb, sct\_img.size, output\=output)
    print(output)

New in version 3.0.0.

### Use PIL bbox style and percent values[¶](#use-pil-bbox-style-and-percent-values "Permalink to this headline")

You can use the same value as you would do with `PIL.ImageGrab(bbox=tuple(...))`. This is an example that uses it, but also using percentage values:

import mss.tools

with mss.mss() as sct:
    \# Use the 1st monitor
    monitor \= sct.monitors\[1\]

    \# Capture a bbox using percent values
    left \= monitor\["left"\] + monitor\["width"\] \* 5 // 100  \# 5% from the left
    top \= monitor\["top"\] + monitor\["height"\] \* 5 // 100  \# 5% from the top
    right \= left + 400  \# 400px width
    lower \= top + 400  \# 400px height
    bbox \= (left, top, right, lower)

    \# Grab the picture
    \# Using PIL would be something like:
    \# im = ImageGrab(bbox=bbox)
    im \= sct.grab(bbox)

    \# Save it!
    mss.tools.to\_png(im.rgb, im.size, output\="screenshot.png")

New in version 3.1.0.

### PNG Compression[¶](#png-compression "Permalink to this headline")

You can tweak the PNG compression level (see [`zlib.compress()`](https://docs.python.org/3/library/zlib.html#zlib.compress "(in Python v3.11)") for details):

sct.compression\_level \= 2

New in version 3.2.0.

### Get PNG bytes, no file output[¶](#get-png-bytes-no-file-output "Permalink to this headline")

You can get the bytes of the PNG image:

with mss.mss() as sct:
    \# The monitor or screen part to capture
    monitor \= sct.monitors\[1\]  \# or a region

    \# Grab the data
    sct\_img \= sct.grab(monitor)

    \# Generate the PNG
    png \= mss.tools.to\_png(sct\_img.rgb, sct\_img.size)

Advanced[¶](#advanced "Permalink to this headline")
---------------------------------------------------

You can handle data using a custom class:

import mss
from mss.models import Monitor
from mss.screenshot import ScreenShot

class SimpleScreenShot(ScreenShot):
    """
    Define your own custom method to deal with screen shot raw data.
    Of course, you can inherit from the ScreenShot class and change
    or add new methods.
    """

    def \_\_init\_\_(self, data: bytearray, monitor: Monitor, \*\*\_: Any) \-> None:
        self.data \= data
        self.monitor \= monitor

with mss.mss() as sct:
    sct.cls\_image \= SimpleScreenShot
    image \= sct.grab(sct.monitors\[1\])
    \# ...

New in version 3.1.0.

PIL[¶](#pil "Permalink to this headline")
-----------------------------------------

You can use the Python Image Library (aka Pillow) to do whatever you want with raw pixels. This is an example using [frombytes()](http://pillow.readthedocs.io/en/latest/reference/Image.html#PIL.Image.frombytes):

import mss

with mss.mss() as sct:
    \# Get rid of the first, as it represents the "All in One" monitor:
    for num, monitor in enumerate(sct.monitors\[1:\], 1):
        \# Get raw pixels from the screen
        sct\_img \= sct.grab(monitor)

        \# Create the Image
        img \= Image.frombytes("RGB", sct\_img.size, sct\_img.bgra, "raw", "BGRX")
        \# The same, but less efficient:
        \# img = Image.frombytes('RGB', sct\_img.size, sct\_img.rgb)

        \# And save it!
        output \= f"monitor-{num}.png"
        img.save(output)
        print(output)

New in version 3.0.0.

### Playing with pixels[¶](#playing-with-pixels "Permalink to this headline")

This is an example using [putdata()](https://github.com/python-pillow/Pillow/blob/b9b5d39f2b32cec75b9cf96b882acb7a77a4ed4b/PIL/Image.py#L1523):

import mss

with mss.mss() as sct:
    \# Get a screenshot of the 1st monitor
    sct\_img \= sct.grab(sct.monitors\[1\])

    \# Create an Image
    img \= Image.new("RGB", sct\_img.size)

    \# Best solution: create a list(tuple(R, G, B), ...) for putdata()
    pixels \= zip(sct\_img.raw\[2::4\], sct\_img.raw\[1::4\], sct\_img.raw\[::4\])
    img.putdata(list(pixels))

    \# But you can set individual pixels too (slower)
    """
    pixels = img.load()
    for x in range(sct\_img.width):
        for y in range(sct\_img.height):
            pixels\[x, y\] = sct\_img.pixel(x, y)
    """

    \# Show it!
    img.show()

New in version 3.0.0.

OpenCV/Numpy[¶](#opencv-numpy "Permalink to this headline")
-----------------------------------------------------------

See how fast you can record the screen. You can easily view a HD movie with VLC and see it too in the OpenCV window. And with \_\_no\_\_ lag please.

import cv2
import numpy

import mss

with mss.mss() as sct:
    \# Part of the screen to capture
    monitor \= {"top": 40, "left": 0, "width": 800, "height": 640}

    while "Screen capturing":
        last\_time \= time.time()

        \# Get raw pixels from the screen, save it to a Numpy array
        img \= numpy.array(sct.grab(monitor))

        \# Display the picture
        cv2.imshow("OpenCV/Numpy normal", img)

        \# Display the picture in grayscale
        \# cv2.imshow('OpenCV/Numpy grayscale',
        \#            cv2.cvtColor(img, cv2.COLOR\_BGRA2GRAY))

        print(f"fps: {1 / (time.time() \- last\_time)}")

        \# Press "q" to quit
        if cv2.waitKey(25) & 0xFF \== ord("q"):
            cv2.destroyAllWindows()
            break

New in version 3.0.0.

FPS[¶](#fps "Permalink to this headline")
-----------------------------------------

### Benchmark[¶](#benchmark "Permalink to this headline")

Simple naive benchmark to compare with [Reading game frames in Python with OpenCV - Python Plays GTA V](https://pythonprogramming.net/game-frames-open-cv-python-plays-gta-v/):

import cv2
import numpy

import mss

def screen\_record() \-> int:
    try:
        from PIL import ImageGrab
    except ImportError:
        return 0

    \# 800x600 windowed mode
    mon \= (0, 40, 800, 640)

    title \= "\[PIL.ImageGrab\] FPS benchmark"
    fps \= 0
    last\_time \= time.time()

    while time.time() \- last\_time < 1:
        img \= numpy.asarray(ImageGrab.grab(bbox\=mon))
        fps += 1

        cv2.imshow(title, cv2.cvtColor(img, cv2.COLOR\_BGR2RGB))
        if cv2.waitKey(25) & 0xFF \== ord("q"):
            cv2.destroyAllWindows()
            break

    return fps

def screen\_record\_efficient() \-> int:
    \# 800x600 windowed mode
    mon \= {"top": 40, "left": 0, "width": 800, "height": 640}

    title \= "\[MSS\] FPS benchmark"
    fps \= 0
    sct \= mss.mss()
    last\_time \= time.time()

    while time.time() \- last\_time < 1:
        img \= numpy.asarray(sct.grab(mon))
        fps += 1

        cv2.imshow(title, img)
        if cv2.waitKey(25) & 0xFF \== ord("q"):
            cv2.destroyAllWindows()
            break

    return fps

print("PIL:", screen\_record())
print("MSS:", screen\_record\_efficient())

New in version 3.0.0.

### Multiprocessing[¶](#multiprocessing "Permalink to this headline")

Performances can be improved by delegating the PNG file creation to a specific worker. This is a simple example using the [`multiprocessing`](https://docs.python.org/3/library/multiprocessing.html#module-multiprocessing "(in Python v3.11)") inspired by the [TensorFlow Object Detection Introduction](https://github.com/pythonlessons/TensorFlow-object-detection-tutorial) project:

import mss
import mss.tools

def grab(queue: Queue) \-> None:
    rect \= {"top": 0, "left": 0, "width": 600, "height": 800}

    with mss.mss() as sct:
        for \_ in range(1\_000):
            queue.put(sct.grab(rect))

    \# Tell the other worker to stop
    queue.put(None)

def save(queue: Queue) \-> None:
    number \= 0
    output \= "screenshots/file\_{}.png"
    to\_png \= mss.tools.to\_png

    while "there are screenshots":
        img \= queue.get()
        if img is None:
            break

        to\_png(img.rgb, img.size, output\=output.format(number))
        number += 1

if \_\_name\_\_ \== "\_\_main\_\_":
    \# The screenshots queue
    queue: Queue \= Queue()

    \# 2 processes: one for grabing and one for saving PNG files
    Process(target\=grab, args\=(queue,)).start()
    Process(target\=save, args\=(queue,)).start()

New in version 5.0.0.

BGRA to RGB[¶](#bgra-to-rgb "Permalink to this headline")
---------------------------------------------------------

Different possibilities to convert raw BGRA values to RGB:

def mss\_rgb(im):
    """ Better than Numpy versions, but slower than Pillow. """
    return im.rgb

def numpy\_flip(im):
    """ Most efficient Numpy version as of now. """
    frame \= numpy.array(im, dtype\=numpy.uint8)
    return numpy.flip(frame\[:, :, :3\], 2).tobytes()

def numpy\_slice(im):
    """ Slow Numpy version. """
    return numpy.array(im, dtype\=numpy.uint8)\[..., \[2, 1, 0\]\].tobytes()

def pil\_frombytes(im):
    """ Efficient Pillow version. """
    return Image.frombytes('RGB', im.size, im.bgra, 'raw', 'BGRX').tobytes()

with mss.mss() as sct:
    im \= sct.grab(sct.monitors\[1\])
    rgb \= pil\_frombytes(im)
    ...

New in version 3.2.0.

[Next](support.html "Support") [Previous](usage.html "Usage")

* * *

© Copyright 2013-2023, Mickaël 'Tiger-222' Schoentgen & contributors Revision `a8635053`.

Built with [Sphinx](http://sphinx-doc.org/) using a [theme](https://github.com/rtfd/sphinx_rtd_theme) provided by [Read the Docs](https://readthedocs.org).
