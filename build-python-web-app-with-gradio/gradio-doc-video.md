Video
=====

    gradio.Video(···)

Video

Drop Video Here \- or - Click to Upload

[Built with Gradio ![logo](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='576'%20height='576'%20viewBox='0%200%20576%20576'%20fill='none'%3e%3cpath%20d='M287.5%20229L86%20344.5L287.5%20460L489%20344.5L287.5%20229Z'%20stroke='url(%23paint0_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M287.5%20116L86%20231.5L287.5%20347L489%20231.5L287.5%20116Z'%20stroke='url(%23paint1_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M86%20344L288%20229'%20stroke='url(%23paint2_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='bevel'/%3e%3cdefs%3e%3clinearGradient%20id='paint0_linear_102_7'%20x1='60'%20y1='341'%20x2='429.5'%20y2='344'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint1_linear_102_7'%20x1='513.5'%20y1='231'%20x2='143.5'%20y2='231'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint2_linear_102_7'%20x1='60'%20y1='344'%20x2='428.987'%20y2='341.811'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3c/defs%3e%3c/svg%3e)](https://gradio.app) 

### Description[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#description)

Creates a video component that can be used to upload/record videos (as an input) or display videos (as an output). For the video to be playable in the browser it must have a compatible container and codec combination. Allowed combinations are .mp4 with h264 codec, .ogg with theora codec, and .webm with vp9 codec. If the component detects that the output video would not be playable in the browser it will attempt to convert it to a playable mp4 video. If the conversion fails, the original video is returned.  

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Behavior[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#behavior)

**As input component**: Passes the uploaded video as a `str` filepath or URL whose extension can be modified by `format`.
-------------------------------------------------------------------------------------------------------------------------

##### Your function should accept one of these types:

    def predict(
    	value: str | None
    )
    	...

  

**As output component**: Expects a `str` or `pathlib.Path` filepath to a video which is displayed, or a `Tuple[str | pathlib.Path, str | pathlib.Path | None]` where the first element is a filepath to a video and the second element is an optional filepath to a subtitle file.
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

##### Your function should return one of these types:

    def predict(···) -> str | Path | tuple[str | Path, str | Path | None] | None
    	...	
    	return value

### Initialization[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#initialization)

Parameters ▼

    value: str | Path | tuple[str | Path, str | Path | None] | Callable | None

default `= None`

path or URL for the default value that Video component is going to take. Can also be a tuple consisting of (video filepath, subtitle filepath). If a subtitle file is provided, it should be of type .srt or .vtt. Or can be callable, in which case the function will be called whenever the app loads to set the initial value of the component.

    format: str | None

default `= None`

the file extension with which to save video, such as 'avi' or 'mp4'. This parameter applies both when this component is used as an input to determine which file format to convert user-provided video to, and when this component is used as an output to determine the format of video returned to the user. If None, no file format conversion is done and the video is kept as is. Use 'mp4' to ensure browser playability.

    sources: list[Literal['upload', 'webcam']] | Literal['upload', 'webcam'] | None

default `= None`

list of sources permitted for video. "upload" creates a box where user can drop a video file, "webcam" allows user to record a video from their webcam. If None, defaults to both \["upload, "webcam"\].

    height: int | str | None

default `= None`

The height of the component, specified in pixels if a number is passed, or in CSS units if a string is passed. This has no effect on the preprocessed video file, but will affect the displayed video.

    width: int | str | None

default `= None`

The width of the component, specified in pixels if a number is passed, or in CSS units if a string is passed. This has no effect on the preprocessed video file, but will affect the displayed video.

    label: str | None

default `= None`

the label for this component. Appears above the component and is also used as the header if there are a table of examples for this component. If None and used in a \`gr.Interface\`, the label will be the name of the parameter this component is assigned to.

    every: Timer | float | None

default `= None`

continously calls \`value\` to recalculate it if \`value\` is a function (has no effect otherwise). Can provide a Timer whose tick resets \`value\`, or a float that provides the regular interval for the reset Timer.

    inputs: Component | list[Component] | set[Component] | None

default `= None`

components that are used as inputs to calculate \`value\` if \`value\` is a function (has no effect otherwise). \`value\` is recalculated any time the inputs change.

    show_label: bool | None

default `= None`

if True, will display label.

    container: bool

default `= True`

if True, will place the component in a container - providing some extra padding around the border.

    scale: int | None

default `= None`

relative size compared to adjacent Components. For example if Components A and B are in a Row, and A has scale=2, and B has scale=1, A will be twice as wide as B. Should be an integer. scale applies in Rows, and to top-level Components in Blocks where fill\_height=True.

    min_width: int

default `= 160`

minimum pixel width, will wrap if not sufficient screen space to satisfy this value. If a certain scale value results in this Component being narrower than min\_width, the min\_width parameter will be respected first.

    interactive: bool | None

default `= None`

if True, will allow users to upload a video; if False, can only be used to display videos. If not provided, this is inferred based on whether the component is used as an input or output.

    visible: bool

default `= True`

if False, component will be hidden.

    elem_id: str | None

default `= None`

an optional string that is assigned as the id of this component in the HTML DOM. Can be used for targeting CSS styles.

    elem_classes: list[str] | str | None

default `= None`

an optional list of strings that are assigned as the classes of this component in the HTML DOM. Can be used for targeting CSS styles.

    render: bool

default `= True`

if False, component will not render be rendered in the Blocks context. Should be used if the intention is to assign event listeners now but render the component later.

    key: int | str | None

default `= None`

if assigned, will be used to assume identity across a re-render. Components that have the same key across a re-render will have their value preserved.

    mirror_webcam: bool

default `= True`

if True webcam will be mirrored. Default is True.

    include_audio: bool | None

default `= None`

whether the component should record/retain the audio track for a video. By default, audio is excluded for webcam videos and included for uploaded videos.

    autoplay: bool

default `= False`

whether to automatically play the video when the component is used as an output. Note: browsers will not autoplay video files if the user has not interacted with the page yet.

    show_share_button: bool | None

default `= None`

if True, will show a share icon in the corner of the component that allows user to share outputs to Hugging Face Spaces Discussions. If False, icon does not appear. If set to None (default behavior), then the icon appears if this Gradio app is launched on Spaces, but not otherwise.

    show_download_button: bool | None

default `= None`

if True, will show a download icon in the corner of the component that allows user to download the output. If False, icon does not appear. By default, it will be True for output components and False for input components.

    min_length: int | None

default `= None`

the minimum length of video (in seconds) that the user can pass into the prediction function. If None, there is no minimum length.

    max_length: int | None

default `= None`

the maximum length of video (in seconds) that the user can pass into the prediction function. If None, there is no maximum length.

    loop: bool

default `= False`

if True, the video will loop when it reaches the end and continue playing from the beginning.

    streaming: bool

default `= False`

when used set as an output, takes video chunks yielded from the backend and combines them into one streaming video output. Each chunk should be a video file with a .ts extension using an h.264 encoding. Mp4 files are also accepted but they will be converted to h.264 encoding.

    watermark: str | Path | None

default `= None`

an image file to be included as a watermark on the video. The image is not scaled and is displayed on the bottom right of the video. Valid formats for the image are: jpeg, png.

    webcam_constraints: dict[str, Any] | None

default `= None`

A dictionary that allows developers to specify custom media constraints for the webcam stream. This parameter provides flexibility to control the video stream's properties, such as resolution and front or rear camera on mobile devices. See [demo/webcam\_constraints](https://gradio.app/playground?demo=Blank&code=aW1wb3J0IGdyYWRpbyBhcyBncgppbXBvcnQgY3YyCgpkZWYgZ2V0X3ZpZGVvX3NoYXBlKHZpZGVvKToKICAgIGNhcCA9IGN2Mi5WaWRlb0NhcHR1cmUodmlkZW8pCiAgICB3aWR0aCA9IGludChjYXAuZ2V0KGN2Mi5DQVBfUFJPUF9GUkFNRV9XSURUSCkpCiAgICBoZWlnaHQgPSBpbnQoY2FwLmdldChjdjIuQ0FQX1BST1BfRlJBTUVfSEVJR0hUKSkKICAgIGNhcC5yZWxlYXNlKCkKICAgIHJldHVybiB7IndpZHRoIjogd2lkdGgsICJoZWlnaHQiOiBoZWlnaHR9CgpkZWYgaW1hZ2VfbW9kKGltYWdlKToKICAgIHdpZHRoLCBoZWlnaHQgPSBpbWFnZS5zaXplCiAgICByZXR1cm4geyJ3aWR0aCI6IHdpZHRoLCAiaGVpZ2h0IjogaGVpZ2h0fQoKCnZpZGVvID0gZ3IuSW50ZXJmYWNlKAogICAgZm49Z2V0X3ZpZGVvX3NoYXBlLAogICAgaW5wdXRzPWdyLlZpZGVvKHdlYmNhbV9jb25zdHJhaW50cz17InZpZGVvIjogeyJ3aWR0aCI6IDgwMCwgImhlaWdodCI6IDYwMH19LCBzb3VyY2VzPSJ3ZWJjYW0iKSwKICAgIG91dHB1dHM9Z3IuSlNPTigpCikKCmltYWdlID0gZ3IuSW50ZXJmYWNlKAogICAgICAgIGltYWdlX21vZCwKICAgICAgICBnci5JbWFnZSh0eXBlPSJwaWwiLCB3ZWJjYW1fY29uc3RyYWludHM9eyJ2aWRlbyI6IHsid2lkdGgiOiA4MDAsICJoZWlnaHQiOiA2MDB9fSwgc291cmNlcz0id2ViY2FtIiksCiAgICAgICAgZ3IuSnNvbigpKQoKd2l0aCBnci5CbG9ja3MoKSBhcyBkZW1vOgogICAgZ3IuTWFya2Rvd24oIiIiIyBXZWJjYW0gQ29uc3RyYWludHMKICAgICAgICAgICAgICAgIFRoZSB3ZWJjYW0gY29uc3RyYWludHMgYXJlIHNldCB0byA4MDB4NjAwIHdpdGggdGhlIGZvbGxvd2luZyBzeW50YXg6CiAgICAgICAgICAgICAgICBgYGBweXRob24KICAgICAgICAgICAgICAgIGdyLlZpZGVvKHdlYmNhbV9jb25zdHJhaW50cz17InZpZGVvIjogeyJ3aWR0aCI6IDgwMCwgImhlaWdodCI6IDYwMH19LCBzb3VyY2VzPSJ3ZWJjYW0iKQogICAgICAgICAgICAgICAgYGBgCiAgICAgICAgICAgICAgICAiIiIpCiAgICB3aXRoIGdyLlRhYnMoKToKICAgICAgICB3aXRoIGdyLlRhYigiVmlkZW8iKToKICAgICAgICAgICAgdmlkZW8ucmVuZGVyKCkKICAgICAgICB3aXRoIGdyLlRhYigiSW1hZ2UiKToKICAgICAgICAgICAgaW1hZ2UucmVuZGVyKCkKCmlmIF9fbmFtZV9fID09ICJfX21haW5fXyI6CiAgICBkZW1vLmxhdW5jaCgp&reqs=b3BlbmN2LXB5dGhvbg%3D%3D)

### Shortcuts[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#shortcuts)

Class

Interface String Shortcut

Initialization

`gradio.Video`

"video"

Uses default values

`gradio.PlayableVideo`

"playablevideo"

Uses format="mp4"

### Demos[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#demos)

video\_identity\_2

Open in 🎢 ↗

app.py

Run

⌘+↵

![lightning icon](data:image/svg+xml,%3c!--%20Lightning%20https://iconscout.com/icons/lightning%20by%20IconLauk%20https://iconscout.com/contributors/icon-lauk%20on%20IconScout%20https://iconscout.com'%20--%3e%3csvg%20xmlns='http://www.w3.org/2000/svg'%20enable-background='new%200%200%2032%2032'%20viewBox='0%200%2032%2032'%20id='lightning'%3e%3cpath%20fill='%23ff7c00'%20d='M26.9,10.5C26.7,10.2,26.4,10,26,10h-9V2c0-0.4-0.3-0.8-0.7-1c-0.4-0.1-0.9,0-1.1,0.4l-10,14c-0.2,0.3-0.3,0.7-0.1,1%20C5.3,16.8,5.6,17,6,17h8.8L13,29.9c-0.1,0.5,0.2,0.9,0.6,1.1c0.1,0,0.2,0.1,0.3,0.1c0.3,0,0.7-0.2,0.8-0.5l12-19%20C27,11.2,27,10.8,26.9,10.5z'/%3e%3c/svg%3e) Interactive

99

1

2

3

4

5

6

7

8

9

10

11

12

›

⌄

⌄

import gradio as gr

  

def video\_identity(video):

return video

  

demo \= gr.Interface(video\_identity,

gr.Video(),

"playable\_video",

)

  

if \_\_name\_\_ \== "\_\_main\_\_":

demo.launch()

Loading...

    import gradio as gr
    
    def video_identity(video):
        return video
    
    demo = gr.Interface(video_identity,
                        gr.Video(),
                        "playable_video",
                        )
    
    if __name__ == "__main__":
        demo.launch()
    

Loading...

[gradio/video\_identity\_2](https://huggingface.co/spaces/gradio/video_identity_2) built with [Gradio](https://gradio.app). Hosted on [![Hugging Face Space](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='10'%20height='10'%20fill='none'%3e%3cpath%20fill='%23FF3270'%20d='M1.93%206.03v2.04h2.04V6.03H1.93Z'/%3e%3cpath%20fill='%23861FFF'%20d='M6.03%206.03v2.04h2.04V6.03H6.03Z'/%3e%3cpath%20fill='%23097EFF'%20d='M1.93%201.93v2.04h2.04V1.93H1.93Z'/%3e%3cpath%20fill='%23000'%20fill-rule='evenodd'%20d='M.5%201.4c0-.5.4-.9.9-.9h3.1a.9.9%200%200%201%20.87.67A2.44%202.44%200%200%201%209.5%202.95c0%20.65-.25%201.24-.67%201.68.39.1.67.46.67.88v3.08c0%20.5-.4.91-.9.91H1.4a.9.9%200%200%201-.9-.9V1.4Zm1.43.53v2.04h2.04V1.93H1.93Zm0%206.14V6.03h2.04v2.04H1.93Zm4.1%200V6.03h2.04v2.04H6.03Zm0-5.12a1.02%201.02%200%201%201%202.04%200%201.02%201.02%200%200%201-2.04%200Z'%20clip-rule='evenodd'/%3e%3cpath%20fill='%23FFD702'%20d='M7.05%201.93a1.02%201.02%200%201%200%200%202.04%201.02%201.02%200%200%200%200-2.04Z'/%3e%3c/svg%3e) Spaces](https://huggingface.co/spaces)

### Event Listeners[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#event-listeners)

#### Description

Event listeners allow you to respond to user interactions with the UI components you've defined in a Gradio Blocks app. When a user interacts with an element, such as changing a slider value or uploading an image, a function is called.

#### Supported Event Listeners

The Video component supports the following event listeners. Each event listener takes the same parameters, which are listed in the [Event Parameters](#event-listeners-arguments) table below.

Listener

Description

`Video.change(fn, ···)`

Triggered when the value of the Video changes either because of user input (e.g. a user types in a textbox) OR because of a function update (e.g. an image receives a value from the output of an event trigger). See `.input()` for a listener that is only triggered by user input.

`Video.clear(fn, ···)`

This listener is triggered when the user clears the Video using the clear button for the component.

`Video.start_recording(fn, ···)`

This listener is triggered when the user starts recording with the Video.

`Video.stop_recording(fn, ···)`

This listener is triggered when the user stops recording with the Video.

`Video.stop(fn, ···)`

This listener is triggered when the user reaches the end of the media playing in the Video.

`Video.play(fn, ···)`

This listener is triggered when the user plays the media in the Video.

`Video.pause(fn, ···)`

This listener is triggered when the media in the Video stops for any reason.

`Video.end(fn, ···)`

This listener is triggered when the user reaches the end of the media playing in the Video.

`Video.upload(fn, ···)`

This listener is triggered when the user uploads a file into the Video.

#### Event Parameters

Parameters ▼

    fn: Callable | None | Literal['decorator']

default `= "decorator"`

the function to call when this event is triggered. Often a machine learning model's prediction function. Each parameter of the function corresponds to one input component, and the function should return a single value or a tuple of values, with each element in the tuple corresponding to one output component.

    inputs: Component | BlockContext | list[Component | BlockContext] | Set[Component | BlockContext] | None

default `= None`

List of gradio.components to use as inputs. If the function takes no inputs, this should be an empty list.

    outputs: Component | BlockContext | list[Component | BlockContext] | Set[Component | BlockContext] | None

default `= None`

List of gradio.components to use as outputs. If the function returns no outputs, this should be an empty list.

    api_name: str | None | Literal[False]

default `= None`

defines how the endpoint appears in the API docs. Can be a string, None, or False. If set to a string, the endpoint will be exposed in the API docs with the given name. If None (default), the name of the function will be used as the API endpoint. If False, the endpoint will not be exposed in the API docs and downstream apps (including those that \`gr.load\` this app) will not be able to use this event.

    scroll_to_output: bool

default `= False`

If True, will scroll to output component on completion

    show_progress: Literal['full', 'minimal', 'hidden']

default `= "full"`

how to show the progress animation while event is running: "full" shows a spinner which covers the output component area as well as a runtime display in the upper right corner, "minimal" only shows the runtime display, "hidden" shows no progress animation at all

    queue: bool

default `= True`

If True, will place the request on the queue, if the queue has been enabled. If False, will not put this event on the queue, even if the queue has been enabled. If None, will use the queue setting of the gradio app.

    batch: bool

default `= False`

If True, then the function should process a batch of inputs, meaning that it should accept a list of input values for each parameter. The lists should be of equal length (and be up to length \`max\_batch\_size\`). The function is then \*required\* to return a tuple of lists (even if there is only 1 output component), with each list in the tuple corresponding to one output component.

    max_batch_size: int

default `= 4`

Maximum number of inputs to batch together if this is called from the queue (only relevant if batch=True)

    preprocess: bool

default `= True`

If False, will not run preprocessing of component data before running 'fn' (e.g. leaving it as a base64 string if this method is called with the \`Image\` component).

    postprocess: bool

default `= True`

If False, will not run postprocessing of component data before returning 'fn' output to the browser.

    cancels: dict[str, Any] | list[dict[str, Any]] | None

default `= None`

A list of other events to cancel when this listener is triggered. For example, setting cancels=\[click\_event\] will cancel the click\_event, where click\_event is the return value of another components .click method. Functions that have not yet run (or generators that are iterating) will be cancelled, but functions that are currently running will be allowed to finish.

    trigger_mode: Literal['once', 'multiple', 'always_last'] | None

default `= None`

If "once" (default for all events except \`.change()\`) would not allow any submissions while an event is pending. If set to "multiple", unlimited submissions are allowed while pending, and "always\_last" (default for \`.change()\` and \`.key\_up()\` events) would allow a second submission after the pending event is complete.

    js: str | None

default `= None`

Optional frontend js method to run before running 'fn'. Input arguments for js method are values of 'inputs' and 'outputs', return should be a list of values for output components.

    concurrency_limit: int | None | Literal['default']

default `= "default"`

If set, this is the maximum number of this event that can be running simultaneously. Can be set to None to mean no concurrency\_limit (any number of this event can be running simultaneously). Set to "default" to use the default concurrency limit (defined by the \`default\_concurrency\_limit\` parameter in \`Blocks.queue()\`, which itself is 1 by default).

    concurrency_id: str | None

default `= None`

If set, this is the id of the concurrency group. Events with the same concurrency\_id will be limited by the lowest set concurrency\_limit.

    show_api: bool

default `= True`

whether to show this event in the "view API" page of the Gradio app, or in the ".view\_api()" method of the Gradio clients. Unlike setting api\_name to False, setting show\_api to False will still allow downstream apps as well as the Clients to use this event. If fn is None, show\_api will automatically be set to False.

    time_limit: int | None

default `= None`

    stream_every: float

default `= 0.5`

    like_user_message: bool

default `= False`