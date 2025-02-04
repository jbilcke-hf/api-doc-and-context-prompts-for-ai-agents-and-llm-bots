FileExplorer
============

    gradio.FileExplorer(···)

### Description[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#description)

Creates a file explorer component that allows users to browse files on the machine hosting the Gradio app. As an input component, it also allows users to select files to be used as input to a function, while as an output component, it displays selected files.  

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Behavior[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#behavior)

**As input component**: Passes the selected file or directory as a `str` path (relative to `root`) or `list[str}` depending on `file_count`
-------------------------------------------------------------------------------------------------------------------------------------------

##### Your function should accept one of these types:

    def predict(
    	value: list[str] | str | None
    )
    	...

  

**As output component**: Expects function to return a `str` path to a file, or `list[str]` consisting of paths to files.
------------------------------------------------------------------------------------------------------------------------

##### Your function should return one of these types:

    def predict(···) -> str | list[str] | None
    	...	
    	return value

### Initialization[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#initialization)

Parameters ▼

    glob: str

default `= "**/*"`

The glob-style pattern used to select which files to display, e.g. "\*" to match all files, "\*.png" to match all .png files, "\*\*/\*.txt" to match any .txt file in any subdirectory, etc. The default value matches all files and folders recursively. See the Python glob documentation at https://docs.python.org/3/library/glob.html for more information.

    value: str | list[str] | Callable | None

default `= None`

The file (or list of files, depending on the \`file\_count\` parameter) to show as "selected" when the component is first loaded. If a callable is provided, it will be called when the app loads to set the initial value of the component. If not provided, no files are shown as selected.

    file_count: Literal['single', 'multiple']

default `= "multiple"`

Whether to allow single or multiple files to be selected. If "single", the component will return a single absolute file path as a string. If "multiple", the component will return a list of absolute file paths as a list of strings.

    root_dir: str | Path

default `= "."`

Path to root directory to select files from. If not provided, defaults to current working directory.

    ignore_glob: str | None

default `= None`

The glob-style, case-sensitive pattern that will be used to exclude files from the list. For example, "\*.py" will exclude all .py files from the list. See the Python glob documentation at https://docs.python.org/3/library/glob.html for more information.

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

    height: int | str | None

default `= None`

The maximum height of the file component, specified in pixels if a number is passed, or in CSS units if a string is passed. If more files are uploaded than can fit in the height, a scrollbar will appear.

    max_height: int | str | None

default `= 500`

    min_height: int | str | None

default `= None`

    interactive: bool | None

default `= None`

if True, will allow users to select file(s); if False, will only display files. If not provided, this is inferred based on whether the component is used as an input or output.

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

`gradio.FileExplorer`

"fileexplorer"

Uses default values

### Demos[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#demos)

file\_explorer

Open in 🎢 ↗

app.py

Importing gradio package...

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

import gradio as gr

from pathlib import Path

  

current\_file\_path \= Path(\_\_file\_\_).resolve()

relative\_path \= "path/to/file"

absolute\_path \= (current\_file\_path.parent / ".." / ".." / "gradio").resolve()

  

def get\_file\_content(file):

return (file,)

  

with gr.Blocks() as demo:

gr.Markdown('### \`FileExplorer\` to \`FileExplorer\` -- \`file\_count="multiple"\`')

submit\_btn \= gr.Button("Select")

with gr.Row():

file \= gr.FileExplorer(

glob\="\*\*/components/\*.py",

\# value=\["themes/utils"\],

root\_dir\=absolute\_path,

ignore\_glob\="\*\*/\_\_init\_\_.py",

)

  

file2 \= gr.FileExplorer(

glob\="\*\*/components/\*\*/\*.py",

root\_dir\=absolute\_path,

ignore\_glob\="\*\*/\_\_init\_\_.py",

)

submit\_btn.click(lambda x: x, file, file2)

  

gr.Markdown("---")

gr.Markdown('### \`FileExplorer\` to \`Code\` -- \`file\_count="single"\`')

with gr.Group():

with gr.Row():

file\_3 \= gr.FileExplorer(

scale\=1,

glob\="\*\*/components/\*\*/\*.py",

value\=\["themes/utils"\],

    import gradio as gr
    from pathlib import Path
    
    current_file_path = Path(__file__).resolve()
    relative_path = "path/to/file"
    absolute_path = (current_file_path.parent / ".." / ".." / "gradio").resolve()
    
    def get_file_content(file):
        return (file,)
    
    with gr.Blocks() as demo:
        gr.Markdown('### `FileExplorer` to `FileExplorer` -- `file_count="multiple"`')
        submit_btn = gr.Button("Select")
        with gr.Row():
            file = gr.FileExplorer(
                glob="**/components/*.py",
                # value=["themes/utils"],
                root_dir=absolute_path,
                ignore_glob="**/__init__.py",
            )
    
            file2 = gr.FileExplorer(
                glob="**/components/**/*.py",
                root_dir=absolute_path,
                ignore_glob="**/__init__.py",
            )
        submit_btn.click(lambda x: x, file, file2)
    
        gr.Markdown("---")
        gr.Markdown('### `FileExplorer` to `Code` -- `file_count="single"`')
        with gr.Group():
            with gr.Row():
                file_3 = gr.FileExplorer(
                    scale=1,
                    glob="**/components/**/*.py",
                    value=["themes/utils"],
                    file_count="single",
                    root_dir=absolute_path,
                    ignore_glob="**/__init__.py",
                    elem_id="file",
                )
    
                code = gr.Code(lines=30, scale=2, language="python")
    
        file_3.change(get_file_content, file_3, code)
    
    if __name__ == "__main__":
        demo.launch()
    

Loading...

[gradio/file\_explorer](https://huggingface.co/spaces/gradio/file_explorer) built with [Gradio](https://gradio.app). Hosted on [![Hugging Face Space](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='10'%20height='10'%20fill='none'%3e%3cpath%20fill='%23FF3270'%20d='M1.93%206.03v2.04h2.04V6.03H1.93Z'/%3e%3cpath%20fill='%23861FFF'%20d='M6.03%206.03v2.04h2.04V6.03H6.03Z'/%3e%3cpath%20fill='%23097EFF'%20d='M1.93%201.93v2.04h2.04V1.93H1.93Z'/%3e%3cpath%20fill='%23000'%20fill-rule='evenodd'%20d='M.5%201.4c0-.5.4-.9.9-.9h3.1a.9.9%200%200%201%20.87.67A2.44%202.44%200%200%201%209.5%202.95c0%20.65-.25%201.24-.67%201.68.39.1.67.46.67.88v3.08c0%20.5-.4.91-.9.91H1.4a.9.9%200%200%201-.9-.9V1.4Zm1.43.53v2.04h2.04V1.93H1.93Zm0%206.14V6.03h2.04v2.04H1.93Zm4.1%200V6.03h2.04v2.04H6.03Zm0-5.12a1.02%201.02%200%201%201%202.04%200%201.02%201.02%200%200%201-2.04%200Z'%20clip-rule='evenodd'/%3e%3cpath%20fill='%23FFD702'%20d='M7.05%201.93a1.02%201.02%200%201%200%200%202.04%201.02%201.02%200%200%200%200-2.04Z'/%3e%3c/svg%3e) Spaces](https://huggingface.co/spaces)

### Event Listeners[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#event-listeners)

#### Description

Event listeners allow you to respond to user interactions with the UI components you've defined in a Gradio Blocks app. When a user interacts with an element, such as changing a slider value or uploading an image, a function is called.

#### Supported Event Listeners

The FileExplorer component supports the following event listeners. Each event listener takes the same parameters, which are listed in the [Event Parameters](#event-listeners-arguments) table below.

Listener

Description

`FileExplorer.change(fn, ···)`

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