*   [Docs](index.html) »
*   MSS API
*   [Edit on GitHub](https://github.com/BoboTiG/python-mss/blob/master/docs/source/api.rst)

* * *

MSS API[¶](#mss-api "Permalink to this headline")
=================================================

Classes[¶](#classes "Permalink to this headline")
-------------------------------------------------

### macOS[¶](#module-mss.darwin "Permalink to this headline")

`mss.darwin.``CFUNCTIONS`[¶](#mss.darwin.CFUNCTIONS "Permalink to this definition")

New in version 6.1.0.

`mss.darwin.``cgfloat`()[¶](#mss.darwin.cgfloat "Permalink to this definition")

_class_ `mss.darwin.``CGPoint`[¶](#mss.darwin.CGPoint "Permalink to this definition")

_class_ `mss.darwin.``CGSize`[¶](#mss.darwin.CGSize "Permalink to this definition")

_class_ `mss.darwin.``CGRect`[¶](#mss.darwin.CGRect "Permalink to this definition")

_class_ `mss.darwin.``MSS`[¶](#mss.darwin.MSS "Permalink to this definition")

`core`[¶](#mss.darwin.MSS.core "Permalink to this definition")

`max_displays`[¶](#mss.darwin.MSS.max_displays "Permalink to this definition")

### GNU/Linux[¶](#module-mss.linux "Permalink to this headline")

`mss.linux.``CFUNCTIONS`[¶](#mss.linux.CFUNCTIONS "Permalink to this definition")

New in version 6.1.0.

`mss.linux.``PLAINMASK`[¶](#mss.linux.PLAINMASK "Permalink to this definition")

`mss.linux.``ZPIXMAP`[¶](#mss.linux.ZPIXMAP "Permalink to this definition")

_class_ `mss.linux.``Display`[¶](#mss.linux.Display "Permalink to this definition")

Structure that serves as the connection to the X server, and that contains all the information about that X server.

_class_ `mss.linux.``Event`[¶](#mss.linux.Event "Permalink to this definition")

XErrorEvent to debug eventual errors.

_class_ `mss.linux.``XFixesCursorImage`[¶](#mss.linux.XFixesCursorImage "Permalink to this definition")

Cursor structure

_class_ `mss.linux.``XImage`[¶](#mss.linux.XImage "Permalink to this definition")

Description of an image as it exists in the client’s memory.

_class_ `mss.linux.``XRRCrtcInfo`[¶](#mss.linux.XRRCrtcInfo "Permalink to this definition")

Structure that contains CRTC information.

_class_ `mss.linux.``XRRModeInfo`[¶](#mss.linux.XRRModeInfo "Permalink to this definition")

_class_ `mss.linux.``XRRScreenResources`[¶](#mss.linux.XRRScreenResources "Permalink to this definition")

Structure that contains arrays of XIDs that point to the available outputs and associated CRTCs.

_class_ `mss.linux.``XWindowAttributes`[¶](#mss.linux.XWindowAttributes "Permalink to this definition")

Attributes for the specified window.

_class_ `mss.linux.``MSS`[¶](#mss.linux.MSS "Permalink to this definition")

`close`()[¶](#mss.linux.MSS.close "Permalink to this definition")

Clean-up method.

New in version 8.0.0.

### Windows[¶](#module-mss.windows "Permalink to this headline")

`mss.windows.``CAPTUREBLT`[¶](#mss.windows.CAPTUREBLT "Permalink to this definition")

`mss.windows.``CFUNCTIONS`[¶](#mss.windows.CFUNCTIONS "Permalink to this definition")

New in version 6.1.0.

`mss.windows.``DIB_RGB_COLORS`[¶](#mss.windows.DIB_RGB_COLORS "Permalink to this definition")

`mss.windows.``SRCCOPY`[¶](#mss.windows.SRCCOPY "Permalink to this definition")

_class_ `mss.windows.``BITMAPINFOHEADER`[¶](#mss.windows.BITMAPINFOHEADER "Permalink to this definition")

_class_ `mss.windows.``BITMAPINFO`[¶](#mss.windows.BITMAPINFO "Permalink to this definition")

`mss.windows.``MONITORNUMPROC`[¶](#mss.windows.MONITORNUMPROC "Permalink to this definition")

New in version 6.1.0.

_class_ `mss.windows.``MSS`[¶](#mss.windows.MSS "Permalink to this definition")

`gdi32`[¶](#mss.windows.MSS.gdi32 "Permalink to this definition")

`user32`[¶](#mss.windows.MSS.user32 "Permalink to this definition")

Methods[¶](#module-mss.base "Permalink to this headline")
---------------------------------------------------------

`mss.base.``lock`[¶](#mss.base.lock "Permalink to this definition")

New in version 6.0.0.

_class_ `mss.base.``MSSBase`[¶](#mss.base.MSSBase "Permalink to this definition")

The parent’s class for every OS implementation.

`cls_image`[¶](#mss.base.MSSBase.cls_image "Permalink to this definition")

`compression_level`[¶](#mss.base.MSSBase.compression_level "Permalink to this definition")

PNG compression level used when saving the screenshot data into a file (see [`zlib.compress()`](https://docs.python.org/3/library/zlib.html#zlib.compress "(in Python v3.11)") for details).

New in version 3.2.0.

`with_cursor`[¶](#mss.base.MSSBase.with_cursor "Permalink to this definition")

Include the mouse cursor in screenshots.

New in version 8.0.0.

`__init__`(_compression\_level=6_, _display=None_, _max\_displays=32_, _with\_cursor=False_)[¶](#mss.base.MSSBase.__init__ "Permalink to this definition")



Parameters:

*   **compression\_level** ([_int_](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")) – PNG compression level.
*   **display** ([_bytes_](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.11)")_,_ [_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)") _or_ [_None_](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")) – The display to use. Only effective on GNU/Linux.
*   **max\_displays** ([_int_](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")) – Maximum number of displays. Only effective on macOS.
*   **with\_cursor** ([_bool_](https://docs.python.org/3/library/functions.html#bool "(in Python v3.11)")) – Include the mouse cursor in screenshots.

New in version 8.0.0: `compression_level`, `display`, `max_displays`, and `with_cursor`, keyword arguments.

`close`()[¶](#mss.base.MSSBase.close "Permalink to this definition")

Clean-up method.

New in version 4.0.0.

`grab`(_region_)[¶](#mss.base.MSSBase.grab "Permalink to this definition")



Parameters:

**monitor** ([_dict_](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.11)")) – region’s coordinates.

Return type:

[`ScreenShot`](#mss.base.ScreenShot "mss.base.ScreenShot")

Retrieve screen pixels for a given _region_. Subclasses need to implement this.

Note

_monitor_ can be a `tuple` like `PIL.Image.grab()` accepts, it will be converted to the appropriate `dict`.

`save`(\[_mon=1_\]\[, _output='mon-{mon}.png'_\]\[, _callback=None_\])[¶](#mss.base.MSSBase.save "Permalink to this definition")



Parameters:

*   **mon** ([_int_](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")) – the monitor’s number.
*   **output** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – the output’s file name.
*   **callback** (_callable_ _or_ [_None_](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")) – callback called before saving the screen shot to a file. Takes the _output_ argument as parameter.

Return type:

iterable

Returns:

Created file(s).

Grab a screen shot and save it to a file. The _output_ parameter can take several keywords to customize the filename:

> *   `{mon}`: the monitor number
> *   `{top}`: the screen shot y-coordinate of the upper-left corner
> *   `{left}`: the screen shot x-coordinate of the upper-left corner
> *   `{width}`: the screen shot’s width
> *   `{height}`: the screen shot’s height
> *   `{date}`: the current date using the default formatter

As it is using the [`format()`](https://docs.python.org/3/library/functions.html#format "(in Python v3.11)") function, you can specify formatting options like `{date:%Y-%m-%s}`.

Warning

On Windows, the default date format may result with a filename containing ‘:’ which is not allowed:

IOerror: \[Errno 22\] invalid mode ('wb') or filename: 'sct\_1-2019-01-01 21:20:43.114194.png'

To fix this, you must provide a custom date formatting.

`shot`()[¶](#mss.base.MSSBase.shot "Permalink to this definition")



Return str:

The created file.

Helper to save the screen shot of the first monitor, by default. You can pass the same arguments as for [`save()`](#mss.base.MSSBase.save "mss.base.MSSBase.save").

New in version 3.0.0.

_class_ `mss.base.``ScreenShot`[¶](#mss.base.ScreenShot "Permalink to this definition")

Screen shot object.

Note

A better name would have been _Image_, but to prevent collisions with `PIL.Image`, it has been decided to use _ScreenShot_.

_classmethod_ `from_size`(_cls_, _data_, _width_, _height_)[¶](#mss.base.ScreenShot.from_size "Permalink to this definition")



Parameters:

*   **data** ([_bytearray_](https://docs.python.org/3/library/stdtypes.html#bytearray "(in Python v3.11)")) – raw BGRA pixels retrieved by ctypes OS independent implementations.
*   **width** ([_int_](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")) – the monitor’s width.
*   **height** ([_int_](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")) – the monitor’s height.

Return type:

[`ScreenShot`](#mss.base.ScreenShot "mss.base.ScreenShot")

Instantiate a new class given only screen shot’s data and size.

`pixel`(_coord\_x_, _coord\_y_)[¶](#mss.base.ScreenShot.pixel "Permalink to this definition")



Parameters:

*   **coord\_x** ([_int_](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")) – The x coordinate.
*   **coord\_y** ([_int_](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")) – The y coordinate.

Return type:

[tuple](https://docs.python.org/3/library/stdtypes.html#tuple "(in Python v3.11)")([int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)"), [int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)"), [int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)"))

Get the pixel value at the given position.

New in version 3.0.0.

`mss.tools.``to_png`(_data_, _size_, _level=6_, _output=None_)[¶](#mss.tools.to_png "Permalink to this definition")



Parameters:

*   **data** ([_bytes_](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.11)")) – RGBRGB…RGB data.
*   **size** ([_tuple_](https://docs.python.org/3/library/stdtypes.html#tuple "(in Python v3.11)")) – The (width, height) pair.
*   **level** ([_int_](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")) – PNG compression level.
*   **output** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – output’s file name.

Raises:

*   [**ScreenShotError**](#mss.exception.ScreenShotError "mss.exception.ScreenShotError") – On error when writing _data_ to _output_.
*   [**zlib.error**](https://docs.python.org/3/library/zlib.html#zlib.error "(in Python v3.11)") – On bad compression _level_.

Dump data to the image file. Pure Python PNG implementation. If _output_ is `None`, create no file but return the whole PNG data.

New in version 3.0.0.

Changed in version 3.2.0: The _level_ keyword argument to control the PNG compression level.

Properties[¶](#properties "Permalink to this headline")
-------------------------------------------------------

_class_ `mss.base.``MSSBase`[¶](#mss.tools.mss.base.MSSBase "Permalink to this definition")

`monitors`[¶](#mss.tools.mss.base.MSSBase.monitors "Permalink to this definition")

Positions of all monitors. If the monitor has rotation, you have to deal with it inside this method.

This method has to fill `self._monitors` with all information and use it as a cache:

*   `self._monitors[0]` is a dict of all monitors together
*   `self._monitors[N]` is a dict of the monitor N (with N > 0)

Each monitor is a dict with:

*   `left`: the x-coordinate of the upper-left corner
*   `top`: the y-coordinate of the upper-left corner
*   `width`: the width
*   `height`: the height

Subclasses need to implement this.



Return type:

[list](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.11)")\[[dict](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.11)")\[[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)"), [int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")\]\]

_class_ `mss.base.``ScreenShot`[¶](#mss.tools.mss.base.ScreenShot "Permalink to this definition")

`__array_interface__`[¶](#mss.tools.mss.base.ScreenShot.__array_interface__ "Permalink to this definition")

Numpy array interface support. It uses raw data in BGRA form.



Return type:

[dict](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.11)")\[[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)"), Any\]

`bgra`[¶](#mss.tools.mss.base.ScreenShot.bgra "Permalink to this definition")

BGRA values from the BGRA raw pixels.



Return type:

[bytes](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.11)")

New in version 3.2.0.

`height`[¶](#mss.tools.mss.base.ScreenShot.height "Permalink to this definition")

The screen shot’s height.



Return type:

[int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")

`left`[¶](#mss.tools.mss.base.ScreenShot.left "Permalink to this definition")

The screen shot’s left coordinate.



Return type:

[int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")

`pixels`[¶](#mss.tools.mss.base.ScreenShot.pixels "Permalink to this definition")

List of RGB tuples.



Return type:

[list](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.11)")\[[tuple](https://docs.python.org/3/library/stdtypes.html#tuple "(in Python v3.11)")([int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)"), [int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)"), [int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)"))\]

`pos`[¶](#mss.tools.mss.base.ScreenShot.pos "Permalink to this definition")

The screen shot’s coordinates.



Return type:

[`collections.namedtuple()`](https://docs.python.org/3/library/collections.html#collections.namedtuple "(in Python v3.11)")

`rgb`[¶](#mss.tools.mss.base.ScreenShot.rgb "Permalink to this definition")

Computed RGB values from the BGRA raw pixels.



Return type:

[bytes](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.11)")

New in version 3.0.0.

`size`[¶](#mss.tools.mss.base.ScreenShot.size "Permalink to this definition")

The screen shot’s size.



Return type:

[`collections.namedtuple()`](https://docs.python.org/3/library/collections.html#collections.namedtuple "(in Python v3.11)")

`top`[¶](#mss.tools.mss.base.ScreenShot.top "Permalink to this definition")

The screen shot’s top coordinate.



Return type:

[int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")

`width`[¶](#mss.tools.mss.base.ScreenShot.width "Permalink to this definition")

The screen shot’s width.



Return type:

[int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")

Exception[¶](#module-mss.exception "Permalink to this headline")
----------------------------------------------------------------

_exception_ `mss.exception.``ScreenShotError`[¶](#mss.exception.ScreenShotError "Permalink to this definition")

Base class for MSS exceptions.

`details`[¶](#mss.exception.ScreenShotError.details "Permalink to this definition")

On GNU/Linux, and if the error comes from the XServer, it contains XError details. This is an empty dict by default.

For XErrors, you can find information on [Using the Default Error Handlers](https://tronche.com/gui/x/xlib/event-handling/protocol-errors/default-handlers.html).



Return type:

[dict](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.11)")\[[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)"), Any\]

New in version 3.3.0.

Factory[¶](#module-mss.factory "Permalink to this headline")
------------------------------------------------------------

`mss.factory.``mss`()[¶](#mss.factory.mss "Permalink to this definition")

Factory function to instance the appropriate MSS class.

[Next](developers.html "Developers") [Previous](support.html "Support")

* * *

© Copyright 2013-2023, Mickaël 'Tiger-222' Schoentgen & contributors Revision `a8635053`.

Built with [Sphinx](http://sphinx-doc.org/) using a [theme](https://github.com/rtfd/sphinx_rtd_theme) provided by [Read the Docs](https://readthedocs.org).
