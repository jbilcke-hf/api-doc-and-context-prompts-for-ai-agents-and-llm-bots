New to Gradio? Start here: [Getting Started](/quickstart)

See the [Release History](/changelog)

[

←

HighlightedText



](./highlightedtext)[

Image

→

](./image)

HTML
====

    gradio.HTML(···)

Loading Gradio wheels...

### Description[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#description)

Creates a component to display arbitrary HTML output. As this component does not accept user input, it is rarely used as an input component.  

-----------------------------------------------------------------------------------------------------------------------------------------------

### Behavior[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#behavior)

**As input component**: (Rarely used) passes the HTML as a `str`.
-----------------------------------------------------------------

##### Your function should accept one of these types:

    def predict(
    	value: str | None
    )
    	...

  

**As output component**: Expects a `str` consisting of valid HTML.
------------------------------------------------------------------

##### Your function should return one of these types:

    def predict(···) -> str | None
    	...	
    	return value

### Initialization[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#initialization)

Parameters ▼

    value: str | Callable | None

default `= None`

Default value. If callable, the function will be called whenever the app loads to set the initial value of the component.

    label: str | None

default `= None`

the label for this component. Is used as the header if there are a table of examples for this component. If None and used in a \`gr.Interface\`, the label will be the name of the parameter this component is assigned to.

    every: Timer | float | None

default `= None`

Continously calls \`value\` to recalculate it if \`value\` is a function (has no effect otherwise). Can provide a Timer whose tick resets \`value\`, or a float that provides the regular interval for the reset Timer.

    inputs: Component | list[Component] | set[Component] | None

default `= None`

Components that are used as inputs to calculate \`value\` if \`value\` is a function (has no effect otherwise). \`value\` is recalculated any time the inputs change.

    show_label: bool

default `= False`

If True, the label will be displayed. If False, the label will be hidden.

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

    min_height: int | None

default `= None`

The minimum height of the component, specified in pixels if a number is passed, or in CSS units if a string is passed. If HTML content exceeds the height, the component will expand to fit the content.

    max_height: int | None

default `= None`

The maximum height of the component, specified in pixels if a number is passed, or in CSS units if a string is passed. If content exceeds the height, the component will scroll.

    container: bool

default `= False`

If True, the HTML component will be displayed in a container. Default is False.

    padding: bool

default `= True`

If True, the HTML component will have a certain padding (set by the \`--block-padding\` CSS variable) in all directions. Default is True.

### Shortcuts[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#shortcuts)

Class

Interface String Shortcut

Initialization

`gradio.HTML`

"html"

Uses default values

### Demos[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#demos)

blocks\_scroll

Open in 🎢 ↗

app.py

Pyodide environment initialization is ongoing in another session...

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

›

⌄

⌄

import gradio as gr

  

demo \= gr.Blocks()

  

with demo:

inp \= gr.Textbox(placeholder\="Enter text.")

scroll\_btn \= gr.Button("Scroll")

no\_scroll\_btn \= gr.Button("No Scroll")

big\_block \= gr.HTML("""

<div style='height: 800px; width: 100px; background-color: pink;'></div>

""")

out \= gr.Textbox()

  

scroll\_btn.click(lambda x: x,

inputs\=inp,

outputs\=out,

scroll\_to\_output\=True)

no\_scroll\_btn.click(lambda x: x,

inputs\=inp,

outputs\=out)

  

if \_\_name\_\_ \== "\_\_main\_\_":

demo.launch()

    import gradio as gr
    
    demo = gr.Blocks()
    
    with demo:
        inp = gr.Textbox(placeholder="Enter text.")
        scroll_btn = gr.Button("Scroll")
        no_scroll_btn = gr.Button("No Scroll")
        big_block = gr.HTML("""
        
        """)
        out = gr.Textbox()
    
        scroll_btn.click(lambda x: x,
                   inputs=inp,
                   outputs=out,
                    scroll_to_output=True)
        no_scroll_btn.click(lambda x: x,
                   inputs=inp,
                   outputs=out)
    
    if __name__ == "__main__":
        demo.launch()
    

Loading...

[gradio/blocks\_scroll](https://huggingface.co/spaces/gradio/blocks_scroll) built with [Gradio](https://gradio.app). Hosted on [![Hugging Face Space](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='10'%20height='10'%20fill='none'%3e%3cpath%20fill='%23FF3270'%20d='M1.93%206.03v2.04h2.04V6.03H1.93Z'/%3e%3cpath%20fill='%23861FFF'%20d='M6.03%206.03v2.04h2.04V6.03H6.03Z'/%3e%3cpath%20fill='%23097EFF'%20d='M1.93%201.93v2.04h2.04V1.93H1.93Z'/%3e%3cpath%20fill='%23000'%20fill-rule='evenodd'%20d='M.5%201.4c0-.5.4-.9.9-.9h3.1a.9.9%200%200%201%20.87.67A2.44%202.44%200%200%201%209.5%202.95c0%20.65-.25%201.24-.67%201.68.39.1.67.46.67.88v3.08c0%20.5-.4.91-.9.91H1.4a.9.9%200%200%201-.9-.9V1.4Zm1.43.53v2.04h2.04V1.93H1.93Zm0%206.14V6.03h2.04v2.04H1.93Zm4.1%200V6.03h2.04v2.04H6.03Zm0-5.12a1.02%201.02%200%201%201%202.04%200%201.02%201.02%200%200%201-2.04%200Z'%20clip-rule='evenodd'/%3e%3cpath%20fill='%23FFD702'%20d='M7.05%201.93a1.02%201.02%200%201%200%200%202.04%201.02%201.02%200%200%200%200-2.04Z'/%3e%3c/svg%3e) Spaces](https://huggingface.co/spaces)

### Event Listeners[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#event-listeners)

#### Description

Event listeners allow you to respond to user interactions with the UI components you've defined in a Gradio Blocks app. When a user interacts with an element, such as changing a slider value or uploading an image, a function is called.

#### Supported Event Listeners

The HTML component supports the following event listeners. Each event listener takes the same parameters, which are listed in the [Event Parameters](#event-listeners-arguments) table below.

Listener

Description

`HTML.change(fn, ···)`

Triggered when the value of the HTML changes either because of user input (e.g. a user types in a textbox) OR because of a function update (e.g. an image receives a value from the output of an event trigger). See `.input()` for a listener that is only triggered by user input.

`HTML.click(fn, ···)`

Triggered when the HTML is clicked.

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

[

←

HighlightedText



](./highlightedtext)[

Image

→

](./image)