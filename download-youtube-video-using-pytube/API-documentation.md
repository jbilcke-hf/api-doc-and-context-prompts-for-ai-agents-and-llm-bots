*   [Docs](index.html) »
*   API
*   [Edit on GitHub](https://github.com/nficano/pytube/blob/master/docs/api.rst)

* * *

API[¶](#api "Permalink to this headline")
=========================================

YouTube Object[¶](#youtube-object "Permalink to this headline")
---------------------------------------------------------------

_class_ `pytube.``YouTube`(_url: str, on\_progress\_callback: Optional\[Callable\[\[Any, bytes, int\], None\]\] = None, on\_complete\_callback: Optional\[Callable\[\[Any, Optional\[str\]\], None\]\] = None, proxies: Dict\[str, str\] = None, use\_oauth: bool = False, allow\_oauth\_cache: bool = True_)[\[source\]](_modules/pytube/__main__.html#YouTube)[¶](#pytube.YouTube "Permalink to this definition")

Core developer interface for pytube.

`author`[¶](#pytube.YouTube.author "Permalink to this definition")

Get the video author. :rtype: str

`bypass_age_gate`()[\[source\]](_modules/pytube/__main__.html#YouTube.bypass_age_gate)[¶](#pytube.YouTube.bypass_age_gate "Permalink to this definition")

Attempt to update the vid\_info by bypassing the age gate.

`caption_tracks`[¶](#pytube.YouTube.caption_tracks "Permalink to this definition")

Get a list of [`Caption`](#pytube.Caption "pytube.Caption").

 

Return type:

List\[[Caption](#pytube.Caption "pytube.Caption")\]

`captions`[¶](#pytube.YouTube.captions "Permalink to this definition")

Interface to query caption tracks.

 

Return type:

`CaptionQuery`.

`channel_id`[¶](#pytube.YouTube.channel_id "Permalink to this definition")

Get the video poster’s channel id.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`channel_url`[¶](#pytube.YouTube.channel_url "Permalink to this definition")

Construct the channel url for the video’s poster from the channel id.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`check_availability`()[\[source\]](_modules/pytube/__main__.html#YouTube.check_availability)[¶](#pytube.YouTube.check_availability "Permalink to this definition")

Check whether the video is available.

Raises different exceptions based on why the video is unavailable, otherwise does nothing.

`description`[¶](#pytube.YouTube.description "Permalink to this definition")

Get the video description.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`fmt_streams`[¶](#pytube.YouTube.fmt_streams "Permalink to this definition")

Returns a list of streams if they have been initialized.

If the streams have not been initialized, finds all relevant streams and initializes them.

_static_ `from_id`(_video\_id: str_) → pytube.\_\_main\_\_.YouTube[\[source\]](_modules/pytube/__main__.html#YouTube.from_id)[¶](#pytube.YouTube.from_id "Permalink to this definition")

Construct a [`YouTube`](#pytube.YouTube "pytube.YouTube") object from a video id.

 

Parameters:

**video\_id** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The video id of the YouTube video.

Return type:

[`YouTube`](#pytube.YouTube "pytube.YouTube")

`keywords`[¶](#pytube.YouTube.keywords "Permalink to this definition")

Get the video keywords.

 

Return type:

List\[[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")\]

`length`[¶](#pytube.YouTube.length "Permalink to this definition")

Get the video length in seconds.

 

Return type:

[int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")

`metadata`[¶](#pytube.YouTube.metadata "Permalink to this definition")

Get the metadata for the video.

 

Return type:

YouTubeMetadata

`publish_date`[¶](#pytube.YouTube.publish_date "Permalink to this definition")

Get the publish date.

 

Return type:

datetime

`rating`[¶](#pytube.YouTube.rating "Permalink to this definition")

Get the video average rating.

 

Return type:

[float](https://docs.python.org/3/library/functions.html#float "(in Python v3.11)")

`register_on_complete_callback`(_func: Callable\[\[Any, Optional\[str\]\], None\]_)[\[source\]](_modules/pytube/__main__.html#YouTube.register_on_complete_callback)[¶](#pytube.YouTube.register_on_complete_callback "Permalink to this definition")

Register a download complete callback function post initialization.

 

Parameters:

**func** (_callable_) – A callback function that takes `stream` and `file_path`.

Return type:

[None](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")

`register_on_progress_callback`(_func: Callable\[\[Any, bytes, int\], None\]_)[\[source\]](_modules/pytube/__main__.html#YouTube.register_on_progress_callback)[¶](#pytube.YouTube.register_on_progress_callback "Permalink to this definition")

Register a download progress callback function post initialization.

 

Parameters:

**func** (_callable_) –

A callback function that takes `stream`, `chunk`,

and `bytes_remaining` as parameters.

Return type:

[None](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")

`streaming_data`[¶](#pytube.YouTube.streaming_data "Permalink to this definition")

Return streamingData from video info.

`streams`[¶](#pytube.YouTube.streams "Permalink to this definition")

Interface to query both adaptive (DASH) and progressive streams.

 

Return type:

`StreamQuery`.

`thumbnail_url`[¶](#pytube.YouTube.thumbnail_url "Permalink to this definition")

Get the thumbnail url image.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`title`[¶](#pytube.YouTube.title "Permalink to this definition")

Get the video title.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`vid_info`[¶](#pytube.YouTube.vid_info "Permalink to this definition")

Parse the raw vid info and return the parsed result.

 

Return type:

Dict\[Any, Any\]

`views`[¶](#pytube.YouTube.views "Permalink to this definition")

Get the number of the times the video has been viewed.

 

Return type:

[int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")

Playlist Object[¶](#playlist-object "Permalink to this headline")
-----------------------------------------------------------------

_class_ `pytube.contrib.playlist.``Playlist`(_url: str_, _proxies: Optional\[Dict\[str_, _str\]\] = None_)[\[source\]](_modules/pytube/contrib/playlist.html#Playlist)[¶](#pytube.contrib.playlist.Playlist "Permalink to this definition")

Load a YouTube playlist with URL

`count`(_value_) → integer -- return number of occurrences of value[¶](#pytube.contrib.playlist.Playlist.count "Permalink to this definition")

`html`[¶](#pytube.contrib.playlist.Playlist.html "Permalink to this definition")

Get the playlist page html.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`index`(_value_\[, _start_\[, _stop_\]\]) → integer -- return first index of value.[¶](#pytube.contrib.playlist.Playlist.index "Permalink to this definition")

Raises ValueError if the value is not present.

Supporting start and stop arguments is optional, but recommended.

`initial_data`[¶](#pytube.contrib.playlist.Playlist.initial_data "Permalink to this definition")

Extract the initial data from the playlist page html.

 

Return type:

[dict](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.11)")

`last_updated`[¶](#pytube.contrib.playlist.Playlist.last_updated "Permalink to this definition")

Extract the date that the playlist was last updated.

For some playlists, this will be a specific date, which is returned as a datetime object. For other playlists, this is an estimate such as “1 week ago”. Due to the fact that this value is returned as a string, pytube does a best-effort parsing where possible, and returns the raw string where it is not possible.

 

Returns:

Date of last playlist update where possible, else the string provided

Return type:

[datetime.date](https://docs.python.org/3/library/datetime.html#datetime.date "(in Python v3.11)")

`length`[¶](#pytube.contrib.playlist.Playlist.length "Permalink to this definition")

Extract the number of videos in the playlist.

 

Returns:

Playlist video count

Return type:

[int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")

`owner`[¶](#pytube.contrib.playlist.Playlist.owner "Permalink to this definition")

Extract the owner of the playlist.

 

Returns:

Playlist owner name.

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`owner_id`[¶](#pytube.contrib.playlist.Playlist.owner_id "Permalink to this definition")

Extract the channel\_id of the owner of the playlist.

 

Returns:

Playlist owner’s channel ID.

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`owner_url`[¶](#pytube.contrib.playlist.Playlist.owner_url "Permalink to this definition")

Create the channel url of the owner of the playlist.

 

Returns:

Playlist owner’s channel url.

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`playlist_id`[¶](#pytube.contrib.playlist.Playlist.playlist_id "Permalink to this definition")

Get the playlist id.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`playlist_url`[¶](#pytube.contrib.playlist.Playlist.playlist_url "Permalink to this definition")

Get the base playlist url.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`sidebar_info`[¶](#pytube.contrib.playlist.Playlist.sidebar_info "Permalink to this definition")

Extract the sidebar info from the playlist page html.

 

Return type:

[dict](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.11)")

`title`[¶](#pytube.contrib.playlist.Playlist.title "Permalink to this definition")

Extract playlist title

 

Returns:

playlist title (name)

Return type:

Optional\[[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")\]

`trimmed`(_video\_id: str_) → Iterable\[str\][\[source\]](_modules/pytube/contrib/playlist.html#Playlist.trimmed)[¶](#pytube.contrib.playlist.Playlist.trimmed "Permalink to this definition")

Retrieve a list of YouTube video URLs trimmed at the given video ID

i.e. if the playlist has video IDs 1,2,3,4 calling trimmed(3) returns \[1,2\] :type video\_id: str

> video ID to trim the returned list of playlist URLs at

 

Return type:

List\[[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")\]

Returns:

List of video URLs from the playlist trimmed at the given ID

`url_generator`()[\[source\]](_modules/pytube/contrib/playlist.html#Playlist.url_generator)[¶](#pytube.contrib.playlist.Playlist.url_generator "Permalink to this definition")

Generator that yields video URLs.

 

Yields:

Video URLs

`video_urls`[¶](#pytube.contrib.playlist.Playlist.video_urls "Permalink to this definition")

Complete links of all the videos in playlist

 

Return type:

List\[[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")\]

Returns:

List of video URLs

`videos`[¶](#pytube.contrib.playlist.Playlist.videos "Permalink to this definition")

Yields YouTube objects of videos in this playlist

 

Return type:

List\[[YouTube](#pytube.YouTube "pytube.YouTube")\]

Returns:

List of YouTube

`views`[¶](#pytube.contrib.playlist.Playlist.views "Permalink to this definition")

Extract view count for playlist.

 

Returns:

Playlist view count

Return type:

[int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")

`yt_api_key`[¶](#pytube.contrib.playlist.Playlist.yt_api_key "Permalink to this definition")

Extract the INNERTUBE\_API\_KEY from the playlist ytcfg.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`ytcfg`[¶](#pytube.contrib.playlist.Playlist.ytcfg "Permalink to this definition")

Extract the ytcfg from the playlist page html.

 

Return type:

[dict](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.11)")

Channel Object[¶](#channel-object "Permalink to this headline")
---------------------------------------------------------------

_class_ `pytube.contrib.channel.``Channel`(_url: str_, _proxies: Optional\[Dict\[str_, _str\]\] = None_)[\[source\]](_modules/pytube/contrib/channel.html#Channel)[¶](#pytube.contrib.channel.Channel "Permalink to this definition")

`about_html`[¶](#pytube.contrib.channel.Channel.about_html "Permalink to this definition")

Get the html for the /about page.

Currently unused for any functionality.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`channel_id`[¶](#pytube.contrib.channel.Channel.channel_id "Permalink to this definition")

Get the ID of the YouTube channel.

This will return the underlying ID, not the vanity URL.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`channel_name`[¶](#pytube.contrib.channel.Channel.channel_name "Permalink to this definition")

Get the name of the YouTube channel.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`community_html`[¶](#pytube.contrib.channel.Channel.community_html "Permalink to this definition")

Get the html for the /community page.

Currently unused for any functionality.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`count`(_value_) → integer -- return number of occurrences of value[¶](#pytube.contrib.channel.Channel.count "Permalink to this definition")

`featured_channels_html`[¶](#pytube.contrib.channel.Channel.featured_channels_html "Permalink to this definition")

Get the html for the /channels page.

Currently unused for any functionality.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`html`[¶](#pytube.contrib.channel.Channel.html "Permalink to this definition")

Get the html for the /videos page.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`index`(_value_\[, _start_\[, _stop_\]\]) → integer -- return first index of value.[¶](#pytube.contrib.channel.Channel.index "Permalink to this definition")

Raises ValueError if the value is not present.

Supporting start and stop arguments is optional, but recommended.

`initial_data`[¶](#pytube.contrib.channel.Channel.initial_data "Permalink to this definition")

Extract the initial data from the playlist page html.

 

Return type:

[dict](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.11)")

`last_updated`[¶](#pytube.contrib.channel.Channel.last_updated "Permalink to this definition")

Extract the date that the playlist was last updated.

For some playlists, this will be a specific date, which is returned as a datetime object. For other playlists, this is an estimate such as “1 week ago”. Due to the fact that this value is returned as a string, pytube does a best-effort parsing where possible, and returns the raw string where it is not possible.

 

Returns:

Date of last playlist update where possible, else the string provided

Return type:

[datetime.date](https://docs.python.org/3/library/datetime.html#datetime.date "(in Python v3.11)")

`length`[¶](#pytube.contrib.channel.Channel.length "Permalink to this definition")

Extract the number of videos in the playlist.

 

Returns:

Playlist video count

Return type:

[int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")

`owner`[¶](#pytube.contrib.channel.Channel.owner "Permalink to this definition")

Extract the owner of the playlist.

 

Returns:

Playlist owner name.

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`owner_id`[¶](#pytube.contrib.channel.Channel.owner_id "Permalink to this definition")

Extract the channel\_id of the owner of the playlist.

 

Returns:

Playlist owner’s channel ID.

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`owner_url`[¶](#pytube.contrib.channel.Channel.owner_url "Permalink to this definition")

Create the channel url of the owner of the playlist.

 

Returns:

Playlist owner’s channel url.

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`playlist_id`[¶](#pytube.contrib.channel.Channel.playlist_id "Permalink to this definition")

Get the playlist id.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`playlist_url`[¶](#pytube.contrib.channel.Channel.playlist_url "Permalink to this definition")

Get the base playlist url.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`playlists_html`[¶](#pytube.contrib.channel.Channel.playlists_html "Permalink to this definition")

Get the html for the /playlists page.

Currently unused for any functionality.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`sidebar_info`[¶](#pytube.contrib.channel.Channel.sidebar_info "Permalink to this definition")

Extract the sidebar info from the playlist page html.

 

Return type:

[dict](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.11)")

`title`[¶](#pytube.contrib.channel.Channel.title "Permalink to this definition")

Extract playlist title

 

Returns:

playlist title (name)

Return type:

Optional\[[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")\]

`trimmed`(_video\_id: str_) → Iterable\[str\][¶](#pytube.contrib.channel.Channel.trimmed "Permalink to this definition")

Retrieve a list of YouTube video URLs trimmed at the given video ID

i.e. if the playlist has video IDs 1,2,3,4 calling trimmed(3) returns \[1,2\] :type video\_id: str

> video ID to trim the returned list of playlist URLs at

 

Return type:

List\[[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")\]

Returns:

List of video URLs from the playlist trimmed at the given ID

`url_generator`()[¶](#pytube.contrib.channel.Channel.url_generator "Permalink to this definition")

Generator that yields video URLs.

 

Yields:

Video URLs

`vanity_url`[¶](#pytube.contrib.channel.Channel.vanity_url "Permalink to this definition")

Get the vanity URL of the YouTube channel.

Returns None if it doesn’t exist.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`video_urls`[¶](#pytube.contrib.channel.Channel.video_urls "Permalink to this definition")

Complete links of all the videos in playlist

 

Return type:

List\[[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")\]

Returns:

List of video URLs

`videos`[¶](#pytube.contrib.channel.Channel.videos "Permalink to this definition")

Yields YouTube objects of videos in this playlist

 

Return type:

List\[[YouTube](#pytube.YouTube "pytube.YouTube")\]

Returns:

List of YouTube

`views`[¶](#pytube.contrib.channel.Channel.views "Permalink to this definition")

Extract view count for playlist.

 

Returns:

Playlist view count

Return type:

[int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")

`yt_api_key`[¶](#pytube.contrib.channel.Channel.yt_api_key "Permalink to this definition")

Extract the INNERTUBE\_API\_KEY from the playlist ytcfg.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`ytcfg`[¶](#pytube.contrib.channel.Channel.ytcfg "Permalink to this definition")

Extract the ytcfg from the playlist page html.

 

Return type:

[dict](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.11)")

Stream Object[¶](#stream-object "Permalink to this headline")
-------------------------------------------------------------

_class_ `pytube.``Stream`(_stream: Dict\[KT, VT\], monostate: pytube.monostate.Monostate_)[\[source\]](_modules/pytube/streams.html#Stream)[¶](#pytube.Stream "Permalink to this definition")

Container for stream manifest data.

`default_filename`[¶](#pytube.Stream.default_filename "Permalink to this definition")

Generate filename based on the video title.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

Returns:

An os file system compatible filename.

`download`(_output\_path: Optional\[str\] = None_, _filename: Optional\[str\] = None_, _filename\_prefix: Optional\[str\] = None_, _skip\_existing: bool = True_, _timeout: Optional\[int\] = None_, _max\_retries: Optional\[int\] = 0_) → str[\[source\]](_modules/pytube/streams.html#Stream.download)[¶](#pytube.Stream.download "Permalink to this definition")

Write the media stream to disk.

 

Parameters:

*   **output\_path** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)") _or_ [_None_](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")) – (optional) Output path for writing media file. If one is not specified, defaults to the current working directory.
*   **filename** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)") _or_ [_None_](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")) – (optional) Output filename (stem only) for writing media file. If one is not specified, the default filename is used.
*   **filename\_prefix** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)") _or_ [_None_](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")) – (optional) A string that will be prepended to the filename. For example a number in a playlist or the name of a series. If one is not specified, nothing will be prepended This is separate from filename so you can use the default filename but still add a prefix.
*   **skip\_existing** ([_bool_](https://docs.python.org/3/library/functions.html#bool "(in Python v3.11)")) – (optional) Skip existing files, defaults to True
*   **timeout** ([_int_](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")) – (optional) Request timeout length in seconds. Uses system default.
*   **max\_retries** ([_int_](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")) – (optional) Number of retries to attempt after socket timeout. Defaults to 0.

Returns:

Path to the saved video

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

`filesize`[¶](#pytube.Stream.filesize "Permalink to this definition")

File size of the media stream in bytes.

 

Return type:

[int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")

Returns:

Filesize (in bytes) of the stream.

`filesize_approx`[¶](#pytube.Stream.filesize_approx "Permalink to this definition")

Get approximate filesize of the video

Falls back to HTTP call if there is not sufficient information to approximate

 

Return type:

[int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")

Returns:

size of video in bytes

`filesize_gb`[¶](#pytube.Stream.filesize_gb "Permalink to this definition")

File size of the media stream in gigabytes.

 

Return type:

[float](https://docs.python.org/3/library/functions.html#float "(in Python v3.11)")

Returns:

Rounded filesize (in gigabytes) of the stream.

`filesize_kb`[¶](#pytube.Stream.filesize_kb "Permalink to this definition")

File size of the media stream in kilobytes.

 

Return type:

[float](https://docs.python.org/3/library/functions.html#float "(in Python v3.11)")

Returns:

Rounded filesize (in kilobytes) of the stream.

`filesize_mb`[¶](#pytube.Stream.filesize_mb "Permalink to this definition")

File size of the media stream in megabytes.

 

Return type:

[float](https://docs.python.org/3/library/functions.html#float "(in Python v3.11)")

Returns:

Rounded filesize (in megabytes) of the stream.

`includes_audio_track`[¶](#pytube.Stream.includes_audio_track "Permalink to this definition")

Whether the stream only contains audio.

 

Return type:

[bool](https://docs.python.org/3/library/functions.html#bool "(in Python v3.11)")

`includes_video_track`[¶](#pytube.Stream.includes_video_track "Permalink to this definition")

Whether the stream only contains video.

 

Return type:

[bool](https://docs.python.org/3/library/functions.html#bool "(in Python v3.11)")

`is_adaptive`[¶](#pytube.Stream.is_adaptive "Permalink to this definition")

Whether the stream is DASH.

 

Return type:

[bool](https://docs.python.org/3/library/functions.html#bool "(in Python v3.11)")

`is_progressive`[¶](#pytube.Stream.is_progressive "Permalink to this definition")

Whether the stream is progressive.

 

Return type:

[bool](https://docs.python.org/3/library/functions.html#bool "(in Python v3.11)")

`on_complete`(_file\_path: Optional\[str\]_)[\[source\]](_modules/pytube/streams.html#Stream.on_complete)[¶](#pytube.Stream.on_complete "Permalink to this definition")

On download complete handler function.

 

Parameters:

**file\_path** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The file handle where the media is being written to.

Return type:

[None](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")

`on_progress`(_chunk: bytes_, _file\_handler: BinaryIO_, _bytes\_remaining: int_)[\[source\]](_modules/pytube/streams.html#Stream.on_progress)[¶](#pytube.Stream.on_progress "Permalink to this definition")

On progress callback function.

This function writes the binary data to the file, then checks if an additional callback is defined in the monostate. This is exposed to allow things like displaying a progress bar.

 

Parameters:

*   **chunk** ([_bytes_](https://docs.python.org/3/library/stdtypes.html#bytes "(in Python v3.11)")) – Segment of media file binary data, not yet written to disk.
*   **file\_handler** ([`io.BufferedWriter`](https://docs.python.org/3/library/io.html#io.BufferedWriter "(in Python v3.11)")) – The file handle where the media is being written to.
*   **bytes\_remaining** ([_int_](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")) – The delta between the total file size in bytes and amount already downloaded.

Return type:

[None](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")

`parse_codecs`() → Tuple\[Optional\[str\], Optional\[str\]\][\[source\]](_modules/pytube/streams.html#Stream.parse_codecs)[¶](#pytube.Stream.parse_codecs "Permalink to this definition")

Get the video/audio codecs from list of codecs.

Parse a variable length sized list of codecs and returns a constant two element tuple, with the video codec as the first element and audio as the second. Returns None if one is not available (adaptive only).

 

Return type:

[tuple](https://docs.python.org/3/library/stdtypes.html#tuple "(in Python v3.11)")

Returns:

A two element tuple with audio and video codecs.

`stream_to_buffer`(_buffer: BinaryIO_) → None[\[source\]](_modules/pytube/streams.html#Stream.stream_to_buffer)[¶](#pytube.Stream.stream_to_buffer "Permalink to this definition")

Write the media stream to buffer

 

Return type:

io.BytesIO buffer

`title`[¶](#pytube.Stream.title "Permalink to this definition")

Get title of video

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

Returns:

Youtube video title

StreamQuery Object[¶](#streamquery-object "Permalink to this headline")
-----------------------------------------------------------------------

_class_ `pytube.query.``StreamQuery`(_fmt\_streams_)[\[source\]](_modules/pytube/query.html#StreamQuery)[¶](#pytube.query.StreamQuery "Permalink to this definition")

Interface for querying the available media streams.

`all`() → List\[pytube.streams.Stream\][\[source\]](_modules/pytube/query.html#StreamQuery.all)[¶](#pytube.query.StreamQuery.all "Permalink to this definition")

Get all the results represented by this query as a list.

 

Return type:

[list](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.11)")

`asc`() → pytube.query.StreamQuery[\[source\]](_modules/pytube/query.html#StreamQuery.asc)[¶](#pytube.query.StreamQuery.asc "Permalink to this definition")

Sort streams in ascending order.

 

Return type:

[`StreamQuery`](#pytube.query.StreamQuery "pytube.query.StreamQuery")

`count`(_value: Optional\[str\] = None_) → int[\[source\]](_modules/pytube/query.html#StreamQuery.count)[¶](#pytube.query.StreamQuery.count "Permalink to this definition")

Get the count of items in the list.

 

Return type:

[int](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")

`desc`() → pytube.query.StreamQuery[\[source\]](_modules/pytube/query.html#StreamQuery.desc)[¶](#pytube.query.StreamQuery.desc "Permalink to this definition")

Sort streams in descending order.

 

Return type:

[`StreamQuery`](#pytube.query.StreamQuery "pytube.query.StreamQuery")

`filter`(_fps=None_, _res=None_, _resolution=None_, _mime\_type=None_, _type=None_, _subtype=None_, _file\_extension=None_, _abr=None_, _bitrate=None_, _video\_codec=None_, _audio\_codec=None_, _only\_audio=None_, _only\_video=None_, _progressive=None_, _adaptive=None_, _is\_dash=None_, _custom\_filter\_functions=None_)[\[source\]](_modules/pytube/query.html#StreamQuery.filter)[¶](#pytube.query.StreamQuery.filter "Permalink to this definition")

Apply the given filtering criterion.

 

Parameters:

*   **fps** ([_int_](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)") _or_ [_None_](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")) – (optional) The frames per second.
*   **resolution** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)") _or_ [_None_](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")) – (optional) Alias to `res`.
*   **res** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)") _or_ [_None_](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")) – (optional) The video resolution.
*   **mime\_type** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)") _or_ [_None_](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")) – (optional) Two-part identifier for file formats and format contents composed of a “type”, a “subtype”.
*   **type** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)") _or_ [_None_](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")) – (optional) Type part of the `mime_type` (e.g.: audio, video).
*   **subtype** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)") _or_ [_None_](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")) – (optional) Sub-type part of the `mime_type` (e.g.: mp4, mov).
*   **file\_extension** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)") _or_ [_None_](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")) – (optional) Alias to `sub_type`.
*   **abr** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)") _or_ [_None_](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")) – (optional) Average bitrate (ABR) refers to the average amount of data transferred per unit of time (e.g.: 64kbps, 192kbps).
*   **bitrate** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)") _or_ [_None_](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")) – (optional) Alias to `abr`.
*   **video\_codec** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)") _or_ [_None_](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")) – (optional) Video compression format.
*   **audio\_codec** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)") _or_ [_None_](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")) – (optional) Audio compression format.
*   **progressive** ([_bool_](https://docs.python.org/3/library/functions.html#bool "(in Python v3.11)")) – Excludes adaptive streams (one file contains both audio and video tracks).
*   **adaptive** ([_bool_](https://docs.python.org/3/library/functions.html#bool "(in Python v3.11)")) – Excludes progressive streams (audio and video are on separate tracks).
*   **is\_dash** ([_bool_](https://docs.python.org/3/library/functions.html#bool "(in Python v3.11)")) – Include/exclude dash streams.
*   **only\_audio** ([_bool_](https://docs.python.org/3/library/functions.html#bool "(in Python v3.11)")) – Excludes streams with video tracks.
*   **only\_video** ([_bool_](https://docs.python.org/3/library/functions.html#bool "(in Python v3.11)")) – Excludes streams with audio tracks.
*   **custom\_filter\_functions** ([_list_](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.11)") _or_ [_None_](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")) – (optional) Interface for defining complex filters without subclassing.

`first`() → Optional\[pytube.streams.Stream\][\[source\]](_modules/pytube/query.html#StreamQuery.first)[¶](#pytube.query.StreamQuery.first "Permalink to this definition")

Get the first `Stream` in the results.

 

Return type:

`Stream` or None

Returns:

the first result of this query or None if the result doesn’t contain any streams.

`get_audio_only`(_subtype: str = 'mp4'_) → Optional\[pytube.streams.Stream\][\[source\]](_modules/pytube/query.html#StreamQuery.get_audio_only)[¶](#pytube.query.StreamQuery.get_audio_only "Permalink to this definition")

Get highest bitrate audio stream for given codec (defaults to mp4)

 

Parameters:

**subtype** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – Audio subtype, defaults to mp4

Return type:

`Stream` or None

Returns:

The `Stream` matching the given itag or None if not found.

`get_by_itag`(_itag: int_) → Optional\[pytube.streams.Stream\][\[source\]](_modules/pytube/query.html#StreamQuery.get_by_itag)[¶](#pytube.query.StreamQuery.get_by_itag "Permalink to this definition")

Get the corresponding `Stream` for a given itag.

 

Parameters:

**itag** ([_int_](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")) – YouTube format identifier code.

Return type:

`Stream` or None

Returns:

The `Stream` matching the given itag or None if not found.

`get_by_resolution`(_resolution: str_) → Optional\[pytube.streams.Stream\][\[source\]](_modules/pytube/query.html#StreamQuery.get_by_resolution)[¶](#pytube.query.StreamQuery.get_by_resolution "Permalink to this definition")

Get the corresponding `Stream` for a given resolution.

Stream must be a progressive mp4.

 

Parameters:

**resolution** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – Video resolution i.e. “720p”, “480p”, “360p”, “240p”, “144p”

Return type:

`Stream` or None

Returns:

The `Stream` matching the given itag or None if not found.

`get_highest_resolution`() → Optional\[pytube.streams.Stream\][\[source\]](_modules/pytube/query.html#StreamQuery.get_highest_resolution)[¶](#pytube.query.StreamQuery.get_highest_resolution "Permalink to this definition")

Get highest resolution stream that is a progressive video.

 

Return type:

`Stream` or None

Returns:

The `Stream` matching the given itag or None if not found.

`get_lowest_resolution`() → Optional\[pytube.streams.Stream\][\[source\]](_modules/pytube/query.html#StreamQuery.get_lowest_resolution)[¶](#pytube.query.StreamQuery.get_lowest_resolution "Permalink to this definition")

Get lowest resolution stream that is a progressive mp4.

 

Return type:

`Stream` or None

Returns:

The `Stream` matching the given itag or None if not found.

`index`(_value_\[, _start_\[, _stop_\]\]) → integer -- return first index of value.[¶](#pytube.query.StreamQuery.index "Permalink to this definition")

Raises ValueError if the value is not present.

Supporting start and stop arguments is optional, but recommended.

`last`()[\[source\]](_modules/pytube/query.html#StreamQuery.last)[¶](#pytube.query.StreamQuery.last "Permalink to this definition")

Get the last `Stream` in the results.

 

Return type:

`Stream` or None

Returns:

Return the last result of this query or None if the result doesn’t contain any streams.

`order_by`(_attribute\_name: str_) → pytube.query.StreamQuery[\[source\]](_modules/pytube/query.html#StreamQuery.order_by)[¶](#pytube.query.StreamQuery.order_by "Permalink to this definition")

Apply a sort order. Filters out stream the do not have the attribute.

 

Parameters:

**attribute\_name** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The name of the attribute to sort by.

`otf`(_is\_otf: bool = False_) → pytube.query.StreamQuery[\[source\]](_modules/pytube/query.html#StreamQuery.otf)[¶](#pytube.query.StreamQuery.otf "Permalink to this definition")

Filter stream by OTF, useful if some streams have 404 URLs

 

Parameters:

**is\_otf** ([_bool_](https://docs.python.org/3/library/functions.html#bool "(in Python v3.11)")) – Set to False to retrieve only non-OTF streams

Return type:

[`StreamQuery`](#pytube.query.StreamQuery "pytube.query.StreamQuery")

Returns:

A StreamQuery object with otf filtered streams

Caption Object[¶](#caption-object "Permalink to this headline")
---------------------------------------------------------------

_class_ `pytube.``Caption`(_caption\_track: Dict\[KT, VT\]_)[\[source\]](_modules/pytube/captions.html#Caption)[¶](#pytube.Caption "Permalink to this definition")

Container for caption tracks.

`download`(_title: str_, _srt: bool = True_, _output\_path: Optional\[str\] = None_, _filename\_prefix: Optional\[str\] = None_) → str[\[source\]](_modules/pytube/captions.html#Caption.download)[¶](#pytube.Caption.download "Permalink to this definition")

Write the media stream to disk.

 

Parameters:

*   **title** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – Output filename (stem only) for writing media file. If one is not specified, the default filename is used.
*   **srt** – Set to True to download srt, false to download xml. Defaults to True.

:type srt bool :param output\_path:

> (optional) Output path for writing media file. If one is not specified, defaults to the current working directory.

 

Parameters:

**filename\_prefix** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)") _or_ [_None_](https://docs.python.org/3/library/constants.html#None "(in Python v3.11)")) – (optional) A string that will be prepended to the filename. For example a number in a playlist or the name of a series. If one is not specified, nothing will be prepended This is separate from filename so you can use the default filename but still add a prefix.

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

_static_ `float_to_srt_time_format`(_d: float_) → str[\[source\]](_modules/pytube/captions.html#Caption.float_to_srt_time_format)[¶](#pytube.Caption.float_to_srt_time_format "Permalink to this definition")

Convert decimal durations into proper srt format.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

Returns:

SubRip Subtitle (str) formatted time duration.

float\_to\_srt\_time\_format(3.89) -> ‘00:00:03,890’

`generate_srt_captions`() → str[\[source\]](_modules/pytube/captions.html#Caption.generate_srt_captions)[¶](#pytube.Caption.generate_srt_captions "Permalink to this definition")

Generate “SubRip Subtitle” captions.

Takes the xml captions from [`xml_captions()`](#pytube.Caption.xml_captions "pytube.Caption.xml_captions") and recompiles them into the “SubRip Subtitle” format.

`json_captions`[¶](#pytube.Caption.json_captions "Permalink to this definition")

Download and parse the json caption tracks.

`xml_caption_to_srt`(_xml\_captions: str_) → str[\[source\]](_modules/pytube/captions.html#Caption.xml_caption_to_srt)[¶](#pytube.Caption.xml_caption_to_srt "Permalink to this definition")

Convert xml caption tracks to “SubRip Subtitle (srt)”.

 

Parameters:

**xml\_captions** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – XML formatted caption tracks.

`xml_captions`[¶](#pytube.Caption.xml_captions "Permalink to this definition")

Download the xml caption tracks.

CaptionQuery Object[¶](#captionquery-object "Permalink to this headline")
-------------------------------------------------------------------------

_class_ `pytube.query.``CaptionQuery`(_captions: List\[pytube.captions.Caption\]_)[\[source\]](_modules/pytube/query.html#CaptionQuery)[¶](#pytube.query.CaptionQuery "Permalink to this definition")

Interface for querying the available captions.

`all`() → List\[pytube.captions.Caption\][\[source\]](_modules/pytube/query.html#CaptionQuery.all)[¶](#pytube.query.CaptionQuery.all "Permalink to this definition")

Get all the results represented by this query as a list.

 

Return type:

[list](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.11)")

`get`(_k_\[, _d_\]) → D\[k\] if k in D, else d. d defaults to None.[¶](#pytube.query.CaptionQuery.get "Permalink to this definition")

`get_by_language_code`(_lang\_code: str_) → Optional\[pytube.captions.Caption\][\[source\]](_modules/pytube/query.html#CaptionQuery.get_by_language_code)[¶](#pytube.query.CaptionQuery.get_by_language_code "Permalink to this definition")

Get the `Caption` for a given `lang_code`.

 

Parameters:

**lang\_code** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The code that identifies the caption language.

Return type:

`Caption` or None

Returns:

The `Caption` matching the given `lang_code` or None if it does not exist.

`items`() → a set-like object providing a view on D's items[¶](#pytube.query.CaptionQuery.items "Permalink to this definition")

`keys`() → a set-like object providing a view on D's keys[¶](#pytube.query.CaptionQuery.keys "Permalink to this definition")

`values`() → an object providing a view on D's values[¶](#pytube.query.CaptionQuery.values "Permalink to this definition")

Search Object[¶](#search-object "Permalink to this headline")
-------------------------------------------------------------

_class_ `pytube.contrib.search.``Search`(_query_)[\[source\]](_modules/pytube/contrib/search.html#Search)[¶](#pytube.contrib.search.Search "Permalink to this definition")

`completion_suggestions`[¶](#pytube.contrib.search.Search.completion_suggestions "Permalink to this definition")

Return query autocompletion suggestions for the query.

 

Return type:

[list](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.11)")

Returns:

A list of autocomplete suggestions provided by YouTube for the query.

`fetch_and_parse`(_continuation=None_)[\[source\]](_modules/pytube/contrib/search.html#Search.fetch_and_parse)[¶](#pytube.contrib.search.Search.fetch_and_parse "Permalink to this definition")

Fetch from the innertube API and parse the results.

 

Parameters:

**continuation** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – Continuation string for fetching results.

Return type:

[tuple](https://docs.python.org/3/library/stdtypes.html#tuple "(in Python v3.11)")

Returns:

A tuple of a list of YouTube objects and a continuation string.

`fetch_query`(_continuation=None_)[\[source\]](_modules/pytube/contrib/search.html#Search.fetch_query)[¶](#pytube.contrib.search.Search.fetch_query "Permalink to this definition")

Fetch raw results from the innertube API.

 

Parameters:

**continuation** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – Continuation string for fetching results.

Return type:

[dict](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.11)")

Returns:

The raw json object returned by the innertube API.

`get_next_results`()[\[source\]](_modules/pytube/contrib/search.html#Search.get_next_results)[¶](#pytube.contrib.search.Search.get_next_results "Permalink to this definition")

Use the stored continuation string to fetch the next set of results.

This method does not return the results, but instead updates the results property.

`results`[¶](#pytube.contrib.search.Search.results "Permalink to this definition")

Return search results.

On first call, will generate and return the first set of results. Additional results can be generated using `.get_next_results()`.

 

Return type:

[list](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.11)")

Returns:

A list of YouTube objects.

Extract[¶](#module-pytube.extract "Permalink to this headline")
---------------------------------------------------------------

This module contains all non-cipher related data extraction logic.

`pytube.extract.``apply_descrambler`(_stream\_data: Dict\[KT, VT\]_) → None[\[source\]](_modules/pytube/extract.html#apply_descrambler)[¶](#pytube.extract.apply_descrambler "Permalink to this definition")

Apply various in-place transforms to YouTube’s media stream data.

Creates a `list` of dictionaries by string splitting on commas, then taking each list item, parsing it as a query string, converting it to a `dict` and unquoting the value.

 

Parameters:

**stream\_data** ([_dict_](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.11)")) – Dictionary containing query string encoded values.

**Example**:

\>>> d \= {'foo': 'bar=1&var=test,em=5&t=url%20encoded'}
\>>> apply\_descrambler(d, 'foo')
\>>> print(d)
{'foo': \[{'bar': '1', 'var': 'test'}, {'em': '5', 't': 'url encoded'}\]}

`pytube.extract.``apply_signature`(_stream\_manifest: Dict\[KT, VT\], vid\_info: Dict\[KT, VT\], js: str_) → None[\[source\]](_modules/pytube/extract.html#apply_signature)[¶](#pytube.extract.apply_signature "Permalink to this definition")

Apply the decrypted signature to the stream manifest.

 

Parameters:

*   **stream\_manifest** ([_dict_](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.11)")) – Details of the media streams available.
*   **js** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The contents of the base.js asset file.

`pytube.extract.``channel_name`(_url: str_) → str[\[source\]](_modules/pytube/extract.html#channel_name)[¶](#pytube.extract.channel_name "Permalink to this definition")

Extract the `channel_name` or `channel_id` from a YouTube url.

This function supports the following patterns:

*   `https://youtube.com/c/_channel_name_/*`
*   :samp:[\`](#id2)[https://youtube.com/channel](https://youtube.com/channel)/{channel\_id}/\*
*   `https://youtube.com/u/_channel_name_/*`
*   :samp:[\`](#id4)[https://youtube.com/user](https://youtube.com/user)/{channel\_id}/\*

 

Parameters:

**url** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – A YouTube url containing a channel name.

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

Returns:

YouTube channel name.

`pytube.extract.``get_ytcfg`(_html: str_) → str[\[source\]](_modules/pytube/extract.html#get_ytcfg)[¶](#pytube.extract.get_ytcfg "Permalink to this definition")

Get the entirety of the ytcfg object.

This is built over multiple pieces, so we have to find all matches and combine the dicts together.

 

Parameters:

**html** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The html contents of the watch page.

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

Returns:

Substring of the html containing the encoded manifest data.

`pytube.extract.``get_ytplayer_config`(_html: str_) → Any[\[source\]](_modules/pytube/extract.html#get_ytplayer_config)[¶](#pytube.extract.get_ytplayer_config "Permalink to this definition")

Get the YouTube player configuration data from the watch html.

Extract the `ytplayer_config`, which is json data embedded within the watch html and serves as the primary source of obtaining the stream manifest data.

 

Parameters:

**html** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The html contents of the watch page.

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

Returns:

Substring of the html containing the encoded manifest data.

`pytube.extract.``get_ytplayer_js`(_html: str_) → Any[\[source\]](_modules/pytube/extract.html#get_ytplayer_js)[¶](#pytube.extract.get_ytplayer_js "Permalink to this definition")

Get the YouTube player base JavaScript path.

:param str html

The html contents of the watch page.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

Returns:

Path to YouTube’s base.js file.

`pytube.extract.``initial_data`(_watch\_html: str_) → str[\[source\]](_modules/pytube/extract.html#initial_data)[¶](#pytube.extract.initial_data "Permalink to this definition")

Extract the ytInitialData json from the watch\_html page.

This mostly contains metadata necessary for rendering the page on-load, such as video information, copyright notices, etc.

@param watch\_html: Html of the watch page @return:

`pytube.extract.``initial_player_response`(_watch\_html: str_) → str[\[source\]](_modules/pytube/extract.html#initial_player_response)[¶](#pytube.extract.initial_player_response "Permalink to this definition")

Extract the ytInitialPlayerResponse json from the watch\_html page.

This mostly contains metadata necessary for rendering the page on-load, such as video information, copyright notices, etc.

@param watch\_html: Html of the watch page @return:

`pytube.extract.``is_age_restricted`(_watch\_html: str_) → bool[\[source\]](_modules/pytube/extract.html#is_age_restricted)[¶](#pytube.extract.is_age_restricted "Permalink to this definition")

Check if content is age restricted.

 

Parameters:

**watch\_html** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The html contents of the watch page.

Return type:

[bool](https://docs.python.org/3/library/functions.html#bool "(in Python v3.11)")

Returns:

Whether or not the content is age restricted.

`pytube.extract.``is_private`(_watch\_html_)[\[source\]](_modules/pytube/extract.html#is_private)[¶](#pytube.extract.is_private "Permalink to this definition")

Check if content is private.

 

Parameters:

**watch\_html** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The html contents of the watch page.

Return type:

[bool](https://docs.python.org/3/library/functions.html#bool "(in Python v3.11)")

Returns:

Whether or not the content is private.

`pytube.extract.``js_url`(_html: str_) → str[\[source\]](_modules/pytube/extract.html#js_url)[¶](#pytube.extract.js_url "Permalink to this definition")

Get the base JavaScript url.

Construct the base JavaScript url, which contains the decipher “transforms”.

 

Parameters:

**html** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The html contents of the watch page.

`pytube.extract.``metadata`(_initial\_data_) → Optional\[pytube.metadata.YouTubeMetadata\][\[source\]](_modules/pytube/extract.html#metadata)[¶](#pytube.extract.metadata "Permalink to this definition")

Get the informational metadata for the video.

e.g.: \[

> {
> 
> ‘Song’: ‘강남스타일(Gangnam Style)’, ‘Artist’: ‘PSY’, ‘Album’: ‘PSY SIX RULES Pt.1’, ‘Licensed to YouTube by’: ‘YG Entertainment Inc. \[…\]’
> 
> }

\]

 

Return type:

YouTubeMetadata

`pytube.extract.``mime_type_codec`(_mime\_type\_codec: str_) → Tuple\[str, List\[str\]\][\[source\]](_modules/pytube/extract.html#mime_type_codec)[¶](#pytube.extract.mime_type_codec "Permalink to this definition")

Parse the type data.

Breaks up the data in the `type` key of the manifest, which contains the mime type and codecs serialized together, and splits them into separate elements.

**Example**:

mime\_type\_codec(‘audio/webm; codecs=”opus”’) -> (‘audio/webm’, \[‘opus’\])

 

Parameters:

**mime\_type\_codec** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – String containing mime type and codecs.

Return type:

[tuple](https://docs.python.org/3/library/stdtypes.html#tuple "(in Python v3.11)")

Returns:

The mime type and a list of codecs.

`pytube.extract.``playability_status`(_watch\_html: str) -> (<class 'str'>_, _<class 'str'>_)[\[source\]](_modules/pytube/extract.html#playability_status)[¶](#pytube.extract.playability_status "Permalink to this definition")

Return the playability status and status explanation of a video.

For example, a video may have a status of LOGIN\_REQUIRED, and an explanation of “This is a private video. Please sign in to verify that you may see it.”

This explanation is what gets incorporated into the media player overlay.

 

Parameters:

**watch\_html** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The html contents of the watch page.

Return type:

[bool](https://docs.python.org/3/library/functions.html#bool "(in Python v3.11)")

Returns:

Playability status and reason of the video.

`pytube.extract.``playlist_id`(_url: str_) → str[\[source\]](_modules/pytube/extract.html#playlist_id)[¶](#pytube.extract.playlist_id "Permalink to this definition")

Extract the `playlist_id` from a YouTube url.

This function supports the following patterns:

*   `https://youtube.com/playlist?list=_playlist_id_`
*   `https://youtube.com/watch?v=_video_id_&list=_playlist_id_`

 

Parameters:

**url** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – A YouTube url containing a playlist id.

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

Returns:

YouTube playlist id.

`pytube.extract.``publish_date`(_watch\_html: str_)[\[source\]](_modules/pytube/extract.html#publish_date)[¶](#pytube.extract.publish_date "Permalink to this definition")

Extract publish date :param str watch\_html:

> The html contents of the watch page.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

Returns:

Publish date of the video.

`pytube.extract.``recording_available`(_watch\_html_)[\[source\]](_modules/pytube/extract.html#recording_available)[¶](#pytube.extract.recording_available "Permalink to this definition")

Check if live stream recording is available.

 

Parameters:

**watch\_html** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The html contents of the watch page.

Return type:

[bool](https://docs.python.org/3/library/functions.html#bool "(in Python v3.11)")

Returns:

Whether or not the content is private.

`pytube.extract.``video_id`(_url: str_) → str[\[source\]](_modules/pytube/extract.html#video_id)[¶](#pytube.extract.video_id "Permalink to this definition")

Extract the `video_id` from a YouTube url.

This function supports the following patterns:

*   `https://youtube.com/watch?v=_video_id_`
*   `https://youtube.com/embed/_video_id_`
*   `https://youtu.be/_video_id_`

 

Parameters:

**url** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – A YouTube url containing a video id.

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

Returns:

YouTube video id.

`pytube.extract.``video_info_url`(_video\_id: str_, _watch\_url: str_) → str[\[source\]](_modules/pytube/extract.html#video_info_url)[¶](#pytube.extract.video_info_url "Permalink to this definition")

Construct the video\_info url.

 

Parameters:

*   **video\_id** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – A YouTube video identifier.
*   **watch\_url** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – A YouTube watch url.

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

Returns:

`https://youtube.com/get_video_info` with necessary GET parameters.

`pytube.extract.``video_info_url_age_restricted`(_video\_id: str_, _embed\_html: str_) → str[\[source\]](_modules/pytube/extract.html#video_info_url_age_restricted)[¶](#pytube.extract.video_info_url_age_restricted "Permalink to this definition")

Construct the video\_info url.

 

Parameters:

*   **video\_id** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – A YouTube video identifier.
*   **embed\_html** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The html contents of the embed page (for age restricted videos).

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

Returns:

`https://youtube.com/get_video_info` with necessary GET parameters.

Cipher[¶](#module-pytube.cipher "Permalink to this headline")
-------------------------------------------------------------

This module contains all logic necessary to decipher the signature.

YouTube’s strategy to restrict downloading videos is to send a ciphered version of the signature to the client, along with the decryption algorithm obfuscated in JavaScript. For the clients to play the videos, JavaScript must take the ciphered version, cycle it through a series of “transform functions,” and then signs the media URL with the output.

This module is responsible for (1) finding and extracting those “transform functions” (2) maps them to Python equivalents and (3) taking the ciphered signature and decoding it.

`pytube.cipher.``get_initial_function_name`(_js: str_) → str[\[source\]](_modules/pytube/cipher.html#get_initial_function_name)[¶](#pytube.cipher.get_initial_function_name "Permalink to this definition")

Extract the name of the function responsible for computing the signature. :param str js:

> The contents of the base.js asset file.

 

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

Returns:

Function name from regex match

`pytube.cipher.``get_throttling_function_array`(_js: str_) → List\[Any\][\[source\]](_modules/pytube/cipher.html#get_throttling_function_array)[¶](#pytube.cipher.get_throttling_function_array "Permalink to this definition")

Extract the “c” array.

 

Parameters:

**js** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The contents of the base.js asset file.

Returns:

The array of various integers, arrays, and functions.

`pytube.cipher.``get_throttling_function_code`(_js: str_) → str[\[source\]](_modules/pytube/cipher.html#get_throttling_function_code)[¶](#pytube.cipher.get_throttling_function_code "Permalink to this definition")

Extract the raw code for the throttling function.

 

Parameters:

**js** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The contents of the base.js asset file.

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

Returns:

The name of the function used to compute the throttling parameter.

`pytube.cipher.``get_throttling_function_name`(_js: str_) → str[\[source\]](_modules/pytube/cipher.html#get_throttling_function_name)[¶](#pytube.cipher.get_throttling_function_name "Permalink to this definition")

Extract the name of the function that computes the throttling parameter.

 

Parameters:

**js** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The contents of the base.js asset file.

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

Returns:

The name of the function used to compute the throttling parameter.

`pytube.cipher.``get_throttling_plan`(_js: str_)[\[source\]](_modules/pytube/cipher.html#get_throttling_plan)[¶](#pytube.cipher.get_throttling_plan "Permalink to this definition")

Extract the “throttling plan”.

The “throttling plan” is a list of tuples used for calling functions in the c array. The first element of the tuple is the index of the function to call, and any remaining elements of the tuple are arguments to pass to that function.

 

Parameters:

**js** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The contents of the base.js asset file.

Returns:

The full function code for computing the throttlign parameter.

`pytube.cipher.``get_transform_map`(_js: str_, _var: str_) → Dict\[KT, VT\][\[source\]](_modules/pytube/cipher.html#get_transform_map)[¶](#pytube.cipher.get_transform_map "Permalink to this definition")

Build a transform function lookup.

Build a lookup table of obfuscated JavaScript function names to the Python equivalents.

 

Parameters:

*   **js** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The contents of the base.js asset file.
*   **var** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The obfuscated variable name that stores an object with all functions that descrambles the signature.

`pytube.cipher.``get_transform_object`(_js: str_, _var: str_) → List\[str\][\[source\]](_modules/pytube/cipher.html#get_transform_object)[¶](#pytube.cipher.get_transform_object "Permalink to this definition")

Extract the “transform object”.

The “transform object” contains the function definitions referenced in the “transform plan”. The `var` argument is the obfuscated variable name which contains these functions, for example, given the function call `DE.AJ(a,15)` returned by the transform plan, “DE” would be the var.

 

Parameters:

*   **js** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The contents of the base.js asset file.
*   **var** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The obfuscated variable name that stores an object with all functions that descrambles the signature.

**Example**:

\>>> get\_transform\_object(js, 'DE')
\['AJ:function(a){a.reverse()}',
'VR:function(a,b){a.splice(0,b)}',
'kT:function(a,b){var c=a\[0\];a\[0\]=a\[b%a.length\];a\[b\]=c}'\]

`pytube.cipher.``get_transform_plan`(_js: str_) → List\[str\][\[source\]](_modules/pytube/cipher.html#get_transform_plan)[¶](#pytube.cipher.get_transform_plan "Permalink to this definition")

Extract the “transform plan”.

The “transform plan” is the functions that the ciphered signature is cycled through to obtain the actual signature.

 

Parameters:

**js** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The contents of the base.js asset file.

**Example**:

\[‘DE.AJ(a,15)’, ‘DE.VR(a,3)’, ‘DE.AJ(a,51)’, ‘DE.VR(a,3)’, ‘DE.kT(a,51)’, ‘DE.kT(a,8)’, ‘DE.VR(a,3)’, ‘DE.kT(a,21)’\]

`pytube.cipher.``js_splice`(_arr: list_, _start: int_, _delete\_count=None_, _\*items_)[\[source\]](_modules/pytube/cipher.html#js_splice)[¶](#pytube.cipher.js_splice "Permalink to this definition")

Implementation of javascript’s splice function.

 

Parameters:

*   **arr** ([_list_](https://docs.python.org/3/library/stdtypes.html#list "(in Python v3.11)")) – Array to splice
*   **start** ([_int_](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")) – Index at which to start changing the array
*   **delete\_count** ([_int_](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")) – Number of elements to delete from the array
*   **\*items** –
    
    Items to add to the array
    

Reference: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/splice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice) # noqa:E501

`pytube.cipher.``map_functions`(_js\_func: str_) → Callable[\[source\]](_modules/pytube/cipher.html#map_functions)[¶](#pytube.cipher.map_functions "Permalink to this definition")

For a given JavaScript transform function, return the Python equivalent.

 

Parameters:

**js\_func** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The JavaScript version of the transform function.

`pytube.cipher.``reverse`(_arr: List\[T\], \_: Optional\[Any\]_)[\[source\]](_modules/pytube/cipher.html#reverse)[¶](#pytube.cipher.reverse "Permalink to this definition")

Reverse elements in a list.

This function is equivalent to:

function(a, b) { a.reverse() }

This method takes an unused `b` variable as their transform functions universally sent two arguments.

**Example**:

\>>> reverse(\[1, 2, 3, 4\])
\[4, 3, 2, 1\]

`pytube.cipher.``splice`(_arr: List\[T\], b: int_)[\[source\]](_modules/pytube/cipher.html#splice)[¶](#pytube.cipher.splice "Permalink to this definition")

Add/remove items to/from a list.

This function is equivalent to:

function(a, b) { a.splice(0, b) }

**Example**:

\>>> splice(\[1, 2, 3, 4\], 2)
\[1, 2\]

`pytube.cipher.``swap`(_arr: List\[T\], b: int_)[\[source\]](_modules/pytube/cipher.html#swap)[¶](#pytube.cipher.swap "Permalink to this definition")

Swap positions at b modulus the list length.

This function is equivalent to:

function(a, b) { var c\=a\[0\];a\[0\]\=a\[b%a.length\];a\[b\]\=c }

**Example**:

\>>> swap(\[1, 2, 3, 4\], 2)
\[3, 2, 1, 4\]

`pytube.cipher.``throttling_cipher_function`(_d: list_, _e: str_)[\[source\]](_modules/pytube/cipher.html#throttling_cipher_function)[¶](#pytube.cipher.throttling_cipher_function "Permalink to this definition")

This ciphers d with e to generate a new list.

In the javascript, the operation is as follows: var h = \[A-Za-z0-9-\_\], f = 96; // simplified from switch-case loop d.forEach(

> function(l,m,n){
> 
> this.push(
> 
> n\[m\]=h\[
> 
> (h.indexOf(l)-h.indexOf(this\[m\])+m-32+f–)%h.length
> 
> \]
> 
> )
> 
> }, e.split(“”)

)

`pytube.cipher.``throttling_mod_func`(_d: list_, _e: int_)[\[source\]](_modules/pytube/cipher.html#throttling_mod_func)[¶](#pytube.cipher.throttling_mod_func "Permalink to this definition")

Perform the modular function from the throttling array functions.

In the javascript, the modular operation is as follows: e = (e % d.length + d.length) % d.length

We simply translate this to python here.

`pytube.cipher.``throttling_nested_splice`(_d: list_, _e: int_)[\[source\]](_modules/pytube/cipher.html#throttling_nested_splice)[¶](#pytube.cipher.throttling_nested_splice "Permalink to this definition")

Nested splice function in throttling js.

In the javascript, the operation is as follows: function(d,e){

> e=(e%d.length+d.length)%d.length; d.splice(
> 
> > 0, 1, d.splice(
> > 
> > > e, 1, d\[0\]
> > 
> > )\[0\]
> 
> )

}

While testing, all this seemed to do is swap element 0 and e, but the actual process is preserved in case there was an edge case that was not considered.

`pytube.cipher.``throttling_prepend`(_d: list_, _e: int_)[\[source\]](_modules/pytube/cipher.html#throttling_prepend)[¶](#pytube.cipher.throttling_prepend "Permalink to this definition")

In the javascript, the operation is as follows: function(d,e){

> e=(e%d.length+d.length)%d.length; d.splice(-e).reverse().forEach(
> 
> > function(f){
> > 
> > d.unshift(f)
> > 
> > }
> 
> )

}

Effectively, this moves the last e elements of d to the beginning.

`pytube.cipher.``throttling_push`(_d: list_, _e: Any_)[\[source\]](_modules/pytube/cipher.html#throttling_push)[¶](#pytube.cipher.throttling_push "Permalink to this definition")

Pushes an element onto a list.

`pytube.cipher.``throttling_reverse`(_arr: list_)[\[source\]](_modules/pytube/cipher.html#throttling_reverse)[¶](#pytube.cipher.throttling_reverse "Permalink to this definition")

Reverses the input list.

Needs to do an in-place reversal so that the passed list gets changed. To accomplish this, we create a reversed copy, and then change each indvidual element.

`pytube.cipher.``throttling_swap`(_d: list_, _e: int_)[\[source\]](_modules/pytube/cipher.html#throttling_swap)[¶](#pytube.cipher.throttling_swap "Permalink to this definition")

Swap positions of the 0’th and e’th elements in-place.

`pytube.cipher.``throttling_unshift`(_d: list_, _e: int_)[\[source\]](_modules/pytube/cipher.html#throttling_unshift)[¶](#pytube.cipher.throttling_unshift "Permalink to this definition")

Rotates the elements of the list to the right.

In the javascript, the operation is as follows: for(e=(e%d.length+d.length)%d.length;e–;)d.unshift(d.pop())

Exceptions[¶](#module-pytube.exceptions "Permalink to this headline")
---------------------------------------------------------------------

Library specific exception definitions.

_exception_ `pytube.exceptions.``AgeRestrictedError`(_video\_id: str_)[\[source\]](_modules/pytube/exceptions.html#AgeRestrictedError)[¶](#pytube.exceptions.AgeRestrictedError "Permalink to this definition")

Video is age restricted, and cannot be accessed without OAuth.

_exception_ `pytube.exceptions.``ExtractError`[\[source\]](_modules/pytube/exceptions.html#ExtractError)[¶](#pytube.exceptions.ExtractError "Permalink to this definition")

Data extraction based exception.

_exception_ `pytube.exceptions.``HTMLParseError`[\[source\]](_modules/pytube/exceptions.html#HTMLParseError)[¶](#pytube.exceptions.HTMLParseError "Permalink to this definition")

HTML could not be parsed

_exception_ `pytube.exceptions.``LiveStreamError`(_video\_id: str_)[\[source\]](_modules/pytube/exceptions.html#LiveStreamError)[¶](#pytube.exceptions.LiveStreamError "Permalink to this definition")

Video is a live stream.

_exception_ `pytube.exceptions.``MaxRetriesExceeded`[\[source\]](_modules/pytube/exceptions.html#MaxRetriesExceeded)[¶](#pytube.exceptions.MaxRetriesExceeded "Permalink to this definition")

Maximum number of retries exceeded.

_exception_ `pytube.exceptions.``MembersOnly`(_video\_id: str_)[\[source\]](_modules/pytube/exceptions.html#MembersOnly)[¶](#pytube.exceptions.MembersOnly "Permalink to this definition")

Video is members-only.

YouTube has special videos that are only viewable to users who have subscribed to a content creator. ref: [https://support.google.com/youtube/answer/7544492?hl=en](https://support.google.com/youtube/answer/7544492?hl=en)

_exception_ `pytube.exceptions.``PytubeError`[\[source\]](_modules/pytube/exceptions.html#PytubeError)[¶](#pytube.exceptions.PytubeError "Permalink to this definition")

Base pytube exception that all others inherit.

This is done to not pollute the built-in exceptions, which _could_ result in unintended errors being unexpectedly and incorrectly handled within implementers code.

_exception_ `pytube.exceptions.``RecordingUnavailable`(_video\_id: str_)[\[source\]](_modules/pytube/exceptions.html#RecordingUnavailable)[¶](#pytube.exceptions.RecordingUnavailable "Permalink to this definition")

_exception_ `pytube.exceptions.``RegexMatchError`(_caller: str, pattern: Union\[str, Pattern\[AnyStr\]\]_)[\[source\]](_modules/pytube/exceptions.html#RegexMatchError)[¶](#pytube.exceptions.RegexMatchError "Permalink to this definition")

Regex pattern did not return any matches.

_exception_ `pytube.exceptions.``VideoPrivate`(_video\_id: str_)[\[source\]](_modules/pytube/exceptions.html#VideoPrivate)[¶](#pytube.exceptions.VideoPrivate "Permalink to this definition")

_exception_ `pytube.exceptions.``VideoRegionBlocked`(_video\_id: str_)[\[source\]](_modules/pytube/exceptions.html#VideoRegionBlocked)[¶](#pytube.exceptions.VideoRegionBlocked "Permalink to this definition")

_exception_ `pytube.exceptions.``VideoUnavailable`(_video\_id: str_)[\[source\]](_modules/pytube/exceptions.html#VideoUnavailable)[¶](#pytube.exceptions.VideoUnavailable "Permalink to this definition")

Base video unavailable error.

Helpers[¶](#module-pytube.helpers "Permalink to this headline")
---------------------------------------------------------------

Various helper functions implemented by pytube.

_class_ `pytube.helpers.``DeferredGeneratorList`(_generator_)[\[source\]](_modules/pytube/helpers.html#DeferredGeneratorList)[¶](#pytube.helpers.DeferredGeneratorList "Permalink to this definition")

A wrapper class for deferring list generation.

Pytube has some continuation generators that create web calls, which means that any time a full list is requested, all of those web calls must be made at once, which could lead to slowdowns. This will allow individual elements to be queried, so that slowdowns only happen as necessary. For example, you can iterate over elements in the list without accessing them all simultaneously. This should allow for speed improvements for playlist and channel interactions.

`generate_all`()[\[source\]](_modules/pytube/helpers.html#DeferredGeneratorList.generate_all)[¶](#pytube.helpers.DeferredGeneratorList.generate_all "Permalink to this definition")

Generate all items.

`pytube.helpers.``cache`(_func: Callable\[\[...\], GenericType\]_) → GenericType[\[source\]](_modules/pytube/helpers.html#cache)[¶](#pytube.helpers.cache "Permalink to this definition")

mypy compatible annotation wrapper for lru\_cache

`pytube.helpers.``create_mock_html_json`(_vid\_id_) → Dict\[str, Any\][\[source\]](_modules/pytube/helpers.html#create_mock_html_json)[¶](#pytube.helpers.create_mock_html_json "Permalink to this definition")

Generate a json.gz file with sample html responses.

:param str vid\_id

YouTube video id

:return dict data

Dict used to generate the json.gz file

`pytube.helpers.``deprecated`(_reason: str_) → Callable[\[source\]](_modules/pytube/helpers.html#deprecated)[¶](#pytube.helpers.deprecated "Permalink to this definition")

This is a decorator which can be used to mark functions as deprecated. It will result in a warning being emitted when the function is used.

`pytube.helpers.``generate_all_html_json_mocks`()[\[source\]](_modules/pytube/helpers.html#generate_all_html_json_mocks)[¶](#pytube.helpers.generate_all_html_json_mocks "Permalink to this definition")

Regenerate the video mock json files for all current test videos.

This should automatically output to the test/mocks directory.

`pytube.helpers.``regex_search`(_pattern: str_, _string: str_, _group: int_) → str[\[source\]](_modules/pytube/helpers.html#regex_search)[¶](#pytube.helpers.regex_search "Permalink to this definition")

Shortcut method to search a string for a given pattern.

 

Parameters:

*   **pattern** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – A regular expression pattern.
*   **string** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – A target string to search.
*   **group** ([_int_](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")) – Index of group to return.

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)") or [tuple](https://docs.python.org/3/library/stdtypes.html#tuple "(in Python v3.11)")

Returns:

Substring pattern matches.

`pytube.helpers.``safe_filename`(_s: str_, _max\_length: int = 255_) → str[\[source\]](_modules/pytube/helpers.html#safe_filename)[¶](#pytube.helpers.safe_filename "Permalink to this definition")

Sanitize a string making it safe to use as a filename.

This function was based off the limitations outlined here: [https://en.wikipedia.org/wiki/Filename](https://en.wikipedia.org/wiki/Filename).

 

Parameters:

*   **s** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – A string to make safe for use as a file name.
*   **max\_length** ([_int_](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")) – The maximum filename character length.

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

Returns:

A sanitized string.

`pytube.helpers.``setup_logger`(_level: int = 40_, _log\_filename: Optional\[str\] = None_) → None[\[source\]](_modules/pytube/helpers.html#setup_logger)[¶](#pytube.helpers.setup_logger "Permalink to this definition")

Create a configured instance of logger.

 

Parameters:

**level** ([_int_](https://docs.python.org/3/library/functions.html#int "(in Python v3.11)")) – Describe the severity level of the logs to handle.

`pytube.helpers.``target_directory`(_output\_path: Optional\[str\] = None_) → str[\[source\]](_modules/pytube/helpers.html#target_directory)[¶](#pytube.helpers.target_directory "Permalink to this definition")

Function for determining target directory of a download. Returns an absolute path (if relative one given) or the current path (if none given). Makes directory if it does not exist.

 

Returns:

An absolute directory path as a string.

`pytube.helpers.``uniqueify`(_duped\_list: List\[T\]_) → List\[T\][\[source\]](_modules/pytube/helpers.html#uniqueify)[¶](#pytube.helpers.uniqueify "Permalink to this definition")

Remove duplicate items from a list, while maintaining list order.

:param List duped\_list

List to remove duplicates from

:return List result

De-duplicated list

Request[¶](#module-pytube.request "Permalink to this headline")
---------------------------------------------------------------

Implements a simple wrapper around urlopen.

`pytube.request.``filesize`[\[source\]](_modules/pytube/request.html#filesize)[¶](#pytube.request.filesize "Permalink to this definition")

Fetch size in bytes of file at given URL

 

Parameters:

**url** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The URL to get the size of

Returns:

int: size in bytes of remote file

`pytube.request.``get`(_url_, _extra\_headers=None_, _timeout=<object object>_)[\[source\]](_modules/pytube/request.html#get)[¶](#pytube.request.get "Permalink to this definition")

Send an http GET request.

 

Parameters:

*   **url** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The URL to perform the GET request for.
*   **extra\_headers** ([_dict_](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.11)")) – Extra headers to add to the request

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

Returns:

UTF-8 encoded string of response

`pytube.request.``head`(_url_)[\[source\]](_modules/pytube/request.html#head)[¶](#pytube.request.head "Permalink to this definition")

Fetch headers returned http GET request.

 

Parameters:

**url** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The URL to perform the GET request for.

Return type:

[dict](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.11)")

Returns:

dictionary of lowercase headers

`pytube.request.``post`(_url_, _extra\_headers=None_, _data=None_, _timeout=<object object>_)[\[source\]](_modules/pytube/request.html#post)[¶](#pytube.request.post "Permalink to this definition")

Send an http POST request.

 

Parameters:

*   **url** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The URL to perform the POST request for.
*   **extra\_headers** ([_dict_](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.11)")) – Extra headers to add to the request
*   **data** ([_dict_](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.11)")) – The data to send on the POST request

Return type:

[str](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")

Returns:

UTF-8 encoded string of response

`pytube.request.``seq_filesize`[\[source\]](_modules/pytube/request.html#seq_filesize)[¶](#pytube.request.seq_filesize "Permalink to this definition")

Fetch size in bytes of file at given URL from sequential requests

 

Parameters:

**url** ([_str_](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.11)")) – The URL to get the size of

Returns:

int: size in bytes of remote file

`pytube.request.``seq_stream`(_url_, _timeout=<object object>_, _max\_retries=0_)[\[source\]](_modules/pytube/request.html#seq_stream)[¶](#pytube.request.seq_stream "Permalink to this definition")

Read the response in sequence. :param str url: The URL to perform the GET request for. :rtype: Iterable\[bytes\]

`pytube.request.``stream`(_url_, _timeout=<object object>_, _max\_retries=0_)[\[source\]](_modules/pytube/request.html#stream)[¶](#pytube.request.stream "Permalink to this definition")

Read the response in chunks. :param str url: The URL to perform the GET request for. :rtype: Iterable\[bytes\]

[Previous](user/exceptions.html "Exception handling")

* * *

© Copyright Revision `a32fff39`.

Built with [Sphinx](http://sphinx-doc.org/) using a [theme](https://github.com/rtfd/sphinx_rtd_theme) provided by [Read the Docs](https://readthedocs.org).