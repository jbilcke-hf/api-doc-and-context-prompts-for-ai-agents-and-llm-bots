Plot
====

    gradio.Plot(···)

Plot

![undefined plot visualising provided data](data:image/png;base64,............;)

[Construit avec Gradio ![logo](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='576'%20height='576'%20viewBox='0%200%20576%20576'%20fill='none'%3e%3cpath%20d='M287.5%20229L86%20344.5L287.5%20460L489%20344.5L287.5%20229Z'%20stroke='url(%23paint0_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M287.5%20116L86%20231.5L287.5%20347L489%20231.5L287.5%20116Z'%20stroke='url(%23paint1_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M86%20344L288%20229'%20stroke='url(%23paint2_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='bevel'/%3e%3cdefs%3e%3clinearGradient%20id='paint0_linear_102_7'%20x1='60'%20y1='341'%20x2='429.5'%20y2='344'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint1_linear_102_7'%20x1='513.5'%20y1='231'%20x2='143.5'%20y2='231'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint2_linear_102_7'%20x1='60'%20y1='344'%20x2='428.987'%20y2='341.811'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3c/defs%3e%3c/svg%3e)](https://gradio.app) 

### Description[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#description)

Creates a plot component to display various kinds of plots (matplotlib, plotly, altair, or bokeh plots are supported). As this component does not accept user input, it is rarely used as an input component.  

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Behavior[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#behavior)

**As input component**: (Rarely used) passes the data displayed in the plot as an PlotData dataclass, which includes the plot information as a JSON string, as well as the type of chart and the plotting library.
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

##### Your function should accept one of these types:

    def predict(
    	value: PlotData | None
    )
    	...

  

**As output component**: Expects plot data in one of these formats: a matplotlib.Figure, bokeh.Model, plotly.Figure, or altair.Chart object.
--------------------------------------------------------------------------------------------------------------------------------------------

##### Your function should return one of these types:

    def predict(···) -> Any
    	...	
    	return value

### Initialization[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#initialization)

Parameters ▼

    value: Any | None

default `= None`

Optionally, supply a default plot object to display, must be a matplotlib, plotly, altair, or bokeh figure, or a callable. If callable, the function will be called whenever the app loads to set the initial value of the component.

    format: str

default `= "webp"`

File format in which to send matplotlib plots to the front end, such as 'jpg' or 'png'.

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

    container: bool

default `= True`

If True, will place the component in a container - providing some extra padding around the border.

    scale: int | None

default `= None`

relative size compared to adjacent Components. For example if Components A and B are in a Row, and A has scale=2, and B has scale=1, A will be twice as wide as B. Should be an integer. scale applies in Rows, and to top-level Components in Blocks where fill\_height=True.

    min_width: int

default `= 160`

minimum pixel width, will wrap if not sufficient screen space to satisfy this value. If a certain scale value results in this Component being narrower than min\_width, the min\_width parameter will be respected first.

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

`gradio.Plot`

"plot"

Uses default values

### Demos[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#demos)

blocks\_kinematicsstock\_forecast

Open in 🎢 ↗app.py

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

31

32

33

34

35

36

›

⌄

⌄

⌄

import pandas as pd

import numpy as np

  

import gradio as gr

  

def plot(v, a):

g \= 9.81

theta \= a / 180 \* 3.14

tmax \= ((2 \* v) \* np.sin(theta)) / g

timemat \= tmax \* np.linspace(0, 1, 40)

  

x \= (v \* timemat) \* np.cos(theta)

y \= ((v \* timemat) \* np.sin(theta)) \- ((0.5 \* g) \* (timemat\*\*2))

df \= pd.DataFrame({"x": x, "y": y})

return df

  

demo \= gr.Blocks()

  

with demo:

gr.Markdown(

r"Let's do some kinematics! Choose the speed and angle to see the trajectory. Remember that the range $R = v\_0^2 \\cdot \\frac{\\sin(2\\theta)}{g}$"

)

  

with gr.Row():

speed \= gr.Slider(1, 30, 25, label\="Speed")

angle \= gr.Slider(0, 90, 45, label\="Angle")

output \= gr.LinePlot(

x\="x",

y\="y",

overlay\_point\=True,

tooltip\=\["x", "y"\],

x\_lim\=\[0, 100\],

y\_lim\=\[0, 60\],

width\=350,

height\=300,

)

Let's do some kinematics! Choose the speed and angle to see the trajectory. Remember that the range $R = v\_0^2 \\cdot \\frac{\\sin(2\\theta)}{g}$

Speed

 ↺

1  30

Angle

 ↺

0  90

Textbox

Run

[Construit avec Gradio ![logo](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='576'%20height='576'%20viewBox='0%200%20576%20576'%20fill='none'%3e%3cpath%20d='M287.5%20229L86%20344.5L287.5%20460L489%20344.5L287.5%20229Z'%20stroke='url(%23paint0_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M287.5%20116L86%20231.5L287.5%20347L489%20231.5L287.5%20116Z'%20stroke='url(%23paint1_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M86%20344L288%20229'%20stroke='url(%23paint2_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='bevel'/%3e%3cdefs%3e%3clinearGradient%20id='paint0_linear_102_7'%20x1='60'%20y1='341'%20x2='429.5'%20y2='344'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint1_linear_102_7'%20x1='513.5'%20y1='231'%20x2='143.5'%20y2='231'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint2_linear_102_7'%20x1='60'%20y1='344'%20x2='428.987'%20y2='341.811'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3c/defs%3e%3c/svg%3e)](https://gradio.app) 

    import pandas as pd
    import numpy as np
    
    import gradio as gr
    
    def plot(v, a):
        g = 9.81
        theta = a / 180 * 3.14
        tmax = ((2 * v) * np.sin(theta)) / g
        timemat = tmax * np.linspace(0, 1, 40)
    
        x = (v * timemat) * np.cos(theta)
        y = ((v * timemat) * np.sin(theta)) - ((0.5 * g) * (timemat**2))
        df = pd.DataFrame({"x": x, "y": y})
        return df
    
    demo = gr.Blocks()
    
    with demo:
        gr.Markdown(
            r"Let's do some kinematics! Choose the speed and angle to see the trajectory. Remember that the range $R = v_0^2 \cdot \frac{\sin(2\theta)}{g}$"
        )
    
        with gr.Row():
            speed = gr.Slider(1, 30, 25, label="Speed")
            angle = gr.Slider(0, 90, 45, label="Angle")
        output = gr.LinePlot(
            x="x",
            y="y",
            overlay_point=True,
            tooltip=["x", "y"],
            x_lim=[0, 100],
            y_lim=[0, 60],
            width=350,
            height=300,
        )
        btn = gr.Button(value="Run")
        btn.click(plot, [speed, angle], output)
    
    if __name__ == "__main__":
        demo.launch()
    

Let's do some kinematics! Choose the speed and angle to see the trajectory. Remember that the range $R = v\_0^2 \\cdot \\frac{\\sin(2\\theta)}{g}$

Speed

 ↺

1  30

Angle

 ↺

0  90

Textbox

Run

[gradio/blocks\_kinematics](https://huggingface.co/spaces/gradio/blocks_kinematics) Construit avec [Gradio](https://gradio.app). Hosted on [![Hugging Face Space](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='10'%20height='10'%20fill='none'%3e%3cpath%20fill='%23FF3270'%20d='M1.93%206.03v2.04h2.04V6.03H1.93Z'/%3e%3cpath%20fill='%23861FFF'%20d='M6.03%206.03v2.04h2.04V6.03H6.03Z'/%3e%3cpath%20fill='%23097EFF'%20d='M1.93%201.93v2.04h2.04V1.93H1.93Z'/%3e%3cpath%20fill='%23000'%20fill-rule='evenodd'%20d='M.5%201.4c0-.5.4-.9.9-.9h3.1a.9.9%200%200%201%20.87.67A2.44%202.44%200%200%201%209.5%202.95c0%20.65-.25%201.24-.67%201.68.39.1.67.46.67.88v3.08c0%20.5-.4.91-.9.91H1.4a.9.9%200%200%201-.9-.9V1.4Zm1.43.53v2.04h2.04V1.93H1.93Zm0%206.14V6.03h2.04v2.04H1.93Zm4.1%200V6.03h2.04v2.04H6.03Zm0-5.12a1.02%201.02%200%201%201%202.04%200%201.02%201.02%200%200%201-2.04%200Z'%20clip-rule='evenodd'/%3e%3cpath%20fill='%23FFD702'%20d='M7.05%201.93a1.02%201.02%200%201%200%200%202.04%201.02%201.02%200%200%200%200-2.04Z'/%3e%3c/svg%3e) Spaces](https://huggingface.co/spaces)

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

31

32

33

34

35

›

⌄

⌄

⌄

⌄

⌄

import matplotlib.pyplot as plt

import numpy as np

  

import gradio as gr

  

def plot\_forecast(final\_year, companies, noise, show\_legend, point\_style):

start\_year \= 2020

x \= np.arange(start\_year, final\_year + 1)

year\_count \= x.shape\[0\]

plt\_format \= ({"cross": "X", "line": "-", "circle": "o--"})\[point\_style\]

fig \= plt.figure()

ax \= fig.add\_subplot(111)

for i, company in enumerate(companies):

series \= np.arange(0, year\_count, dtype\=float)

series \= series\*\*2 \* (i + 1)

series += np.random.rand(year\_count) \* noise

ax.plot(x, series, plt\_format)

if show\_legend:

plt.legend(companies)

return fig

  

demo \= gr.Interface(

plot\_forecast,

\[

gr.Radio(\[2025, 2030, 2035, 2040\], label\="Project to:"),

gr.CheckboxGroup(\["Google", "Microsoft", "Gradio"\], label\="Company Selection"),

gr.Slider(1, 100, label\="Noise Level"),

gr.Checkbox(label\="Show Legend"),

gr.Dropdown(\["cross", "line", "circle"\], label\="Style"),

\],

gr.Plot(label\="forecast", format\="png"),

)

  

if \_\_name\_\_ \== "\_\_main\_\_":

demo.launch()

Chargement...

    import matplotlib.pyplot as plt
    import numpy as np
    
    import gradio as gr
    
    def plot_forecast(final_year, companies, noise, show_legend, point_style):
        start_year = 2020
        x = np.arange(start_year, final_year + 1)
        year_count = x.shape[0]
        plt_format = ({"cross": "X", "line": "-", "circle": "o--"})[point_style]
        fig = plt.figure()
        ax = fig.add_subplot(111)
        for i, company in enumerate(companies):
            series = np.arange(0, year_count, dtype=float)
            series = series**2 * (i + 1)
            series += np.random.rand(year_count) * noise
            ax.plot(x, series, plt_format)
        if show_legend:
            plt.legend(companies)
        return fig
    
    demo = gr.Interface(
        plot_forecast,
        [
            gr.Radio([2025, 2030, 2035, 2040], label="Project to:"),
            gr.CheckboxGroup(["Google", "Microsoft", "Gradio"], label="Company Selection"),
            gr.Slider(1, 100, label="Noise Level"),
            gr.Checkbox(label="Show Legend"),
            gr.Dropdown(["cross", "line", "circle"], label="Style"),
        ],
        gr.Plot(label="forecast", format="png"),
    )
    
    if __name__ == "__main__":
        demo.launch()
    

Chargement...

[gradio/stock\_forecast](https://huggingface.co/spaces/gradio/stock_forecast) Construit avec [Gradio](https://gradio.app). Hosted on [![Hugging Face Space](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='10'%20height='10'%20fill='none'%3e%3cpath%20fill='%23FF3270'%20d='M1.93%206.03v2.04h2.04V6.03H1.93Z'/%3e%3cpath%20fill='%23861FFF'%20d='M6.03%206.03v2.04h2.04V6.03H6.03Z'/%3e%3cpath%20fill='%23097EFF'%20d='M1.93%201.93v2.04h2.04V1.93H1.93Z'/%3e%3cpath%20fill='%23000'%20fill-rule='evenodd'%20d='M.5%201.4c0-.5.4-.9.9-.9h3.1a.9.9%200%200%201%20.87.67A2.44%202.44%200%200%201%209.5%202.95c0%20.65-.25%201.24-.67%201.68.39.1.67.46.67.88v3.08c0%20.5-.4.91-.9.91H1.4a.9.9%200%200%201-.9-.9V1.4Zm1.43.53v2.04h2.04V1.93H1.93Zm0%206.14V6.03h2.04v2.04H1.93Zm4.1%200V6.03h2.04v2.04H6.03Zm0-5.12a1.02%201.02%200%201%201%202.04%200%201.02%201.02%200%200%201-2.04%200Z'%20clip-rule='evenodd'/%3e%3cpath%20fill='%23FFD702'%20d='M7.05%201.93a1.02%201.02%200%201%200%200%202.04%201.02%201.02%200%200%200%200-2.04Z'/%3e%3c/svg%3e) Spaces](https://huggingface.co/spaces)

### Event Listeners[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#event-listeners)

#### Description

Event listeners allow you to respond to user interactions with the UI components you've defined in a Gradio Blocks app. When a user interacts with an element, such as changing a slider value or uploading an image, a function is called.

#### Supported Event Listeners

The Plot component supports the following event listeners. Each event listener takes the same parameters, which are listed in the [Event Parameters](#event-listeners-arguments) table below.

Listener

Description

`Plot.change(fn, ···)`

Triggered when the value of the Plot changes either because of user input (e.g. a user types in a textbox) OR because of a function update (e.g. an image receives a value from the output of an event trigger). See `.input()` for a listener that is only triggered by user input.

`Plot.clear(fn, ···)`

This listener is triggered when the user clears the Plot using the clear button for the component.

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

Plot Component For Maps



](../../guides/plot-component-for-maps/)