New to Gradio? Start here: [Getting Started](/quickstart)

See the [Release History](/changelog)

To install Gradio from main, run the following command:

    pip install https://gradio-builds.s3.amazonaws.com/aa2eec284e58d7cb6359389176ddd005c5165c27/gradio-5.9.1-py3-none-any.whl

\*Note: Setting `share=True` in `launch()` will not work.

[

←

BarPlot



](./barplot)[

Chatbot

→

](./chatbot)

Button
======

    gradio.Button(···)

Run

[Built with Gradio ![logo](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='576'%20height='576'%20viewBox='0%200%20576%20576'%20fill='none'%3e%3cpath%20d='M287.5%20229L86%20344.5L287.5%20460L489%20344.5L287.5%20229Z'%20stroke='url(%23paint0_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M287.5%20116L86%20231.5L287.5%20347L489%20231.5L287.5%20116Z'%20stroke='url(%23paint1_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M86%20344L288%20229'%20stroke='url(%23paint2_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='bevel'/%3e%3cdefs%3e%3clinearGradient%20id='paint0_linear_102_7'%20x1='60'%20y1='341'%20x2='429.5'%20y2='344'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint1_linear_102_7'%20x1='513.5'%20y1='231'%20x2='143.5'%20y2='231'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint2_linear_102_7'%20x1='60'%20y1='344'%20x2='428.987'%20y2='341.811'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3c/defs%3e%3c/svg%3e)](https://gradio.app) 

### Description[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#description)

Creates a button that can be assigned arbitrary .click() events. The value (label) of the button can be used as an input to the function (rarely used) or set via the output of a function.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Behavior[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#behavior)

**As input component**: (Rarely used) the `str` corresponding to the button label when the button is clicked
------------------------------------------------------------------------------------------------------------

##### Your function should accept one of these types:

    def predict(
    	value: str | None
    )
    	...

  

**As output component**: string corresponding to the button label
-----------------------------------------------------------------

##### Your function should return one of these types:

    def predict(···) -> str | None
    	...	
    	return value

### Initialization[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#initialization)

Parameters ▼

    value: str | Callable

default `= "Run"`

default text for the button to display. If callable, the function will be called whenever the app loads to set the initial value of the component.

    every: Timer | float | None

default `= None`

continuously calls \`value\` to recalculate it if \`value\` is a function (has no effect otherwise). Can provide a Timer whose tick resets \`value\`, or a float that provides the regular interval for the reset Timer.

    inputs: Component | list[Component] | set[Component] | None

default `= None`

components that are used as inputs to calculate \`value\` if \`value\` is a function (has no effect otherwise). \`value\` is recalculated any time the inputs change.

    variant: Literal['primary', 'secondary', 'stop', 'huggingface']

default `= "secondary"`

sets the background and text color of the button. Use 'primary' for main call-to-action buttons, 'secondary' for a more subdued style, 'stop' for a stop button, 'huggingface' for a black background with white text, consistent with Hugging Face's button styles.

    size: Literal['sm', 'lg'] | None

default `= None`

size of the button. Can be "sm" or "lg".

    icon: str | None

default `= None`

URL or path to the icon file to display within the button. If None, no icon will be displayed.

    link: str | None

default `= None`

URL to open when the button is clicked. If None, no link will be used.

    visible: bool

default `= True`

if False, component will be hidden.

    interactive: bool

default `= True`

if False, the Button will be in a disabled state.

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

    scale: int | None

default `= None`

relative size compared to adjacent Components. For example if Components A and B are in a Row, and A has scale=2, and B has scale=1, A will be twice as wide as B. Should be an integer. scale applies in Rows, and to top-level Components in Blocks where fill\_height=True.

    min_width: int | None

default `= None`

minimum pixel width, will wrap if not sufficient screen space to satisfy this value. If a certain scale value results in this Component being narrower than min\_width, the min\_width parameter will be respected first.

### Shortcuts[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#shortcuts)

Class

Interface String Shortcut

Initialization

`gradio.Button`

"button"

Uses default values

`gradio.ClearButton`

"clearbutton"

Uses default values

`gradio.DuplicateButton`

"duplicatebutton"

Uses default values

`gradio.LoginButton`

"loginbutton"

Uses default values

### Event Listeners[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#event-listeners)

#### Description

Event listeners allow you to respond to user interactions with the UI components you've defined in a Gradio Blocks app. When a user interacts with an element, such as changing a slider value or uploading an image, a function is called.

#### Supported Event Listeners

The Button component supports the following event listeners. Each event listener takes the same parameters, which are listed in the [Event Parameters](#event-listeners-arguments) table below.

Listener

Description

`Button.click(fn, ···)`

Triggered when the Button is clicked.

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

BarPlot



](./barplot)[

Chatbot

→

](./chatbot)