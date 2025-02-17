New to Gradio? Start here: [Getting Started](/quickstart)

See the [Release History](/changelog)

[

←

Chatbot



](./chatbot)[

CheckboxGroup

→

](./checkboxgroup)

Checkbox
========

    gradio.Checkbox(···)

 Checkbox

[Built with Gradio ![logo](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='576'%20height='576'%20viewBox='0%200%20576%20576'%20fill='none'%3e%3cpath%20d='M287.5%20229L86%20344.5L287.5%20460L489%20344.5L287.5%20229Z'%20stroke='url(%23paint0_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M287.5%20116L86%20231.5L287.5%20347L489%20231.5L287.5%20116Z'%20stroke='url(%23paint1_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M86%20344L288%20229'%20stroke='url(%23paint2_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='bevel'/%3e%3cdefs%3e%3clinearGradient%20id='paint0_linear_102_7'%20x1='60'%20y1='341'%20x2='429.5'%20y2='344'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint1_linear_102_7'%20x1='513.5'%20y1='231'%20x2='143.5'%20y2='231'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint2_linear_102_7'%20x1='60'%20y1='344'%20x2='428.987'%20y2='341.811'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3c/defs%3e%3c/svg%3e)](https://gradio.app) 

·

Settings ![Settings](data:image/svg+xml,%3csvg%20width='24'%20height='24'%20viewBox='0%200%2024%2024'%20xmlns='http://www.w3.org/2000/svg'%3e%3c!--%20Outer%20gear%20teeth%20(gray)%20--%3e%3cpath%20d='M19.14%2012.94c.04-.3.06-.61.06-.94%200-.32-.02-.64-.07-.94l2.03-1.58c.18-.14.23-.41.12-.61l-1.92-3.32c-.12-.22-.37-.29-.59-.22l-2.39.96c-.5-.38-1.03-.7-1.62-.94l-.36-2.54c-.04-.24-.24-.41-.48-.41h-3.84c-.24%200-.43.17-.47.41l-.36%202.54c-.59.24-1.13.57-1.62.94l-2.39-.96c-.22-.08-.47%200-.59.22L2.74%208.87c-.12.21-.08.47.12.61l2.03%201.58c-.05.3-.07.62-.07.94s.02.64.07.94l-2.03%201.58c-.18.14-.23.41-.12.61l1.92%203.32c.12.22.37.29.59.22l2.39-.96c.5.38%201.03.7%201.62.94l.36%202.54c.05.24.24.41.48.41h3.84c.24%200%20.44-.17.47-.41l.36-2.54c.59-.24%201.13-.56%201.62-.94l2.39.96c.22.08.47%200%20.59-.22l1.92-3.32c.12-.22.07-.47-.12-.61l-2.01-1.58zM12%2015.6c-1.98%200-3.6-1.62-3.6-3.6s1.62-3.6%203.6-3.6%203.6%201.62%203.6%203.6-1.62%203.6-3.6%203.6z'%20fill='%23808080'/%3e%3c!--%20Inner%20circle%20(now%20gray)%20--%3e%3ccircle%20cx='12'%20cy='12'%20r='2.5'%20fill='%23808080'/%3e%3c/svg%3e) 

### Description[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#description)

Creates a checkbox that can be set to `True` or `False`. Can be used as an input to pass a boolean value to a function or as an output to display a boolean value.  

---------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Behavior[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#behavior)

**As input component**: Passes the status of the checkbox as a `bool`.
----------------------------------------------------------------------

##### Your function should accept one of these types:

    def predict(
    	value: bool | None
    )
    	...

  

**As output component**: Expects a `bool` value that is set as the status of the checkbox
-----------------------------------------------------------------------------------------

##### Your function should return one of these types:

    def predict(···) -> bool | None
    	...	
    	return value

### Initialization[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#initialization)

Parameters ▼

[🔗](#param-checkbox-value)

    value: bool | Callable

default `= False`

if True, checked by default. If a function is provided, the function will be called each time the app loads to set the initial value of this component.

[🔗](#param-checkbox-label)

    label: str | None

default `= None`

the label for this component, displayed above the component if \`show\_label\` is \`True\` and is also used as the header if there are a table of examples for this component. If None and used in a \`gr.Interface\`, the label will be the name of the parameter this component corresponds to.

[🔗](#param-checkbox-info)

    info: str | None

default `= None`

additional component description, appears below the label in smaller font. Supports markdown / HTML syntax.

[🔗](#param-checkbox-every)

    every: Timer | float | None

default `= None`

Continously calls \`value\` to recalculate it if \`value\` is a function (has no effect otherwise). Can provide a Timer whose tick resets \`value\`, or a float that provides the regular interval for the reset Timer.

[🔗](#param-checkbox-inputs)

    inputs: Component | list[Component] | set[Component] | None

default `= None`

Components that are used as inputs to calculate \`value\` if \`value\` is a function (has no effect otherwise). \`value\` is recalculated any time the inputs change.

[🔗](#param-checkbox-show-label)

    show_label: bool | None

default `= None`

if True, will display label.

[🔗](#param-checkbox-container)

    container: bool

default `= True`

If True, will place the component in a container - providing some extra padding around the border.

[🔗](#param-checkbox-scale)

    scale: int | None

default `= None`

relative size compared to adjacent Components. For example if Components A and B are in a Row, and A has scale=2, and B has scale=1, A will be twice as wide as B. Should be an integer. scale applies in Rows, and to top-level Components in Blocks where fill\_height=True.

[🔗](#param-checkbox-min-width)

    min_width: int

default `= 160`

minimum pixel width, will wrap if not sufficient screen space to satisfy this value. If a certain scale value results in this Component being narrower than min\_width, the min\_width parameter will be respected first.

[🔗](#param-checkbox-interactive)

    interactive: bool | None

default `= None`

if True, this checkbox can be checked; if False, checking will be disabled. If not provided, this is inferred based on whether the component is used as an input or output.

[🔗](#param-checkbox-visible)

    visible: bool

default `= True`

If False, component will be hidden.

[🔗](#param-checkbox-elem-id)

    elem_id: str | None

default `= None`

An optional string that is assigned as the id of this component in the HTML DOM. Can be used for targeting CSS styles.

[🔗](#param-checkbox-elem-classes)

    elem_classes: list[str] | str | None

default `= None`

An optional list of strings that are assigned as the classes of this component in the HTML DOM. Can be used for targeting CSS styles.

[🔗](#param-checkbox-render)

    render: bool

default `= True`

If False, component will not render be rendered in the Blocks context. Should be used if the intention is to assign event listeners now but render the component later.

[🔗](#param-checkbox-key)

    key: int | str | None

default `= None`

if assigned, will be used to assume identity across a re-render. Components that have the same key across a re-render will have their value preserved.

### Shortcuts[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#shortcuts)

Class

Interface String Shortcut

Initialization

`gradio.Checkbox`

"checkbox"

Uses default values

### Demos[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#demos)

sentence\_builderhello\_world\_3

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

29

30

›

⌄

⌄

⌄

⌄

import gradio as gr

  

def sentence\_builder(quantity, animal, countries, place, activity\_list, morning):

return f"""The {quantity} {animal}s from {" and ".join(countries)} went to the {place} where they {" and ".join(activity\_list)} until the {"morning" if morning else "night"}"""

  

demo \= gr.Interface(

sentence\_builder,

\[

gr.Slider(2, 20, value\=4, label\="Count", info\="Choose between 2 and 20"),

gr.Dropdown(

\["cat", "dog", "bird"\], label\="Animal", info\="Will add more animals later!"

),

gr.CheckboxGroup(\["USA", "Japan", "Pakistan"\], label\="Countries", info\="Where are they from?"),

gr.Radio(\["park", "zoo", "road"\], label\="Location", info\="Where did they go?"),

gr.Dropdown(

\["ran", "swam", "ate", "slept"\], value\=\["swam", "slept"\], multiselect\=True, label\="Activity", info\="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed auctor, nisl eget ultricies aliquam, nunc nisl aliquet nunc, eget aliquam nisl nunc vel nisl."

),

gr.Checkbox(label\="Morning", info\="Did they do it in the morning?"),

\],

"text",

examples\=\[

\[2, "cat", \["Japan", "Pakistan"\], "park", \["ate", "swam"\], True\],

\[4, "dog", \["Japan"\], "zoo", \["ate", "swam"\], False\],

\[10, "bird", \["USA", "Pakistan"\], "road", \["ran"\], False\],

\[8, "cat", \["Pakistan"\], "zoo", \["ate"\], True\],

\]

)

  

if \_\_name\_\_ \== "\_\_main\_\_":

demo.launch()

Loading...

    import gradio as gr
    
    def sentence_builder(quantity, animal, countries, place, activity_list, morning):
        return f"""The {quantity} {animal}s from {" and ".join(countries)} went to the {place} where they {" and ".join(activity_list)} until the {"morning" if morning else "night"}"""
    
    demo = gr.Interface(
        sentence_builder,
        [
            gr.Slider(2, 20, value=4, label="Count", info="Choose between 2 and 20"),
            gr.Dropdown(
                ["cat", "dog", "bird"], label="Animal", info="Will add more animals later!"
            ),
            gr.CheckboxGroup(["USA", "Japan", "Pakistan"], label="Countries", info="Where are they from?"),
            gr.Radio(["park", "zoo", "road"], label="Location", info="Where did they go?"),
            gr.Dropdown(
                ["ran", "swam", "ate", "slept"], value=["swam", "slept"], multiselect=True, label="Activity", info="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed auctor, nisl eget ultricies aliquam, nunc nisl aliquet nunc, eget aliquam nisl nunc vel nisl."
            ),
            gr.Checkbox(label="Morning", info="Did they do it in the morning?"),
        ],
        "text",
        examples=[
            [2, "cat", ["Japan", "Pakistan"], "park", ["ate", "swam"], True],
            [4, "dog", ["Japan"], "zoo", ["ate", "swam"], False],
            [10, "bird", ["USA", "Pakistan"], "road", ["ran"], False],
            [8, "cat", ["Pakistan"], "zoo", ["ate"], True],
        ]
    )
    
    if __name__ == "__main__":
        demo.launch()
    

Loading...

[gradio/sentence\_builder](https://huggingface.co/spaces/gradio/sentence_builder) built with [Gradio](https://gradio.app). Hosted on [![Hugging Face Space](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='10'%20height='10'%20fill='none'%3e%3cpath%20fill='%23FF3270'%20d='M1.93%206.03v2.04h2.04V6.03H1.93Z'/%3e%3cpath%20fill='%23861FFF'%20d='M6.03%206.03v2.04h2.04V6.03H6.03Z'/%3e%3cpath%20fill='%23097EFF'%20d='M1.93%201.93v2.04h2.04V1.93H1.93Z'/%3e%3cpath%20fill='%23000'%20fill-rule='evenodd'%20d='M.5%201.4c0-.5.4-.9.9-.9h3.1a.9.9%200%200%201%20.87.67A2.44%202.44%200%200%201%209.5%202.95c0%20.65-.25%201.24-.67%201.68.39.1.67.46.67.88v3.08c0%20.5-.4.91-.9.91H1.4a.9.9%200%200%201-.9-.9V1.4Zm1.43.53v2.04h2.04V1.93H1.93Zm0%206.14V6.03h2.04v2.04H1.93Zm4.1%200V6.03h2.04v2.04H6.03Zm0-5.12a1.02%201.02%200%201%201%202.04%200%201.02%201.02%200%200%201-2.04%200Z'%20clip-rule='evenodd'/%3e%3cpath%20fill='%23FFD702'%20d='M7.05%201.93a1.02%201.02%200%201%200%200%202.04%201.02%201.02%200%200%200%200-2.04Z'/%3e%3c/svg%3e) Spaces](https://huggingface.co/spaces)

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

›

⌄

⌄

import gradio as gr

  

def greet(name, is\_morning, temperature):

salutation \= "Good morning" if is\_morning else "Good evening"

greeting \= f"{salutation} {name}. It is {temperature} degrees today"

celsius \= (temperature \- 32) \* 5 / 9

return greeting, round(celsius, 2)

  

demo \= gr.Interface(

fn\=greet,

inputs\=\["text", "checkbox", gr.Slider(0, 100)\],

outputs\=\["text", "number"\],

)

if \_\_name\_\_ \== "\_\_main\_\_":

demo.launch()

Loading...

    import gradio as gr
    
    def greet(name, is_morning, temperature):
        salutation = "Good morning" if is_morning else "Good evening"
        greeting = f"{salutation} {name}. It is {temperature} degrees today"
        celsius = (temperature - 32) * 5 / 9
        return greeting, round(celsius, 2)
    
    demo = gr.Interface(
        fn=greet,
        inputs=["text", "checkbox", gr.Slider(0, 100)],
        outputs=["text", "number"],
    )
    if __name__ == "__main__":
        demo.launch()
    

### Event Listeners[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#event-listeners)

#### Description

Event listeners allow you to respond to user interactions with the UI components you've defined in a Gradio Blocks app. When a user interacts with an element, such as changing a slider value or uploading an image, a function is called.

#### Supported Event Listeners

The Checkbox component supports the following event listeners. Each event listener takes the same parameters, which are listed in the [Event Parameters](#event-listeners-arguments) table below.

Listener

Description

`Checkbox.change(fn, ···)`

Triggered when the value of the Checkbox changes either because of user input (e.g. a user types in a textbox) OR because of a function update (e.g. an image receives a value from the output of an event trigger). See `.input()` for a listener that is only triggered by user input.

`Checkbox.input(fn, ···)`

This listener is triggered when the user changes the value of the Checkbox.

`Checkbox.select(fn, ···)`

Event listener for when the user selects or deselects the Checkbox. Uses event data gradio.SelectData to carry `value` referring to the label of the Checkbox, and `selected` to refer to state of the Checkbox. See EventData documentation on how to use this event data

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

Chatbot



](./chatbot)[

CheckboxGroup

→

](./checkboxgroup)