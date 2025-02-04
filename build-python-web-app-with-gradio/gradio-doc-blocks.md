Blocks
======

    with gradio.Blocks():

### Description[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#description)

Blocks is Gradio's low-level API that allows you to create more custom web applications and demos than Interfaces (yet still entirely in Python).  
  
Compared to the Interface class, Blocks offers more flexibility and control over: (1) the layout of components (2) the events that trigger the execution of functions (3) data flows (e.g. inputs can trigger outputs, which can trigger the next level of outputs). Blocks also offers ways to group together related demos such as with tabs.  
  
The basic usage of Blocks is as follows: create a Blocks object, then use it as a context (with the "with" statement), and then define layouts, components, or events within the Blocks context. Finally, call the launch() method to launch the demo.  

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Example Usage[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#example-usage)

    import gradio as gr
    def update(name):
        return f"Welcome to Gradio, {name}!"
    
    with gr.Blocks() as demo:
        gr.Markdown("Start typing below and then click **Run** to see the output.")
        with gr.Row():
            inp = gr.Textbox(placeholder="What is your name?")
            out = gr.Textbox()
        btn = gr.Button("Run")
        btn.click(fn=update, inputs=inp, outputs=out)
    
    demo.launch()

### Initialization[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#initialization)

Parameters ▼

    theme: Theme | str | None

default `= None`

A Theme object or a string representing a theme. If a string, will look for a built-in theme with that name (e.g. "soft" or "default"), or will attempt to load a theme from the Hugging Face Hub (e.g. "gradio/monochrome"). If None, will use the Default theme.

    analytics_enabled: bool | None

default `= None`

Whether to allow basic telemetry. If None, will use GRADIO\_ANALYTICS\_ENABLED environment variable or default to True.

    mode: str

default `= "blocks"`

A human-friendly name for the kind of Blocks or Interface being created. Used internally for analytics.

    title: str

default `= "Gradio"`

The tab title to display when this is opened in a browser window.

    css: str | None

default `= None`

Custom css as a code string. This css will be included in the demo webpage.

    css_paths: str | Path | list[str | Path] | None

default `= None`

Custom css as a pathlib.Path to a css file or a list of such paths. This css files will be read, concatenated, and included in the demo webpage. If the \`css\` parameter is also set, the css from \`css\` will be included first.

    js: str | None

default `= None`

Custom js as a code string. The custom js should be in the form of a single js function. This function will automatically be executed when the page loads. For more flexibility, use the head parameter to insert js inside <script> tags.

    head: str | None

default `= None`

Custom html code to insert into the head of the demo webpage. This can be used to add custom meta tags, multiple scripts, stylesheets, etc. to the page.

    head_paths: str | Path | list[str | Path] | None

default `= None`

Custom html code as a pathlib.Path to a html file or a list of such paths. This html files will be read, concatenated, and included in the head of the demo webpage. If the \`head\` parameter is also set, the html from \`head\` will be included first.

    fill_height: bool

default `= False`

Whether to vertically expand top-level child components to the height of the window. If True, expansion occurs when the scale value of the child components >= 1.

    fill_width: bool

default `= False`

Whether to horizontally expand to fill container fully. If False, centers and constrains app to a maximum width. Only applies if this is the outermost \`Blocks\` in your Gradio app.

    delete_cache: tuple[int, int] | None

default `= None`

A tuple corresponding \[frequency, age\] both expressed in number of seconds. Every \`frequency\` seconds, the temporary files created by this Blocks instance will be deleted if more than \`age\` seconds have passed since the file was created. For example, setting this to (86400, 86400) will delete temporary files every day. The cache will be deleted entirely when the server restarts. If None, no cache deletion will occur.

### Demos[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#demos)

blocks\_helloblocks\_flipperblocks\_kinematics

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

›

⌄

⌄

⌄

import gradio as gr

  

def welcome(name):

return f"Welcome to Gradio, {name}!"

  

with gr.Blocks() as demo:

gr.Markdown(

"""

\# Hello World!

Start typing below to see the output.

""")

inp \= gr.Textbox(placeholder\="What is your name?")

out \= gr.Textbox()

inp.change(welcome, inp, out)

  

if \_\_name\_\_ \== "\_\_main\_\_":

demo.launch()

Loading...

    import gradio as gr
    
    def welcome(name):
        return f"Welcome to Gradio, {name}!"
    
    with gr.Blocks() as demo:
        gr.Markdown(
        """
        # Hello World!
        Start typing below to see the output.
        """)
        inp = gr.Textbox(placeholder="What is your name?")
        out = gr.Textbox()
        inp.change(welcome, inp, out)
    
    if __name__ == "__main__":
        demo.launch()
    

Loading...

[gradio/blocks\_hello](https://huggingface.co/spaces/gradio/blocks_hello) built with [Gradio](https://gradio.app). Hosted on [![Hugging Face Space](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='10'%20height='10'%20fill='none'%3e%3cpath%20fill='%23FF3270'%20d='M1.93%206.03v2.04h2.04V6.03H1.93Z'/%3e%3cpath%20fill='%23861FFF'%20d='M6.03%206.03v2.04h2.04V6.03H6.03Z'/%3e%3cpath%20fill='%23097EFF'%20d='M1.93%201.93v2.04h2.04V1.93H1.93Z'/%3e%3cpath%20fill='%23000'%20fill-rule='evenodd'%20d='M.5%201.4c0-.5.4-.9.9-.9h3.1a.9.9%200%200%201%20.87.67A2.44%202.44%200%200%201%209.5%202.95c0%20.65-.25%201.24-.67%201.68.39.1.67.46.67.88v3.08c0%20.5-.4.91-.9.91H1.4a.9.9%200%200%201-.9-.9V1.4Zm1.43.53v2.04h2.04V1.93H1.93Zm0%206.14V6.03h2.04v2.04H1.93Zm4.1%200V6.03h2.04v2.04H6.03Zm0-5.12a1.02%201.02%200%201%201%202.04%200%201.02%201.02%200%200%201-2.04%200Z'%20clip-rule='evenodd'/%3e%3cpath%20fill='%23FFD702'%20d='M7.05%201.93a1.02%201.02%200%201%200%200%202.04%201.02%201.02%200%200%200%200-2.04Z'/%3e%3c/svg%3e) Spaces](https://huggingface.co/spaces)

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

36

›

⌄

⌄

⌄

⌄

⌄

⌄

⌄

⌄

import numpy as np

import gradio as gr

  

def flip\_text(x):

return x\[::\-1\]

  

def flip\_image(x):

return np.fliplr(x)

  

with gr.Blocks() as demo:

gr.Markdown("Flip text or image files using this demo.")

with gr.Tab("Flip Text"):

text\_input \= gr.Textbox()

text\_output \= gr.Textbox()

text\_button \= gr.Button("Flip")

with gr.Tab("Flip Image"):

with gr.Row():

image\_input \= gr.Image()

image\_output \= gr.Image()

image\_button \= gr.Button("Flip")

  

with gr.Accordion("Open for More!", open\=False):

gr.Markdown("Look at me...")

temp\_slider \= gr.Slider(

0, 1,

value\=0.1,

step\=0.1,

interactive\=True,

label\="Slide me",

)

  

text\_button.click(flip\_text, inputs\=text\_input, outputs\=text\_output)

image\_button.click(flip\_image, inputs\=image\_input, outputs\=image\_output)

  

if \_\_name\_\_ \== "\_\_main\_\_":

demo.launch()

Loading...

    import numpy as np
    import gradio as gr
    
    def flip_text(x):
        return x[::-1]
    
    def flip_image(x):
        return np.fliplr(x)
    
    with gr.Blocks() as demo:
        gr.Markdown("Flip text or image files using this demo.")
        with gr.Tab("Flip Text"):
            text_input = gr.Textbox()
            text_output = gr.Textbox()
            text_button = gr.Button("Flip")
        with gr.Tab("Flip Image"):
            with gr.Row():
                image_input = gr.Image()
                image_output = gr.Image()
            image_button = gr.Button("Flip")
    
        with gr.Accordion("Open for More!", open=False):
            gr.Markdown("Look at me...")
            temp_slider = gr.Slider(
                0, 1,
                value=0.1,
                step=0.1,
                interactive=True,
                label="Slide me",
            )
    
        text_button.click(flip_text, inputs=text_input, outputs=text_output)
        image_button.click(flip_image, inputs=image_input, outputs=image_output)
    
    if __name__ == "__main__":
        demo.launch()
    

Loading...

[gradio/blocks\_flipper](https://huggingface.co/spaces/gradio/blocks_flipper) built with [Gradio](https://gradio.app). Hosted on [![Hugging Face Space](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='10'%20height='10'%20fill='none'%3e%3cpath%20fill='%23FF3270'%20d='M1.93%206.03v2.04h2.04V6.03H1.93Z'/%3e%3cpath%20fill='%23861FFF'%20d='M6.03%206.03v2.04h2.04V6.03H6.03Z'/%3e%3cpath%20fill='%23097EFF'%20d='M1.93%201.93v2.04h2.04V1.93H1.93Z'/%3e%3cpath%20fill='%23000'%20fill-rule='evenodd'%20d='M.5%201.4c0-.5.4-.9.9-.9h3.1a.9.9%200%200%201%20.87.67A2.44%202.44%200%200%201%209.5%202.95c0%20.65-.25%201.24-.67%201.68.39.1.67.46.67.88v3.08c0%20.5-.4.91-.9.91H1.4a.9.9%200%200%201-.9-.9V1.4Zm1.43.53v2.04h2.04V1.93H1.93Zm0%206.14V6.03h2.04v2.04H1.93Zm4.1%200V6.03h2.04v2.04H6.03Zm0-5.12a1.02%201.02%200%201%201%202.04%200%201.02%201.02%200%200%201-2.04%200Z'%20clip-rule='evenodd'/%3e%3cpath%20fill='%23FFD702'%20d='M7.05%201.93a1.02%201.02%200%201%200%200%202.04%201.02%201.02%200%200%200%200-2.04Z'/%3e%3c/svg%3e) Spaces](https://huggingface.co/spaces)

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

Loading...

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
    

Loading...

[gradio/blocks\_kinematics](https://huggingface.co/spaces/gradio/blocks_kinematics) built with [Gradio](https://gradio.app). Hosted on [![Hugging Face Space](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='10'%20height='10'%20fill='none'%3e%3cpath%20fill='%23FF3270'%20d='M1.93%206.03v2.04h2.04V6.03H1.93Z'/%3e%3cpath%20fill='%23861FFF'%20d='M6.03%206.03v2.04h2.04V6.03H6.03Z'/%3e%3cpath%20fill='%23097EFF'%20d='M1.93%201.93v2.04h2.04V1.93H1.93Z'/%3e%3cpath%20fill='%23000'%20fill-rule='evenodd'%20d='M.5%201.4c0-.5.4-.9.9-.9h3.1a.9.9%200%200%201%20.87.67A2.44%202.44%200%200%201%209.5%202.95c0%20.65-.25%201.24-.67%201.68.39.1.67.46.67.88v3.08c0%20.5-.4.91-.9.91H1.4a.9.9%200%200%201-.9-.9V1.4Zm1.43.53v2.04h2.04V1.93H1.93Zm0%206.14V6.03h2.04v2.04H1.93Zm4.1%200V6.03h2.04v2.04H6.03Zm0-5.12a1.02%201.02%200%201%201%202.04%200%201.02%201.02%200%200%201-2.04%200Z'%20clip-rule='evenodd'/%3e%3cpath%20fill='%23FFD702'%20d='M7.05%201.93a1.02%201.02%200%201%200%200%202.04%201.02%201.02%200%200%200%200-2.04Z'/%3e%3c/svg%3e) Spaces](https://huggingface.co/spaces)

### Methods[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#methods)

### launch [![](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20fill='%23808080'%20viewBox='0%200%20640%20512'%3e%3c!--!%20Font%20Awesome%20Pro%206.0.0%20by%20@fontawesome%20-%20https://fontawesome.com%20License%20-%20https://fontawesome.com/license%20(Commercial%20License)%20Copyright%202022%20Fonticons,%20Inc.%20--%3e%3cpath%20d='M172.5%20131.1C228.1%2075.51%20320.5%2075.51%20376.1%20131.1C426.1%20181.1%20433.5%20260.8%20392.4%20318.3L391.3%20319.9C381%20334.2%20361%20337.6%20346.7%20327.3C332.3%20317%20328.9%20297%20339.2%20282.7L340.3%20281.1C363.2%20249%20359.6%20205.1%20331.7%20177.2C300.3%20145.8%20249.2%20145.8%20217.7%20177.2L105.5%20289.5C73.99%20320.1%2073.99%20372%20105.5%20403.5C133.3%20431.4%20177.3%20435%20209.3%20412.1L210.9%20410.1C225.3%20400.7%20245.3%20404%20255.5%20418.4C265.8%20432.8%20262.5%20452.8%20248.1%20463.1L246.5%20464.2C188.1%20505.3%20110.2%20498.7%2060.21%20448.8C3.741%20392.3%203.741%20300.7%2060.21%20244.3L172.5%20131.1zM467.5%20380C411%20436.5%20319.5%20436.5%20263%20380C213%20330%20206.5%20251.2%20247.6%20193.7L248.7%20192.1C258.1%20177.8%20278.1%20174.4%20293.3%20184.7C307.7%20194.1%20311.1%20214.1%20300.8%20229.3L299.7%20230.9C276.8%20262.1%20280.4%20306.9%20308.3%20334.8C339.7%20366.2%20390.8%20366.2%20422.3%20334.8L534.5%20222.5C566%20191%20566%20139.1%20534.5%20108.5C506.7%2080.63%20462.7%2076.99%20430.7%2099.9L429.1%20101C414.7%20111.3%20394.7%20107.1%20384.5%2093.58C374.2%2079.2%20377.5%2059.21%20391.9%2048.94L393.5%2047.82C451%206.731%20529.8%2013.25%20579.8%2063.24C636.3%20119.7%20636.3%20211.3%20579.8%20267.7L467.5%20380z'/%3e%3c/svg%3e)](#blocks-launch)

    gradio.Blocks.launch(···)

#### Description [![](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20fill='%23808080'%20viewBox='0%200%20640%20512'%3e%3c!--!%20Font%20Awesome%20Pro%206.0.0%20by%20@fontawesome%20-%20https://fontawesome.com%20License%20-%20https://fontawesome.com/license%20(Commercial%20License)%20Copyright%202022%20Fonticons,%20Inc.%20--%3e%3cpath%20d='M172.5%20131.1C228.1%2075.51%20320.5%2075.51%20376.1%20131.1C426.1%20181.1%20433.5%20260.8%20392.4%20318.3L391.3%20319.9C381%20334.2%20361%20337.6%20346.7%20327.3C332.3%20317%20328.9%20297%20339.2%20282.7L340.3%20281.1C363.2%20249%20359.6%20205.1%20331.7%20177.2C300.3%20145.8%20249.2%20145.8%20217.7%20177.2L105.5%20289.5C73.99%20320.1%2073.99%20372%20105.5%20403.5C133.3%20431.4%20177.3%20435%20209.3%20412.1L210.9%20410.1C225.3%20400.7%20245.3%20404%20255.5%20418.4C265.8%20432.8%20262.5%20452.8%20248.1%20463.1L246.5%20464.2C188.1%20505.3%20110.2%20498.7%2060.21%20448.8C3.741%20392.3%203.741%20300.7%2060.21%20244.3L172.5%20131.1zM467.5%20380C411%20436.5%20319.5%20436.5%20263%20380C213%20330%20206.5%20251.2%20247.6%20193.7L248.7%20192.1C258.1%20177.8%20278.1%20174.4%20293.3%20184.7C307.7%20194.1%20311.1%20214.1%20300.8%20229.3L299.7%20230.9C276.8%20262.1%20280.4%20306.9%20308.3%20334.8C339.7%20366.2%20390.8%20366.2%20422.3%20334.8L534.5%20222.5C566%20191%20566%20139.1%20534.5%20108.5C506.7%2080.63%20462.7%2076.99%20430.7%2099.9L429.1%20101C414.7%20111.3%20394.7%20107.1%20384.5%2093.58C374.2%2079.2%20377.5%2059.21%20391.9%2048.94L393.5%2047.82C451%206.731%20529.8%2013.25%20579.8%2063.24C636.3%20119.7%20636.3%20211.3%20579.8%20267.7L467.5%20380z'/%3e%3c/svg%3e)](#launch-description)

Launches a simple web server that serves the demo. Can also be used to create a public link used by anyone to access the demo from their browser by setting share=True.

#### Example Usage [![](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20fill='%23808080'%20viewBox='0%200%20640%20512'%3e%3c!--!%20Font%20Awesome%20Pro%206.0.0%20by%20@fontawesome%20-%20https://fontawesome.com%20License%20-%20https://fontawesome.com/license%20(Commercial%20License)%20Copyright%202022%20Fonticons,%20Inc.%20--%3e%3cpath%20d='M172.5%20131.1C228.1%2075.51%20320.5%2075.51%20376.1%20131.1C426.1%20181.1%20433.5%20260.8%20392.4%20318.3L391.3%20319.9C381%20334.2%20361%20337.6%20346.7%20327.3C332.3%20317%20328.9%20297%20339.2%20282.7L340.3%20281.1C363.2%20249%20359.6%20205.1%20331.7%20177.2C300.3%20145.8%20249.2%20145.8%20217.7%20177.2L105.5%20289.5C73.99%20320.1%2073.99%20372%20105.5%20403.5C133.3%20431.4%20177.3%20435%20209.3%20412.1L210.9%20410.1C225.3%20400.7%20245.3%20404%20255.5%20418.4C265.8%20432.8%20262.5%20452.8%20248.1%20463.1L246.5%20464.2C188.1%20505.3%20110.2%20498.7%2060.21%20448.8C3.741%20392.3%203.741%20300.7%2060.21%20244.3L172.5%20131.1zM467.5%20380C411%20436.5%20319.5%20436.5%20263%20380C213%20330%20206.5%20251.2%20247.6%20193.7L248.7%20192.1C258.1%20177.8%20278.1%20174.4%20293.3%20184.7C307.7%20194.1%20311.1%20214.1%20300.8%20229.3L299.7%20230.9C276.8%20262.1%20280.4%20306.9%20308.3%20334.8C339.7%20366.2%20390.8%20366.2%20422.3%20334.8L534.5%20222.5C566%20191%20566%20139.1%20534.5%20108.5C506.7%2080.63%20462.7%2076.99%20430.7%2099.9L429.1%20101C414.7%20111.3%20394.7%20107.1%20384.5%2093.58C374.2%2079.2%20377.5%2059.21%20391.9%2048.94L393.5%2047.82C451%206.731%20529.8%2013.25%20579.8%2063.24C636.3%20119.7%20636.3%20211.3%20579.8%20267.7L467.5%20380z'/%3e%3c/svg%3e)](#launch-example-usage)

    import gradio as gr
    def reverse(text):
        return text[::-1]
    with gr.Blocks() as demo:
        button = gr.Button(value="Reverse")
        button.click(reverse, gr.Textbox(), gr.Textbox())
    demo.launch(share=True, auth=("username", "password"))

Parameters ▼

    inline: bool | None

default `= None`

whether to display in the gradio app inline in an iframe. Defaults to True in python notebooks; False otherwise.

    inbrowser: bool

default `= False`

whether to automatically launch the gradio app in a new tab on the default browser.

    share: bool | None

default `= None`

whether to create a publicly shareable link for the gradio app. Creates an SSH tunnel to make your UI accessible from anywhere. If not provided, it is set to False by default every time, except when running in Google Colab. When localhost is not accessible (e.g. Google Colab), setting share=False is not supported. Can be set by environment variable GRADIO\_SHARE=True.

    debug: bool

default `= False`

if True, blocks the main thread from running. If running in Google Colab, this is needed to print the errors in the cell output.

    max_threads: int

default `= 40`

the maximum number of total threads that the Gradio app can generate in parallel. The default is inherited from the starlette library (currently 40).

    auth: Callable[[str, str], bool] | tuple[str, str] | list[tuple[str, str]] | None

default `= None`

If provided, username and password (or list of username-password tuples) required to access app. Can also provide function that takes username and password and returns True if valid login.

    auth_message: str | None

default `= None`

If provided, HTML message provided on login page.

    prevent_thread_lock: bool

default `= False`

By default, the gradio app blocks the main thread while the server is running. If set to True, the gradio app will not block and the gradio server will terminate as soon as the script finishes.

    show_error: bool

default `= False`

If True, any errors in the gradio app will be displayed in an alert modal and printed in the browser console log

    server_name: str | None

default `= None`

to make app accessible on local network, set this to "0.0.0.0". Can be set by environment variable GRADIO\_SERVER\_NAME. If None, will use "127.0.0.1".

    server_port: int | None

default `= None`

will start gradio app on this port (if available). Can be set by environment variable GRADIO\_SERVER\_PORT. If None, will search for an available port starting at 7860.

    height: int

default `= 500`

The height in pixels of the iframe element containing the gradio app (used if inline=True)

    width: int | str

default `= "100%"`

The width in pixels of the iframe element containing the gradio app (used if inline=True)

    favicon_path: str | None

default `= None`

If a path to a file (.png, .gif, or .ico) is provided, it will be used as the favicon for the web page.

    ssl_keyfile: str | None

default `= None`

If a path to a file is provided, will use this as the private key file to create a local server running on https.

    ssl_certfile: str | None

default `= None`

If a path to a file is provided, will use this as the signed certificate for https. Needs to be provided if ssl\_keyfile is provided.

    ssl_keyfile_password: str | None

default `= None`

If a password is provided, will use this with the ssl certificate for https.

    ssl_verify: bool

default `= True`

If False, skips certificate validation which allows self-signed certificates to be used.

    quiet: bool

default `= False`

If True, suppresses most print statements.

    show_api: bool

default `= True`

If True, shows the api docs in the footer of the app. Default True.

    allowed_paths: list[str] | None

default `= None`

List of complete filepaths or parent directories that gradio is allowed to serve. Must be absolute paths. Warning: if you provide directories, any files in these directories or their subdirectories are accessible to all users of your app. Can be set by comma separated environment variable GRADIO\_ALLOWED\_PATHS. These files are generally assumed to be secure and will be displayed in the browser when possible.

    blocked_paths: list[str] | None

default `= None`

List of complete filepaths or parent directories that gradio is not allowed to serve (i.e. users of your app are not allowed to access). Must be absolute paths. Warning: takes precedence over \`allowed\_paths\` and all other directories exposed by Gradio by default. Can be set by comma separated environment variable GRADIO\_BLOCKED\_PATHS.

    root_path: str | None

default `= None`

The root path (or "mount point") of the application, if it's not served from the root ("/") of the domain. Often used when the application is behind a reverse proxy that forwards requests to the application. For example, if the application is served at "https://example.com/myapp", the \`root\_path\` should be set to "/myapp". A full URL beginning with http:// or https:// can be provided, which will be used as the root path in its entirety. Can be set by environment variable GRADIO\_ROOT\_PATH. Defaults to "".

    app_kwargs: dict[str, Any] | None

default `= None`

Additional keyword arguments to pass to the underlying FastAPI app as a dictionary of parameter keys and argument values. For example, \`{"docs\_url": "/docs"}\`

    state_session_capacity: int

default `= 10000`

The maximum number of sessions whose information to store in memory. If the number of sessions exceeds this number, the oldest sessions will be removed. Reduce capacity to reduce memory usage when using gradio.State or returning updated components from functions. Defaults to 10000.

    share_server_address: str | None

default `= None`

Use this to specify a custom FRP server and port for sharing Gradio apps (only applies if share=True). If not provided, will use the default FRP server at https://gradio.live. See https://github.com/huggingface/frp for more information.

    share_server_protocol: Literal['http', 'https'] | None

default `= None`

Use this to specify the protocol to use for the share links. Defaults to "https", unless a custom share\_server\_address is provided, in which case it defaults to "http". If you are using a custom share\_server\_address and want to use https, you must set this to "https".

    auth_dependency: Callable[[fastapi.Request], str | None] | None

default `= None`

A function that takes a FastAPI request and returns a string user ID or None. If the function returns None for a specific request, that user is not authorized to access the app (they will see a 401 Unauthorized response). To be used with external authentication systems like OAuth. Cannot be used with \`auth\`.

    max_file_size: str | int | None

default `= None`

The maximum file size in bytes that can be uploaded. Can be a string of the form "<value><unit>", where value is any positive integer and unit is one of "b", "kb", "mb", "gb", "tb". If None, no limit is set.

    enable_monitoring: bool | None

default `= None`

Enables traffic monitoring of the app through the /monitoring endpoint. By default is None, which enables this endpoint. If explicitly True, will also print the monitoring URL to the console. If False, will disable monitoring altogether.

    strict_cors: bool

default `= True`

If True, prevents external domains from making requests to a Gradio server running on localhost. If False, allows requests to localhost that originate from localhost but also, crucially, from "null". This parameter should normally be True to prevent CSRF attacks but may need to be False when embedding a \*locally-running Gradio app\* using web components.

    node_server_name: str | None

default `= None`

    node_port: int | None

default `= None`

    ssr_mode: bool | None

default `= None`

If True, the Gradio app will be rendered using server-side rendering mode, which is typically more performant and provides better SEO, but this requires Node 20+ to be installed on the system. If False, the app will be rendered using client-side rendering mode. If None, will use GRADIO\_SSR\_MODE environment variable or default to False.

    pwa: bool | None

default `= None`

If True, the Gradio app will be set up as an installable PWA (Progressive Web App). If set to None (default behavior), then the PWA feature will be enabled if this Gradio app is launched on Spaces, but not otherwise.

### queue [![](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20fill='%23808080'%20viewBox='0%200%20640%20512'%3e%3c!--!%20Font%20Awesome%20Pro%206.0.0%20by%20@fontawesome%20-%20https://fontawesome.com%20License%20-%20https://fontawesome.com/license%20(Commercial%20License)%20Copyright%202022%20Fonticons,%20Inc.%20--%3e%3cpath%20d='M172.5%20131.1C228.1%2075.51%20320.5%2075.51%20376.1%20131.1C426.1%20181.1%20433.5%20260.8%20392.4%20318.3L391.3%20319.9C381%20334.2%20361%20337.6%20346.7%20327.3C332.3%20317%20328.9%20297%20339.2%20282.7L340.3%20281.1C363.2%20249%20359.6%20205.1%20331.7%20177.2C300.3%20145.8%20249.2%20145.8%20217.7%20177.2L105.5%20289.5C73.99%20320.1%2073.99%20372%20105.5%20403.5C133.3%20431.4%20177.3%20435%20209.3%20412.1L210.9%20410.1C225.3%20400.7%20245.3%20404%20255.5%20418.4C265.8%20432.8%20262.5%20452.8%20248.1%20463.1L246.5%20464.2C188.1%20505.3%20110.2%20498.7%2060.21%20448.8C3.741%20392.3%203.741%20300.7%2060.21%20244.3L172.5%20131.1zM467.5%20380C411%20436.5%20319.5%20436.5%20263%20380C213%20330%20206.5%20251.2%20247.6%20193.7L248.7%20192.1C258.1%20177.8%20278.1%20174.4%20293.3%20184.7C307.7%20194.1%20311.1%20214.1%20300.8%20229.3L299.7%20230.9C276.8%20262.1%20280.4%20306.9%20308.3%20334.8C339.7%20366.2%20390.8%20366.2%20422.3%20334.8L534.5%20222.5C566%20191%20566%20139.1%20534.5%20108.5C506.7%2080.63%20462.7%2076.99%20430.7%2099.9L429.1%20101C414.7%20111.3%20394.7%20107.1%20384.5%2093.58C374.2%2079.2%20377.5%2059.21%20391.9%2048.94L393.5%2047.82C451%206.731%20529.8%2013.25%20579.8%2063.24C636.3%20119.7%20636.3%20211.3%20579.8%20267.7L467.5%20380z'/%3e%3c/svg%3e)](#blocks-queue)

    gradio.Blocks.queue(···)

#### Description [![](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20fill='%23808080'%20viewBox='0%200%20640%20512'%3e%3c!--!%20Font%20Awesome%20Pro%206.0.0%20by%20@fontawesome%20-%20https://fontawesome.com%20License%20-%20https://fontawesome.com/license%20(Commercial%20License)%20Copyright%202022%20Fonticons,%20Inc.%20--%3e%3cpath%20d='M172.5%20131.1C228.1%2075.51%20320.5%2075.51%20376.1%20131.1C426.1%20181.1%20433.5%20260.8%20392.4%20318.3L391.3%20319.9C381%20334.2%20361%20337.6%20346.7%20327.3C332.3%20317%20328.9%20297%20339.2%20282.7L340.3%20281.1C363.2%20249%20359.6%20205.1%20331.7%20177.2C300.3%20145.8%20249.2%20145.8%20217.7%20177.2L105.5%20289.5C73.99%20320.1%2073.99%20372%20105.5%20403.5C133.3%20431.4%20177.3%20435%20209.3%20412.1L210.9%20410.1C225.3%20400.7%20245.3%20404%20255.5%20418.4C265.8%20432.8%20262.5%20452.8%20248.1%20463.1L246.5%20464.2C188.1%20505.3%20110.2%20498.7%2060.21%20448.8C3.741%20392.3%203.741%20300.7%2060.21%20244.3L172.5%20131.1zM467.5%20380C411%20436.5%20319.5%20436.5%20263%20380C213%20330%20206.5%20251.2%20247.6%20193.7L248.7%20192.1C258.1%20177.8%20278.1%20174.4%20293.3%20184.7C307.7%20194.1%20311.1%20214.1%20300.8%20229.3L299.7%20230.9C276.8%20262.1%20280.4%20306.9%20308.3%20334.8C339.7%20366.2%20390.8%20366.2%20422.3%20334.8L534.5%20222.5C566%20191%20566%20139.1%20534.5%20108.5C506.7%2080.63%20462.7%2076.99%20430.7%2099.9L429.1%20101C414.7%20111.3%20394.7%20107.1%20384.5%2093.58C374.2%2079.2%20377.5%2059.21%20391.9%2048.94L393.5%2047.82C451%206.731%20529.8%2013.25%20579.8%2063.24C636.3%20119.7%20636.3%20211.3%20579.8%20267.7L467.5%20380z'/%3e%3c/svg%3e)](#queue-description)

By enabling the queue you can control when users know their position in the queue, and set a limit on maximum number of events allowed.

#### Example Usage [![](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20fill='%23808080'%20viewBox='0%200%20640%20512'%3e%3c!--!%20Font%20Awesome%20Pro%206.0.0%20by%20@fontawesome%20-%20https://fontawesome.com%20License%20-%20https://fontawesome.com/license%20(Commercial%20License)%20Copyright%202022%20Fonticons,%20Inc.%20--%3e%3cpath%20d='M172.5%20131.1C228.1%2075.51%20320.5%2075.51%20376.1%20131.1C426.1%20181.1%20433.5%20260.8%20392.4%20318.3L391.3%20319.9C381%20334.2%20361%20337.6%20346.7%20327.3C332.3%20317%20328.9%20297%20339.2%20282.7L340.3%20281.1C363.2%20249%20359.6%20205.1%20331.7%20177.2C300.3%20145.8%20249.2%20145.8%20217.7%20177.2L105.5%20289.5C73.99%20320.1%2073.99%20372%20105.5%20403.5C133.3%20431.4%20177.3%20435%20209.3%20412.1L210.9%20410.1C225.3%20400.7%20245.3%20404%20255.5%20418.4C265.8%20432.8%20262.5%20452.8%20248.1%20463.1L246.5%20464.2C188.1%20505.3%20110.2%20498.7%2060.21%20448.8C3.741%20392.3%203.741%20300.7%2060.21%20244.3L172.5%20131.1zM467.5%20380C411%20436.5%20319.5%20436.5%20263%20380C213%20330%20206.5%20251.2%20247.6%20193.7L248.7%20192.1C258.1%20177.8%20278.1%20174.4%20293.3%20184.7C307.7%20194.1%20311.1%20214.1%20300.8%20229.3L299.7%20230.9C276.8%20262.1%20280.4%20306.9%20308.3%20334.8C339.7%20366.2%20390.8%20366.2%20422.3%20334.8L534.5%20222.5C566%20191%20566%20139.1%20534.5%20108.5C506.7%2080.63%20462.7%2076.99%20430.7%2099.9L429.1%20101C414.7%20111.3%20394.7%20107.1%20384.5%2093.58C374.2%2079.2%20377.5%2059.21%20391.9%2048.94L393.5%2047.82C451%206.731%20529.8%2013.25%20579.8%2063.24C636.3%20119.7%20636.3%20211.3%20579.8%20267.7L467.5%20380z'/%3e%3c/svg%3e)](#queue-example-usage)

    with gr.Blocks() as demo:
        button = gr.Button(label="Generate Image")
        button.click(fn=image_generator, inputs=gr.Textbox(), outputs=gr.Image())
    demo.queue(max_size=10)
    demo.launch()

Parameters ▼

    status_update_rate: float | Literal['auto']

default `= "auto"`

If "auto", Queue will send status estimations to all clients whenever a job is finished. Otherwise Queue will send status at regular intervals set by this parameter as the number of seconds.

    api_open: bool | None

default `= None`

If True, the REST routes of the backend will be open, allowing requests made directly to those endpoints to skip the queue.

    max_size: int | None

default `= None`

The maximum number of events the queue will store at any given moment. If the queue is full, new events will not be added and a user will receive a message saying that the queue is full. If None, the queue size will be unlimited.

    default_concurrency_limit: int | None | Literal['not_set']

default `= "not_set"`

The default value of \`concurrency\_limit\` to use for event listeners that don't specify a value. Can be set by environment variable GRADIO\_DEFAULT\_CONCURRENCY\_LIMIT. Defaults to 1 if not set otherwise.

### integrate [![](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20fill='%23808080'%20viewBox='0%200%20640%20512'%3e%3c!--!%20Font%20Awesome%20Pro%206.0.0%20by%20@fontawesome%20-%20https://fontawesome.com%20License%20-%20https://fontawesome.com/license%20(Commercial%20License)%20Copyright%202022%20Fonticons,%20Inc.%20--%3e%3cpath%20d='M172.5%20131.1C228.1%2075.51%20320.5%2075.51%20376.1%20131.1C426.1%20181.1%20433.5%20260.8%20392.4%20318.3L391.3%20319.9C381%20334.2%20361%20337.6%20346.7%20327.3C332.3%20317%20328.9%20297%20339.2%20282.7L340.3%20281.1C363.2%20249%20359.6%20205.1%20331.7%20177.2C300.3%20145.8%20249.2%20145.8%20217.7%20177.2L105.5%20289.5C73.99%20320.1%2073.99%20372%20105.5%20403.5C133.3%20431.4%20177.3%20435%20209.3%20412.1L210.9%20410.1C225.3%20400.7%20245.3%20404%20255.5%20418.4C265.8%20432.8%20262.5%20452.8%20248.1%20463.1L246.5%20464.2C188.1%20505.3%20110.2%20498.7%2060.21%20448.8C3.741%20392.3%203.741%20300.7%2060.21%20244.3L172.5%20131.1zM467.5%20380C411%20436.5%20319.5%20436.5%20263%20380C213%20330%20206.5%20251.2%20247.6%20193.7L248.7%20192.1C258.1%20177.8%20278.1%20174.4%20293.3%20184.7C307.7%20194.1%20311.1%20214.1%20300.8%20229.3L299.7%20230.9C276.8%20262.1%20280.4%20306.9%20308.3%20334.8C339.7%20366.2%20390.8%20366.2%20422.3%20334.8L534.5%20222.5C566%20191%20566%20139.1%20534.5%20108.5C506.7%2080.63%20462.7%2076.99%20430.7%2099.9L429.1%20101C414.7%20111.3%20394.7%20107.1%20384.5%2093.58C374.2%2079.2%20377.5%2059.21%20391.9%2048.94L393.5%2047.82C451%206.731%20529.8%2013.25%20579.8%2063.24C636.3%20119.7%20636.3%20211.3%20579.8%20267.7L467.5%20380z'/%3e%3c/svg%3e)](#blocks-integrate)

    gradio.Blocks.integrate(···)

#### Description [![](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20fill='%23808080'%20viewBox='0%200%20640%20512'%3e%3c!--!%20Font%20Awesome%20Pro%206.0.0%20by%20@fontawesome%20-%20https://fontawesome.com%20License%20-%20https://fontawesome.com/license%20(Commercial%20License)%20Copyright%202022%20Fonticons,%20Inc.%20--%3e%3cpath%20d='M172.5%20131.1C228.1%2075.51%20320.5%2075.51%20376.1%20131.1C426.1%20181.1%20433.5%20260.8%20392.4%20318.3L391.3%20319.9C381%20334.2%20361%20337.6%20346.7%20327.3C332.3%20317%20328.9%20297%20339.2%20282.7L340.3%20281.1C363.2%20249%20359.6%20205.1%20331.7%20177.2C300.3%20145.8%20249.2%20145.8%20217.7%20177.2L105.5%20289.5C73.99%20320.1%2073.99%20372%20105.5%20403.5C133.3%20431.4%20177.3%20435%20209.3%20412.1L210.9%20410.1C225.3%20400.7%20245.3%20404%20255.5%20418.4C265.8%20432.8%20262.5%20452.8%20248.1%20463.1L246.5%20464.2C188.1%20505.3%20110.2%20498.7%2060.21%20448.8C3.741%20392.3%203.741%20300.7%2060.21%20244.3L172.5%20131.1zM467.5%20380C411%20436.5%20319.5%20436.5%20263%20380C213%20330%20206.5%20251.2%20247.6%20193.7L248.7%20192.1C258.1%20177.8%20278.1%20174.4%20293.3%20184.7C307.7%20194.1%20311.1%20214.1%20300.8%20229.3L299.7%20230.9C276.8%20262.1%20280.4%20306.9%20308.3%20334.8C339.7%20366.2%20390.8%20366.2%20422.3%20334.8L534.5%20222.5C566%20191%20566%20139.1%20534.5%20108.5C506.7%2080.63%20462.7%2076.99%20430.7%2099.9L429.1%20101C414.7%20111.3%20394.7%20107.1%20384.5%2093.58C374.2%2079.2%20377.5%2059.21%20391.9%2048.94L393.5%2047.82C451%206.731%20529.8%2013.25%20579.8%2063.24C636.3%20119.7%20636.3%20211.3%20579.8%20267.7L467.5%20380z'/%3e%3c/svg%3e)](#integrate-description)

A catch-all method for integrating with other libraries. This method should be run after launch()

Parameters ▼

    comet_ml: <class 'inspect._empty'>

default `= None`

If a comet\_ml Experiment object is provided, will integrate with the experiment and appear on Comet dashboard

    wandb: ModuleType | None

default `= None`

If the wandb module is provided, will integrate with it and appear on WandB dashboard

    mlflow: ModuleType | None

default `= None`

If the mlflow module is provided, will integrate with the experiment and appear on ML Flow dashboard

### load [![](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20fill='%23808080'%20viewBox='0%200%20640%20512'%3e%3c!--!%20Font%20Awesome%20Pro%206.0.0%20by%20@fontawesome%20-%20https://fontawesome.com%20License%20-%20https://fontawesome.com/license%20(Commercial%20License)%20Copyright%202022%20Fonticons,%20Inc.%20--%3e%3cpath%20d='M172.5%20131.1C228.1%2075.51%20320.5%2075.51%20376.1%20131.1C426.1%20181.1%20433.5%20260.8%20392.4%20318.3L391.3%20319.9C381%20334.2%20361%20337.6%20346.7%20327.3C332.3%20317%20328.9%20297%20339.2%20282.7L340.3%20281.1C363.2%20249%20359.6%20205.1%20331.7%20177.2C300.3%20145.8%20249.2%20145.8%20217.7%20177.2L105.5%20289.5C73.99%20320.1%2073.99%20372%20105.5%20403.5C133.3%20431.4%20177.3%20435%20209.3%20412.1L210.9%20410.1C225.3%20400.7%20245.3%20404%20255.5%20418.4C265.8%20432.8%20262.5%20452.8%20248.1%20463.1L246.5%20464.2C188.1%20505.3%20110.2%20498.7%2060.21%20448.8C3.741%20392.3%203.741%20300.7%2060.21%20244.3L172.5%20131.1zM467.5%20380C411%20436.5%20319.5%20436.5%20263%20380C213%20330%20206.5%20251.2%20247.6%20193.7L248.7%20192.1C258.1%20177.8%20278.1%20174.4%20293.3%20184.7C307.7%20194.1%20311.1%20214.1%20300.8%20229.3L299.7%20230.9C276.8%20262.1%20280.4%20306.9%20308.3%20334.8C339.7%20366.2%20390.8%20366.2%20422.3%20334.8L534.5%20222.5C566%20191%20566%20139.1%20534.5%20108.5C506.7%2080.63%20462.7%2076.99%20430.7%2099.9L429.1%20101C414.7%20111.3%20394.7%20107.1%20384.5%2093.58C374.2%2079.2%20377.5%2059.21%20391.9%2048.94L393.5%2047.82C451%206.731%20529.8%2013.25%20579.8%2063.24C636.3%20119.7%20636.3%20211.3%20579.8%20267.7L467.5%20380z'/%3e%3c/svg%3e)](#blocks-load)

    gradio.Blocks.load(block, ···)

#### Description [![](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20fill='%23808080'%20viewBox='0%200%20640%20512'%3e%3c!--!%20Font%20Awesome%20Pro%206.0.0%20by%20@fontawesome%20-%20https://fontawesome.com%20License%20-%20https://fontawesome.com/license%20(Commercial%20License)%20Copyright%202022%20Fonticons,%20Inc.%20--%3e%3cpath%20d='M172.5%20131.1C228.1%2075.51%20320.5%2075.51%20376.1%20131.1C426.1%20181.1%20433.5%20260.8%20392.4%20318.3L391.3%20319.9C381%20334.2%20361%20337.6%20346.7%20327.3C332.3%20317%20328.9%20297%20339.2%20282.7L340.3%20281.1C363.2%20249%20359.6%20205.1%20331.7%20177.2C300.3%20145.8%20249.2%20145.8%20217.7%20177.2L105.5%20289.5C73.99%20320.1%2073.99%20372%20105.5%20403.5C133.3%20431.4%20177.3%20435%20209.3%20412.1L210.9%20410.1C225.3%20400.7%20245.3%20404%20255.5%20418.4C265.8%20432.8%20262.5%20452.8%20248.1%20463.1L246.5%20464.2C188.1%20505.3%20110.2%20498.7%2060.21%20448.8C3.741%20392.3%203.741%20300.7%2060.21%20244.3L172.5%20131.1zM467.5%20380C411%20436.5%20319.5%20436.5%20263%20380C213%20330%20206.5%20251.2%20247.6%20193.7L248.7%20192.1C258.1%20177.8%20278.1%20174.4%20293.3%20184.7C307.7%20194.1%20311.1%20214.1%20300.8%20229.3L299.7%20230.9C276.8%20262.1%20280.4%20306.9%20308.3%20334.8C339.7%20366.2%20390.8%20366.2%20422.3%20334.8L534.5%20222.5C566%20191%20566%20139.1%20534.5%20108.5C506.7%2080.63%20462.7%2076.99%20430.7%2099.9L429.1%20101C414.7%20111.3%20394.7%20107.1%20384.5%2093.58C374.2%2079.2%20377.5%2059.21%20391.9%2048.94L393.5%2047.82C451%206.731%20529.8%2013.25%20579.8%2063.24C636.3%20119.7%20636.3%20211.3%20579.8%20267.7L467.5%20380z'/%3e%3c/svg%3e)](#load-description)

This listener is triggered when the Blocks initially loads in the browser.

Parameters ▼

    block: Block | None

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

### unload [![](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20fill='%23808080'%20viewBox='0%200%20640%20512'%3e%3c!--!%20Font%20Awesome%20Pro%206.0.0%20by%20@fontawesome%20-%20https://fontawesome.com%20License%20-%20https://fontawesome.com/license%20(Commercial%20License)%20Copyright%202022%20Fonticons,%20Inc.%20--%3e%3cpath%20d='M172.5%20131.1C228.1%2075.51%20320.5%2075.51%20376.1%20131.1C426.1%20181.1%20433.5%20260.8%20392.4%20318.3L391.3%20319.9C381%20334.2%20361%20337.6%20346.7%20327.3C332.3%20317%20328.9%20297%20339.2%20282.7L340.3%20281.1C363.2%20249%20359.6%20205.1%20331.7%20177.2C300.3%20145.8%20249.2%20145.8%20217.7%20177.2L105.5%20289.5C73.99%20320.1%2073.99%20372%20105.5%20403.5C133.3%20431.4%20177.3%20435%20209.3%20412.1L210.9%20410.1C225.3%20400.7%20245.3%20404%20255.5%20418.4C265.8%20432.8%20262.5%20452.8%20248.1%20463.1L246.5%20464.2C188.1%20505.3%20110.2%20498.7%2060.21%20448.8C3.741%20392.3%203.741%20300.7%2060.21%20244.3L172.5%20131.1zM467.5%20380C411%20436.5%20319.5%20436.5%20263%20380C213%20330%20206.5%20251.2%20247.6%20193.7L248.7%20192.1C258.1%20177.8%20278.1%20174.4%20293.3%20184.7C307.7%20194.1%20311.1%20214.1%20300.8%20229.3L299.7%20230.9C276.8%20262.1%20280.4%20306.9%20308.3%20334.8C339.7%20366.2%20390.8%20366.2%20422.3%20334.8L534.5%20222.5C566%20191%20566%20139.1%20534.5%20108.5C506.7%2080.63%20462.7%2076.99%20430.7%2099.9L429.1%20101C414.7%20111.3%20394.7%20107.1%20384.5%2093.58C374.2%2079.2%20377.5%2059.21%20391.9%2048.94L393.5%2047.82C451%206.731%20529.8%2013.25%20579.8%2063.24C636.3%20119.7%20636.3%20211.3%20579.8%20267.7L467.5%20380z'/%3e%3c/svg%3e)](#blocks-unload)

    gradio.Blocks.unload(fn, ···)

#### Description [![](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20fill='%23808080'%20viewBox='0%200%20640%20512'%3e%3c!--!%20Font%20Awesome%20Pro%206.0.0%20by%20@fontawesome%20-%20https://fontawesome.com%20License%20-%20https://fontawesome.com/license%20(Commercial%20License)%20Copyright%202022%20Fonticons,%20Inc.%20--%3e%3cpath%20d='M172.5%20131.1C228.1%2075.51%20320.5%2075.51%20376.1%20131.1C426.1%20181.1%20433.5%20260.8%20392.4%20318.3L391.3%20319.9C381%20334.2%20361%20337.6%20346.7%20327.3C332.3%20317%20328.9%20297%20339.2%20282.7L340.3%20281.1C363.2%20249%20359.6%20205.1%20331.7%20177.2C300.3%20145.8%20249.2%20145.8%20217.7%20177.2L105.5%20289.5C73.99%20320.1%2073.99%20372%20105.5%20403.5C133.3%20431.4%20177.3%20435%20209.3%20412.1L210.9%20410.1C225.3%20400.7%20245.3%20404%20255.5%20418.4C265.8%20432.8%20262.5%20452.8%20248.1%20463.1L246.5%20464.2C188.1%20505.3%20110.2%20498.7%2060.21%20448.8C3.741%20392.3%203.741%20300.7%2060.21%20244.3L172.5%20131.1zM467.5%20380C411%20436.5%20319.5%20436.5%20263%20380C213%20330%20206.5%20251.2%20247.6%20193.7L248.7%20192.1C258.1%20177.8%20278.1%20174.4%20293.3%20184.7C307.7%20194.1%20311.1%20214.1%20300.8%20229.3L299.7%20230.9C276.8%20262.1%20280.4%20306.9%20308.3%20334.8C339.7%20366.2%20390.8%20366.2%20422.3%20334.8L534.5%20222.5C566%20191%20566%20139.1%20534.5%20108.5C506.7%2080.63%20462.7%2076.99%20430.7%2099.9L429.1%20101C414.7%20111.3%20394.7%20107.1%20384.5%2093.58C374.2%2079.2%20377.5%2059.21%20391.9%2048.94L393.5%2047.82C451%206.731%20529.8%2013.25%20579.8%2063.24C636.3%20119.7%20636.3%20211.3%20579.8%20267.7L467.5%20380z'/%3e%3c/svg%3e)](#unload-description)

This listener is triggered when the user closes or refreshes the tab, ending the user session. It is useful for cleaning up resources when the app is closed.

#### Example Usage [![](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20fill='%23808080'%20viewBox='0%200%20640%20512'%3e%3c!--!%20Font%20Awesome%20Pro%206.0.0%20by%20@fontawesome%20-%20https://fontawesome.com%20License%20-%20https://fontawesome.com/license%20(Commercial%20License)%20Copyright%202022%20Fonticons,%20Inc.%20--%3e%3cpath%20d='M172.5%20131.1C228.1%2075.51%20320.5%2075.51%20376.1%20131.1C426.1%20181.1%20433.5%20260.8%20392.4%20318.3L391.3%20319.9C381%20334.2%20361%20337.6%20346.7%20327.3C332.3%20317%20328.9%20297%20339.2%20282.7L340.3%20281.1C363.2%20249%20359.6%20205.1%20331.7%20177.2C300.3%20145.8%20249.2%20145.8%20217.7%20177.2L105.5%20289.5C73.99%20320.1%2073.99%20372%20105.5%20403.5C133.3%20431.4%20177.3%20435%20209.3%20412.1L210.9%20410.1C225.3%20400.7%20245.3%20404%20255.5%20418.4C265.8%20432.8%20262.5%20452.8%20248.1%20463.1L246.5%20464.2C188.1%20505.3%20110.2%20498.7%2060.21%20448.8C3.741%20392.3%203.741%20300.7%2060.21%20244.3L172.5%20131.1zM467.5%20380C411%20436.5%20319.5%20436.5%20263%20380C213%20330%20206.5%20251.2%20247.6%20193.7L248.7%20192.1C258.1%20177.8%20278.1%20174.4%20293.3%20184.7C307.7%20194.1%20311.1%20214.1%20300.8%20229.3L299.7%20230.9C276.8%20262.1%20280.4%20306.9%20308.3%20334.8C339.7%20366.2%20390.8%20366.2%20422.3%20334.8L534.5%20222.5C566%20191%20566%20139.1%20534.5%20108.5C506.7%2080.63%20462.7%2076.99%20430.7%2099.9L429.1%20101C414.7%20111.3%20394.7%20107.1%20384.5%2093.58C374.2%2079.2%20377.5%2059.21%20391.9%2048.94L393.5%2047.82C451%206.731%20529.8%2013.25%20579.8%2063.24C636.3%20119.7%20636.3%20211.3%20579.8%20267.7L467.5%20380z'/%3e%3c/svg%3e)](#unload-example-usage)

    import gradio as gr
    with gr.Blocks() as demo:
        gr.Markdown("# When you close the tab, hello will be printed to the console")
        demo.unload(lambda: print("hello"))
    demo.launch()

Parameters ▼

    fn: Callable[..., Any]

Callable function to run to clear resources. The function should not take any arguments and the output is not used.

### Guides[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#guides)

[

Blocks And Event Listeners



](../../guides/blocks-and-event-listeners/)[

Controlling Layout



](../../guides/controlling-layout/)[

State In Blocks



](../../guides/state-in-blocks/)[

Custom CSS And JS



](../../guides/custom-CSS-and-JS/)[

Using Blocks Like Functions



](../../guides/using-blocks-like-functions/)