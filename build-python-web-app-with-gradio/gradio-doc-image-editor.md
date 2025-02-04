ImageEditor
===========

    gradio.ImageEditor(···)

Image

.cls-1 { fill: none; }

Layer 1

Upload an image

or

select the draw tool to start

[Built with Gradio ![logo](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='576'%20height='576'%20viewBox='0%200%20576%20576'%20fill='none'%3e%3cpath%20d='M287.5%20229L86%20344.5L287.5%20460L489%20344.5L287.5%20229Z'%20stroke='url(%23paint0_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M287.5%20116L86%20231.5L287.5%20347L489%20231.5L287.5%20116Z'%20stroke='url(%23paint1_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M86%20344L288%20229'%20stroke='url(%23paint2_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='bevel'/%3e%3cdefs%3e%3clinearGradient%20id='paint0_linear_102_7'%20x1='60'%20y1='341'%20x2='429.5'%20y2='344'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint1_linear_102_7'%20x1='513.5'%20y1='231'%20x2='143.5'%20y2='231'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint2_linear_102_7'%20x1='60'%20y1='344'%20x2='428.987'%20y2='341.811'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3c/defs%3e%3c/svg%3e)](https://gradio.app) 

### Description[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#description)

Creates an image component that, as an input, can be used to upload and edit images using simple editing tools such as brushes, strokes, cropping, and layers. Or, as an output, this component can be used to display images.  

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Behavior[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#behavior)

**As input component**: Passes the uploaded images as an instance of EditorValue, which is just a `dict` with keys: 'background', 'layers', and 'composite'. The values corresponding to 'background' and 'composite' are images, while 'layers' is a `list` of images. The images are of type `PIL.Image`, `np.array`, or `str` filepath, depending on the `type` parameter.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

##### Your function should accept one of these types:

    def predict(
    	value: EditorValue | None
    )
    	...

  

**As output component**: Expects a EditorValue, which is just a dictionary with keys: 'background', 'layers', and 'composite'. The values corresponding to 'background' and 'composite' should be images or None, while `layers` should be a list of images. Images can be of type `PIL.Image`, `np.array`, or `str` filepath/URL. Or, the value can be simply a single image (`ImageType`), in which case it will be used as the background.
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

##### Your function should return one of these types:

    def predict(···) -> EditorValue | ImageType | None
    	...	
    	return value

### Initialization[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#initialization)

Parameters ▼

    value: EditorValue | ImageType | None

default `= None`

Optional initial image(s) to populate the image editor. Should be a dictionary with keys: \`background\`, \`layers\`, and \`composite\`. The values corresponding to \`background\` and \`composite\` should be images or None, while \`layers\` should be a list of images. Images can be of type PIL.Image, np.array, or str filepath/URL. Or, the value can be a callable, in which case the function will be called whenever the app loads to set the initial value of the component.

    height: int | str | None

default `= None`

The height of the component, specified in pixels if a number is passed, or in CSS units if a string is passed. This has no effect on the preprocessed image files or numpy arrays, but will affect the displayed images.

    width: int | str | None

default `= None`

The width of the component, specified in pixels if a number is passed, or in CSS units if a string is passed. This has no effect on the preprocessed image files or numpy arrays, but will affect the displayed images.

    image_mode: Literal['1', 'L', 'P', 'RGB', 'RGBA', 'CMYK', 'YCbCr', 'LAB', 'HSV', 'I', 'F']

default `= "RGBA"`

"RGB" if color, or "L" if black and white. See https://pillow.readthedocs.io/en/stable/handbook/concepts.html for other supported image modes and their meaning.

    sources: Iterable[Literal['upload', 'webcam', 'clipboard']] | Literal['upload', 'webcam', 'clipboard'] | None

default `= ('upload', 'webcam', 'clipboard')`

List of sources that can be used to set the background image. "upload" creates a box where user can drop an image file, "webcam" allows user to take snapshot from their webcam, "clipboard" allows users to paste an image from the clipboard.

    type: Literal['numpy', 'pil', 'filepath']

default `= "numpy"`

The format the images are converted to before being passed into the prediction function. "numpy" converts the images to numpy arrays with shape (height, width, 3) and values from 0 to 255, "pil" converts the images to PIL image objects, "filepath" passes images as str filepaths to temporary copies of the images.

    label: str | None

default `= None`

the label for this component. Appears above the component and is also used as the header if there are a table of examples for this component. If None and used in a \`gr.Interface\`, the label will be the name of the parameter this component is assigned to.

    every: Timer | float | None

default `= None`

Continously calls \`value\` to recalculate it if \`value\` is a function (has no effect otherwise). Can provide a Timer whose tick resets \`value\`, or a float that provides the regular interval for the reset Timer.

    inputs: Component | list[Component] | set[Component] | None

default `= None`

Components that are used as inputs to calculate \`value\` if \`value\` is a function (has no effect otherwise). \`value\` is recalculated any time the inputs change.

    show_label: bool | None

default `= None`

if True, will display label.

    show_download_button: bool

default `= True`

If True, will display button to download image.

    container: bool

default `= True`

If True, will place the component in a container - providing some extra padding around the border.

    scale: int | None

default `= None`

relative size compared to adjacent Components. For example if Components A and B are in a Row, and A has scale=2, and B has scale=1, A will be twice as wide as B. Should be an integer. scale applies in Rows, and to top-level Components in Blocks where fill\_height=True.

    min_width: int

default `= 160`

minimum pixel width, will wrap if not sufficient screen space to satisfy this value. If a certain scale value results in this Component being narrower than min\_width, the min\_width parameter will be respected first.

    interactive: bool | None

default `= None`

if True, will allow users to upload and edit an image; if False, can only be used to display images. If not provided, this is inferred based on whether the component is used as an input or output.

    visible: bool

default `= True`

If False, component will be hidden.

    elem_id: str | None

default `= None`

An optional string that is assigned as the id of this component in the HTML DOM. Can be used for targeting CSS styles.

    elem_classes: list[str] | str | None

default `= None`

An optional list of strings that are assigned as the classes of this component in the HTML DOM. Can be used for targeting CSS styles.

    render: bool

default `= True`

If False, component will not render be rendered in the Blocks context. Should be used if the intention is to assign event listeners now but render the component later.

    key: int | str | None

default `= None`

if assigned, will be used to assume identity across a re-render. Components that have the same key across a re-render will have their value preserved.

    placeholder: str | None

default `= None`

Custom text for the upload area. Overrides default upload messages when provided. Accepts new lines and \`#\` to designate a heading.

    mirror_webcam: bool

default `= True`

If True webcam will be mirrored. Default is True.

    show_share_button: bool | None

default `= None`

If True, will show a share icon in the corner of the component that allows user to share outputs to Hugging Face Spaces Discussions. If False, icon does not appear. If set to None (default behavior), then the icon appears if this Gradio app is launched on Spaces, but not otherwise.

    crop_size: tuple[int | float, int | float] | str | None

default `= None`

The size of the crop box in pixels. If a tuple, the first value is the width and the second value is the height. If a string, the value must be a ratio in the form \`width:height\` (e.g. "16:9").

    transforms: Iterable[Literal['crop']]

default `= ('crop',)`

The transforms tools to make available to users. "crop" allows the user to crop the image.

    eraser: Eraser | None | Literal[False]

default `= None`

The options for the eraser tool in the image editor. Should be an instance of the \`gr.Eraser\` class, or None to use the default settings. Can also be False to hide the eraser tool. [See \`gr.Eraser\` docs](#eraser).

    brush: Brush | None | Literal[False]

default `= None`

The options for the brush tool in the image editor. Should be an instance of the \`gr.Brush\` class, or None to use the default settings. Can also be False to hide the brush tool, which will also hide the eraser tool. [See \`gr.Brush\` docs](#brush).

    format: str

default `= "webp"`

Format to save image if it does not already have a valid format (e.g. if the image is being returned to the frontend as a numpy array or PIL Image). The format should be supported by the PIL library. This parameter has no effect on SVG files.

    layers: bool

default `= True`

If True, will allow users to add layers to the image. If False, the layers option will be hidden.

    canvas_size: tuple[int, int] | None

default `= None`

The size of the default canvas in pixels. If a tuple, the first value is the width and the second value is the height. If None, the canvas size will be the same as the background image or 800 x 600 if no background image is provided.

    show_fullscreen_button: bool

default `= True`

If True, will display button to view image in fullscreen mode.

### Shortcuts[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#shortcuts)

Class

Interface String Shortcut

Initialization

`gradio.ImageEditor`

"imageeditor"

Uses default values

`gradio.Sketchpad`

"sketchpad"

Uses sources=(), brush=Brush(colors=\["#000000"\], color\_mode="fixed")

`gradio.Paint`

"paint"

Uses sources=()

`gradio.ImageMask`

"imagemask"

Uses brush=Brush(colors=\["#000000"\], color\_mode="fixed")

### Demos[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#demos)

image\_editor

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

13

14

15

16

17

18

19

20

21

22

23

24

25

26

27

28

›

⌄

⌄

⌄

⌄

⌄

import gradio as gr

import time

  

def sleep(im):

time.sleep(5)

return \[im\["background"\], im\["layers"\]\[0\], im\["layers"\]\[1\], im\["composite"\]\]

  

def predict(im):

return im\["composite"\]

  

with gr.Blocks() as demo:

with gr.Row():

im \= gr.ImageEditor(

type\="numpy",

crop\_size\="1:1",

)

im\_preview \= gr.Image()

n\_upload \= gr.Number(0, label\="Number of upload events", step\=1)

n\_change \= gr.Number(0, label\="Number of change events", step\=1)

n\_input \= gr.Number(0, label\="Number of input events", step\=1)

  

im.upload(lambda x: x + 1, outputs\=n\_upload, inputs\=n\_upload)

im.change(lambda x: x + 1, outputs\=n\_change, inputs\=n\_change)

im.input(lambda x: x + 1, outputs\=n\_input, inputs\=n\_input)

im.change(predict, outputs\=im\_preview, inputs\=im, show\_progress\="hidden")

  

if \_\_name\_\_ \== "\_\_main\_\_":

demo.launch()

Loading...

    import gradio as gr
    import time
    
    def sleep(im):
        time.sleep(5)
        return [im["background"], im["layers"][0], im["layers"][1], im["composite"]]
    
    def predict(im):
        return im["composite"]
    
    with gr.Blocks() as demo:
        with gr.Row():
            im = gr.ImageEditor(
                type="numpy",
                crop_size="1:1",
            )
            im_preview = gr.Image()
        n_upload = gr.Number(0, label="Number of upload events", step=1)
        n_change = gr.Number(0, label="Number of change events", step=1)
        n_input = gr.Number(0, label="Number of input events", step=1)
    
        im.upload(lambda x: x + 1, outputs=n_upload, inputs=n_upload)
        im.change(lambda x: x + 1, outputs=n_change, inputs=n_change)
        im.input(lambda x: x + 1, outputs=n_input, inputs=n_input)
        im.change(predict, outputs=im_preview, inputs=im, show_progress="hidden")
    
    if __name__ == "__main__":
        demo.launch()
    

Loading...

[gradio/image\_editor](https://huggingface.co/spaces/gradio/image_editor) built with [Gradio](https://gradio.app). Hosted on [![Hugging Face Space](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='10'%20height='10'%20fill='none'%3e%3cpath%20fill='%23FF3270'%20d='M1.93%206.03v2.04h2.04V6.03H1.93Z'/%3e%3cpath%20fill='%23861FFF'%20d='M6.03%206.03v2.04h2.04V6.03H6.03Z'/%3e%3cpath%20fill='%23097EFF'%20d='M1.93%201.93v2.04h2.04V1.93H1.93Z'/%3e%3cpath%20fill='%23000'%20fill-rule='evenodd'%20d='M.5%201.4c0-.5.4-.9.9-.9h3.1a.9.9%200%200%201%20.87.67A2.44%202.44%200%200%201%209.5%202.95c0%20.65-.25%201.24-.67%201.68.39.1.67.46.67.88v3.08c0%20.5-.4.91-.9.91H1.4a.9.9%200%200%201-.9-.9V1.4Zm1.43.53v2.04h2.04V1.93H1.93Zm0%206.14V6.03h2.04v2.04H1.93Zm4.1%200V6.03h2.04v2.04H6.03Zm0-5.12a1.02%201.02%200%201%201%202.04%200%201.02%201.02%200%200%201-2.04%200Z'%20clip-rule='evenodd'/%3e%3cpath%20fill='%23FFD702'%20d='M7.05%201.93a1.02%201.02%200%201%200%200%202.04%201.02%201.02%200%200%200%200-2.04Z'/%3e%3c/svg%3e) Spaces](https://huggingface.co/spaces)

### Event Listeners[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#event-listeners)

#### Description

Event listeners allow you to respond to user interactions with the UI components you've defined in a Gradio Blocks app. When a user interacts with an element, such as changing a slider value or uploading an image, a function is called.

#### Supported Event Listeners

The ImageEditor component supports the following event listeners. Each event listener takes the same parameters, which are listed in the [Event Parameters](#event-listeners-arguments) table below.

Listener

Description

`ImageEditor.clear(fn, ···)`

This listener is triggered when the user clears the ImageEditor using the clear button for the component.

`ImageEditor.change(fn, ···)`

Triggered when the value of the ImageEditor changes either because of user input (e.g. a user types in a textbox) OR because of a function update (e.g. an image receives a value from the output of an event trigger). See `.input()` for a listener that is only triggered by user input.

`ImageEditor.input(fn, ···)`

This listener is triggered when the user changes the value of the ImageEditor.

`ImageEditor.select(fn, ···)`

Event listener for when the user selects or deselects the ImageEditor. Uses event data gradio.SelectData to carry `value` referring to the label of the ImageEditor, and `selected` to refer to state of the ImageEditor. See EventData documentation on how to use this event data

`ImageEditor.upload(fn, ···)`

This listener is triggered when the user uploads a file into the ImageEditor.

`ImageEditor.apply(fn, ···)`

This listener is triggered when the user applies changes to the ImageEditor through an integrated UI action.

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

### Helper Classes[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#helper-classes)

### Brush[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#brush)

    gradio.Brush(···)

#### Description

A dataclass for specifying options for the brush tool in the ImageEditor component. An instance of this class can be passed to the `brush` parameter of `gr.ImageEditor`.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------

#### Initialization

Parameters ▼

    default_size: int | Literal['auto']

default `= "auto"`

The default radius, in pixels, of the brush tool. Defaults to "auto" in which case the radius is automatically determined based on the size of the image (generally 1/50th of smaller dimension).

    colors: Union[list[str], str, None]

default `= None`

A list of colors to make available to the user when using the brush. Defaults to a list of 5 colors.

    default_color: Union[str, Literal['auto']]

default `= "auto"`

The default color of the brush. Defaults to the first color in the \`colors\` list.

    color_mode: Literal['fixed', 'defaults']

default `= "defaults"`

If set to "fixed", user can only select from among the colors in \`colors\`. If "defaults", the colors in \`colors\` are provided as a default palette, but the user can also select any color using a color picker.

### Eraser[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#eraser)

    gradio.Eraser(···)

#### Description

A dataclass for specifying options for the eraser tool in the ImageEditor component. An instance of this class can be passed to the `eraser` parameter of `gr.ImageEditor`.
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------

#### Initialization

Parameters ▼

    default_size: int | Literal['auto']

default `= "auto"`

The default radius, in pixels, of the eraser tool. Defaults to "auto" in which case the radius is automatically determined based on the size of the image (generally 1/50th of smaller dimension).