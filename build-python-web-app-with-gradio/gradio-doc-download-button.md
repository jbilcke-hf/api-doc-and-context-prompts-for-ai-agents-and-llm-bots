New to Gradio? Start here: [Getting Started](/quickstart)

See the [Release History](/changelog)

[

←

DateTime



](./datetime)[

Dropdown

→

](./dropdown)

DownloadButton
==============

    gradio.DownloadButton(···)

### Description[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#description)

Creates a button, that when clicked, allows a user to download a single file of arbitrary type.  

--------------------------------------------------------------------------------------------------

### Behavior[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#behavior)

**As input component**: (Rarely used) passes the file as a `str` into the function.
-----------------------------------------------------------------------------------

##### Your function should accept one of these types:

    def predict(
    	value: str | None
    )
    	...

  

**As output component**: Expects a `str` or `pathlib.Path` filepath
-------------------------------------------------------------------

##### Your function should return one of these types:

    def predict(···) -> str | Path | None
    	...	
    	return value

### Initialization[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#initialization)

Parameters ▼

[🔗](#param-downloadbutton-label)

    label: str

default `= "Download"`

Text to display on the button. Defaults to "Download".

[🔗](#param-downloadbutton-value)

    value: str | Path | Callable | None

default `= None`

A str or pathlib.Path filepath or URL to download, or a Callable that returns a str or pathlib.Path filepath or URL to download.

[🔗](#param-downloadbutton-every)

    every: Timer | float | None

default `= None`

Continously calls \`value\` to recalculate it if \`value\` is a function (has no effect otherwise). Can provide a Timer whose tick resets \`value\`, or a float that provides the regular interval for the reset Timer.

[🔗](#param-downloadbutton-inputs)

    inputs: Component | list[Component] | set[Component] | None

default `= None`

Components that are used as inputs to calculate \`value\` if \`value\` is a function (has no effect otherwise). \`value\` is recalculated any time the inputs change.

[🔗](#param-downloadbutton-variant)

    variant: Literal['primary', 'secondary', 'stop']

default `= "secondary"`

'primary' for main call-to-action, 'secondary' for a more subdued style, 'stop' for a stop button.

[🔗](#param-downloadbutton-visible)

    visible: bool

default `= True`

If False, component will be hidden.

[🔗](#param-downloadbutton-size)

    size: Literal['sm', 'md', 'lg']

default `= "lg"`

size of the button. Can be "sm", "md", or "lg".

[🔗](#param-downloadbutton-icon)

    icon: str | None

default `= None`

URL or path to the icon file to display within the button. If None, no icon will be displayed.

[🔗](#param-downloadbutton-scale)

    scale: int | None

default `= None`

relative size compared to adjacent Components. For example if Components A and B are in a Row, and A has scale=2, and B has scale=1, A will be twice as wide as B. Should be an integer. scale applies in Rows, and to top-level Components in Blocks where fill\_height=True.

[🔗](#param-downloadbutton-min-width)

    min_width: int | None

default `= None`

minimum pixel width, will wrap if not sufficient screen space to satisfy this value. If a certain scale value results in this Component being narrower than min\_width, the min\_width parameter will be respected first.

[🔗](#param-downloadbutton-interactive)

    interactive: bool

default `= True`

If False, the UploadButton will be in a disabled state.

[🔗](#param-downloadbutton-elem-id)

    elem_id: str | None

default `= None`

An optional string that is assigned as the id of this component in the HTML DOM. Can be used for targeting CSS styles.

[🔗](#param-downloadbutton-elem-classes)

    elem_classes: list[str] | str | None

default `= None`

An optional list of strings that are assigned as the classes of this component in the HTML DOM. Can be used for targeting CSS styles.

[🔗](#param-downloadbutton-render)

    render: bool

default `= True`

If False, component will not render be rendered in the Blocks context. Should be used if the intention is to assign event listeners now but render the component later.

[🔗](#param-downloadbutton-key)

    key: int | str | None

default `= None`

if assigned, will be used to assume identity across a re-render. Components that have the same key across a re-render will have their value preserved.

### Shortcuts[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#shortcuts)

Class

Interface String Shortcut

Initialization

`gradio.DownloadButton`

"downloadbutton"

Uses default values

### Demos[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#demos)

upload\_and\_download

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

›

⌄

⌄

⌄

⌄

⌄

from pathlib import Path

import gradio as gr

  

def upload\_file(filepath):

name \= Path(filepath).name

return \[gr.UploadButton(visible\=False), gr.DownloadButton(label\=f"Download {name}", value\=filepath, visible\=True)\]

  

def download\_file():

return \[gr.UploadButton(visible\=True), gr.DownloadButton(visible\=False)\]

  

with gr.Blocks() as demo:

gr.Markdown("First upload a file and and then you'll be able download it (but only once!)")

with gr.Row():

u \= gr.UploadButton("Upload a file", file\_count\="single")

d \= gr.DownloadButton("Download the file", visible\=False)

  

u.upload(upload\_file, u, \[u, d\])

d.click(download\_file, None, \[u, d\])

  

if \_\_name\_\_ \== "\_\_main\_\_":

demo.launch()

Loading...

    from pathlib import Path
    import gradio as gr
    
    def upload_file(filepath):
        name = Path(filepath).name
        return [gr.UploadButton(visible=False), gr.DownloadButton(label=f"Download {name}", value=filepath, visible=True)]
    
    def download_file():
        return [gr.UploadButton(visible=True), gr.DownloadButton(visible=False)]
    
    with gr.Blocks() as demo:
        gr.Markdown("First upload a file and and then you'll be able download it (but only once!)")
        with gr.Row():
            u = gr.UploadButton("Upload a file", file_count="single")
            d = gr.DownloadButton("Download the file", visible=False)
    
        u.upload(upload_file, u, [u, d])
        d.click(download_file, None, [u, d])
    
    if __name__ == "__main__":
        demo.launch()
    

Loading...

[gradio/upload\_and\_download](https://huggingface.co/spaces/gradio/upload_and_download) built with [Gradio](https://gradio.app). Hosted on [![Hugging Face Space](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='10'%20height='10'%20fill='none'%3e%3cpath%20fill='%23FF3270'%20d='M1.93%206.03v2.04h2.04V6.03H1.93Z'/%3e%3cpath%20fill='%23861FFF'%20d='M6.03%206.03v2.04h2.04V6.03H6.03Z'/%3e%3cpath%20fill='%23097EFF'%20d='M1.93%201.93v2.04h2.04V1.93H1.93Z'/%3e%3cpath%20fill='%23000'%20fill-rule='evenodd'%20d='M.5%201.4c0-.5.4-.9.9-.9h3.1a.9.9%200%200%201%20.87.67A2.44%202.44%200%200%201%209.5%202.95c0%20.65-.25%201.24-.67%201.68.39.1.67.46.67.88v3.08c0%20.5-.4.91-.9.91H1.4a.9.9%200%200%201-.9-.9V1.4Zm1.43.53v2.04h2.04V1.93H1.93Zm0%206.14V6.03h2.04v2.04H1.93Zm4.1%200V6.03h2.04v2.04H6.03Zm0-5.12a1.02%201.02%200%201%201%202.04%200%201.02%201.02%200%200%201-2.04%200Z'%20clip-rule='evenodd'/%3e%3cpath%20fill='%23FFD702'%20d='M7.05%201.93a1.02%201.02%200%201%200%200%202.04%201.02%201.02%200%200%200%200-2.04Z'/%3e%3c/svg%3e) Spaces](https://huggingface.co/spaces)

### Event Listeners[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#event-listeners)

#### Description

Event listeners allow you to respond to user interactions with the UI components you've defined in a Gradio Blocks app. When a user interacts with an element, such as changing a slider value or uploading an image, a function is called.

#### Supported Event Listeners

The DownloadButton component supports the following event listeners. Each event listener takes the same parameters, which are listed in the [Event Parameters](#event-listeners-arguments) table below.

Listener

Description

`DownloadButton.click(fn, ···)`

Triggered when the DownloadButton is clicked.

#### Event Parameters

Parameters ▼

[🔗](#param-event-fn)

    fn: Callable | None | Literal['decorator']

default `= "decorator"`

the function to call when this event is triggered. Often a machine learning model's prediction function. Each parameter of the function corresponds to one input component, and the function should return a single value or a tuple of values, with each element in the tuple corresponding to one output component.

[🔗](#param-event-inputs)

    inputs: Component | BlockContext | list[Component | BlockContext] | Set[Component | BlockContext] | None

default `= None`

List of gradio.components to use as inputs. If the function takes no inputs, this should be an empty list.

[🔗](#param-event-outputs)

    outputs: Component | BlockContext | list[Component | BlockContext] | Set[Component | BlockContext] | None

default `= None`

List of gradio.components to use as outputs. If the function returns no outputs, this should be an empty list.

[🔗](#param-event-api-name)

    api_name: str | None | Literal[False]

default `= None`

defines how the endpoint appears in the API docs. Can be a string, None, or False. If set to a string, the endpoint will be exposed in the API docs with the given name. If None (default), the name of the function will be used as the API endpoint. If False, the endpoint will not be exposed in the API docs and downstream apps (including those that \`gr.load\` this app) will not be able to use this event.

[🔗](#param-event-scroll-to-output)

    scroll_to_output: bool

default `= False`

If True, will scroll to output component on completion

[🔗](#param-event-show-progress)

    show_progress: Literal['full', 'minimal', 'hidden']

default `= "full"`

how to show the progress animation while event is running: "full" shows a spinner which covers the output component area as well as a runtime display in the upper right corner, "minimal" only shows the runtime display, "hidden" shows no progress animation at all

[🔗](#param-event-queue)

    queue: bool

default `= True`

If True, will place the request on the queue, if the queue has been enabled. If False, will not put this event on the queue, even if the queue has been enabled. If None, will use the queue setting of the gradio app.

[🔗](#param-event-batch)

    batch: bool

default `= False`

If True, then the function should process a batch of inputs, meaning that it should accept a list of input values for each parameter. The lists should be of equal length (and be up to length \`max\_batch\_size\`). The function is then \*required\* to return a tuple of lists (even if there is only 1 output component), with each list in the tuple corresponding to one output component.

[🔗](#param-event-max-batch-size)

    max_batch_size: int

default `= 4`

Maximum number of inputs to batch together if this is called from the queue (only relevant if batch=True)

[🔗](#param-event-preprocess)

    preprocess: bool

default `= True`

If False, will not run preprocessing of component data before running 'fn' (e.g. leaving it as a base64 string if this method is called with the \`Image\` component).

[🔗](#param-event-postprocess)

    postprocess: bool

default `= True`

If False, will not run postprocessing of component data before returning 'fn' output to the browser.

[🔗](#param-event-cancels)

    cancels: dict[str, Any] | list[dict[str, Any]] | None

default `= None`

A list of other events to cancel when this listener is triggered. For example, setting cancels=\[click\_event\] will cancel the click\_event, where click\_event is the return value of another components .click method. Functions that have not yet run (or generators that are iterating) will be cancelled, but functions that are currently running will be allowed to finish.

[🔗](#param-event-trigger-mode)

    trigger_mode: Literal['once', 'multiple', 'always_last'] | None

default `= None`

If "once" (default for all events except \`.change()\`) would not allow any submissions while an event is pending. If set to "multiple", unlimited submissions are allowed while pending, and "always\_last" (default for \`.change()\` and \`.key\_up()\` events) would allow a second submission after the pending event is complete.

[🔗](#param-event-js)

    js: str | None

default `= None`

Optional frontend js method to run before running 'fn'. Input arguments for js method are values of 'inputs' and 'outputs', return should be a list of values for output components.

[🔗](#param-event-concurrency-limit)

    concurrency_limit: int | None | Literal['default']

default `= "default"`

If set, this is the maximum number of this event that can be running simultaneously. Can be set to None to mean no concurrency\_limit (any number of this event can be running simultaneously). Set to "default" to use the default concurrency limit (defined by the \`default\_concurrency\_limit\` parameter in \`Blocks.queue()\`, which itself is 1 by default).

[🔗](#param-event-concurrency-id)

    concurrency_id: str | None

default `= None`

If set, this is the id of the concurrency group. Events with the same concurrency\_id will be limited by the lowest set concurrency\_limit.

[🔗](#param-event-show-api)

    show_api: bool

default `= True`

whether to show this event in the "view API" page of the Gradio app, or in the ".view\_api()" method of the Gradio clients. Unlike setting api\_name to False, setting show\_api to False will still allow downstream apps as well as the Clients to use this event. If fn is None, show\_api will automatically be set to False.

[🔗](#param-event-time-limit)

    time_limit: int | None

default `= None`

[🔗](#param-event-stream-every)

    stream_every: float

default `= 0.5`

[🔗](#param-event-like-user-message)

    like_user_message: bool

default `= False`

[

←

DateTime



](./datetime)[

Dropdown

→

](./dropdown)