Model3D
=======

    gradio.Model3D(···)

3D Model

Drop File Here \- or - Click to Upload

[Built with Gradio ![logo](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='576'%20height='576'%20viewBox='0%200%20576%20576'%20fill='none'%3e%3cpath%20d='M287.5%20229L86%20344.5L287.5%20460L489%20344.5L287.5%20229Z'%20stroke='url(%23paint0_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M287.5%20116L86%20231.5L287.5%20347L489%20231.5L287.5%20116Z'%20stroke='url(%23paint1_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M86%20344L288%20229'%20stroke='url(%23paint2_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='bevel'/%3e%3cdefs%3e%3clinearGradient%20id='paint0_linear_102_7'%20x1='60'%20y1='341'%20x2='429.5'%20y2='344'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint1_linear_102_7'%20x1='513.5'%20y1='231'%20x2='143.5'%20y2='231'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint2_linear_102_7'%20x1='60'%20y1='344'%20x2='428.987'%20y2='341.811'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3c/defs%3e%3c/svg%3e)](https://gradio.app) ·  

Settings ![Settings](data:image/svg+xml,%3csvg%20width='24'%20height='24'%20viewBox='0%200%2024%2024'%20xmlns='http://www.w3.org/2000/svg'%3e%3c!--%20Outer%20gear%20teeth%20(gray)%20--%3e%3cpath%20d='M19.14%2012.94c.04-.3.06-.61.06-.94%200-.32-.02-.64-.07-.94l2.03-1.58c.18-.14.23-.41.12-.61l-1.92-3.32c-.12-.22-.37-.29-.59-.22l-2.39.96c-.5-.38-1.03-.7-1.62-.94l-.36-2.54c-.04-.24-.24-.41-.48-.41h-3.84c-.24%200-.43.17-.47.41l-.36%202.54c-.59.24-1.13.57-1.62.94l-2.39-.96c-.22-.08-.47%200-.59.22L2.74%208.87c-.12.21-.08.47.12.61l2.03%201.58c-.05.3-.07.62-.07.94s.02.64.07.94l-2.03%201.58c-.18.14-.23.41-.12.61l1.92%203.32c.12.22.37.29.59.22l2.39-.96c.5.38%201.03.7%201.62.94l.36%202.54c.05.24.24.41.48.41h3.84c.24%200%20.44-.17.47-.41l.36-2.54c.59-.24%201.13-.56%201.62-.94l2.39.96c.22.08.47%200%20.59-.22l1.92-3.32c.12-.22.07-.47-.12-.61l-2.01-1.58zM12%2015.6c-1.98%200-3.6-1.62-3.6-3.6s1.62-3.6%203.6-3.6%203.6%201.62%203.6%203.6-1.62%203.6-3.6%203.6z'%20fill='%23808080'/%3e%3c!--%20Inner%20circle%20(now%20gray)%20--%3e%3ccircle%20cx='12'%20cy='12'%20r='2.5'%20fill='%23808080'/%3e%3c/svg%3e) 

### Description[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#description)

Creates a component allows users to upload or view 3D Model files (.obj, .glb, .stl, .gltf, .splat, or .ply).  

----------------------------------------------------------------------------------------------------------------

### Behavior[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#behavior)

**As input component**: Passes the uploaded file as a `str` filepath to the function.
-------------------------------------------------------------------------------------

##### Your function should accept one of these types:

    def predict(
    	value: str | None
    )
    	...

  

**As output component**: Expects function to return a `str` or `pathlib.Path` filepath of type (.obj, .glb, .stl, or .gltf)
---------------------------------------------------------------------------------------------------------------------------

##### Your function should return one of these types:

    def predict(···) -> str | Path | None
    	...	
    	return value

### Initialization[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#initialization)

Parameters ▼

    value: str | Callable | None

default `= None`

path to (.obj, .glb, .stl, .gltf, .splat, or .ply) file to show in model3D viewer. If callable, the function will be called whenever the app loads to set the initial value of the component.

    display_mode: Literal['solid', 'point_cloud', 'wireframe'] | None

default `= None`

the display mode of the 3D model in the scene. Can be "solid" (which renders the model as a solid object), "point\_cloud", or "wireframe". For .splat, or .ply files, this parameter is ignored, as those files can only be rendered as solid objects.

    clear_color: tuple[float, float, float, float] | None

default `= None`

background color of scene, should be a tuple of 4 floats between 0 and 1 representing RGBA values.

    camera_position: tuple[int | float | None, int | float | None, int | float | None]

default `= (None, None, None)`

initial camera position of scene, provided as a tuple of \`(alpha, beta, radius)\`. Each value is optional. If provided, \`alpha\` and \`beta\` should be in degrees reflecting the angular position along the longitudinal and latitudinal axes, respectively. Radius corresponds to the distance from the center of the object to the camera.

    zoom_speed: float

default `= 1`

the speed of zooming in and out of the scene when the cursor wheel is rotated or when screen is pinched on a mobile device. Should be a positive float, increase this value to make zooming faster, decrease to make it slower. Affects the wheelPrecision property of the camera.

    pan_speed: float

default `= 1`

the speed of panning the scene when the cursor is dragged or when the screen is dragged on a mobile device. Should be a positive float, increase this value to make panning faster, decrease to make it slower. Affects the panSensibility property of the camera.

    height: int | str | None

default `= None`

The height of the model3D component, specified in pixels if a number is passed, or in CSS units if a string is passed.

    label: str | None

default `= None`

the label for this component. Appears above the component and is also used as the header if there are a table of examples for this component. If None and used in a \`gr.Interface\`, the label will be the name of the parameter this component is assigned to.

    show_label: bool | None

default `= None`

if True, will display label.

    every: Timer | float | None

default `= None`

Continously calls \`value\` to recalculate it if \`value\` is a function (has no effect otherwise). Can provide a Timer whose tick resets \`value\`, or a float that provides the regular interval for the reset Timer.

    inputs: Component | list[Component] | set[Component] | None

default `= None`

Components that are used as inputs to calculate \`value\` if \`value\` is a function (has no effect otherwise). \`value\` is recalculated any time the inputs change.

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

if True, will allow users to upload a file; if False, can only be used to display files. If not provided, this is inferred based on whether the component is used as an input or output.

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

### Shortcuts[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#shortcuts)

Class

Interface String Shortcut

Initialization

`gradio.Model3D`

"model3d"

Uses default values

### Event Listeners[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#event-listeners)

#### Description

Event listeners allow you to respond to user interactions with the UI components you've defined in a Gradio Blocks app. When a user interacts with an element, such as changing a slider value or uploading an image, a function is called.

#### Supported Event Listeners

The Model3D component supports the following event listeners. Each event listener takes the same parameters, which are listed in the [Event Parameters](#event-listeners-arguments) table below.

Listener

Description

`Model3D.change(fn, ···)`

Triggered when the value of the Model3D changes either because of user input (e.g. a user types in a textbox) OR because of a function update (e.g. an image receives a value from the output of an event trigger). See `.input()` for a listener that is only triggered by user input.

`Model3D.upload(fn, ···)`

This listener is triggered when the user uploads a file into the Model3D.

`Model3D.edit(fn, ···)`

This listener is triggered when the user edits the Model3D (e.g. image) using the built-in editor.

`Model3D.clear(fn, ···)`

This listener is triggered when the user clears the Model3D using the clear button for the component.

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

### Guides[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#guides)

[

How To Use 3D Model Component



](../../guides/how-to-use-3D-model-component/)