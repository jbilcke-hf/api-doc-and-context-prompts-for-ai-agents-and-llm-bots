Dataframe
=========

    gradio.Dataframe(···)

1

2

3

0

1

false

1

⋮

2

⋮

3

⋮

0

1

true

1

0

false

[Built with Gradio ![logo](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='576'%20height='576'%20viewBox='0%200%20576%20576'%20fill='none'%3e%3cpath%20d='M287.5%20229L86%20344.5L287.5%20460L489%20344.5L287.5%20229Z'%20stroke='url(%23paint0_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M287.5%20116L86%20231.5L287.5%20347L489%20231.5L287.5%20116Z'%20stroke='url(%23paint1_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M86%20344L288%20229'%20stroke='url(%23paint2_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='bevel'/%3e%3cdefs%3e%3clinearGradient%20id='paint0_linear_102_7'%20x1='60'%20y1='341'%20x2='429.5'%20y2='344'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint1_linear_102_7'%20x1='513.5'%20y1='231'%20x2='143.5'%20y2='231'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint2_linear_102_7'%20x1='60'%20y1='344'%20x2='428.987'%20y2='341.811'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3c/defs%3e%3c/svg%3e)](https://gradio.app) ·  

Settings ![Settings](data:image/svg+xml,%3csvg%20width='24'%20height='24'%20viewBox='0%200%2024%2024'%20xmlns='http://www.w3.org/2000/svg'%3e%3c!--%20Outer%20gear%20teeth%20(gray)%20--%3e%3cpath%20d='M19.14%2012.94c.04-.3.06-.61.06-.94%200-.32-.02-.64-.07-.94l2.03-1.58c.18-.14.23-.41.12-.61l-1.92-3.32c-.12-.22-.37-.29-.59-.22l-2.39.96c-.5-.38-1.03-.7-1.62-.94l-.36-2.54c-.04-.24-.24-.41-.48-.41h-3.84c-.24%200-.43.17-.47.41l-.36%202.54c-.59.24-1.13.57-1.62.94l-2.39-.96c-.22-.08-.47%200-.59.22L2.74%208.87c-.12.21-.08.47.12.61l2.03%201.58c-.05.3-.07.62-.07.94s.02.64.07.94l-2.03%201.58c-.18.14-.23.41-.12.61l1.92%203.32c.12.22.37.29.59.22l2.39-.96c.5.38%201.03.7%201.62.94l.36%202.54c.05.24.24.41.48.41h3.84c.24%200%20.44-.17.47-.41l.36-2.54c.59-.24%201.13-.56%201.62-.94l2.39.96c.22.08.47%200%20.59-.22l1.92-3.32c.12-.22.07-.47-.12-.61l-2.01-1.58zM12%2015.6c-1.98%200-3.6-1.62-3.6-3.6s1.62-3.6%203.6-3.6%203.6%201.62%203.6%203.6-1.62%203.6-3.6%203.6z'%20fill='%23808080'/%3e%3c!--%20Inner%20circle%20(now%20gray)%20--%3e%3ccircle%20cx='12'%20cy='12'%20r='2.5'%20fill='%23808080'/%3e%3c/svg%3e) 

### Description[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#description)

This component displays a table of value spreadsheet-like component. Can be used to display data as an output component, or as an input to collect data from the user.
----------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Behavior[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#behavior)

**As input component**: Passes the uploaded spreadsheet data as a `pandas.DataFrame`, `numpy.array`, `polars.DataFrame`, or native 2D Python `list[list]` depending on `type`
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

##### Your function should accept one of these types:

    def predict(
    	value: pd.DataFrame | np.ndarray | pl.DataFrame | list[list]
    )
    	...

  

**As output component**: Expects data in any of these formats: `pandas.DataFrame`, `pandas.Styler`, `numpy.array`, `polars.DataFrame`, `list[list]`, `list`, or a `dict` with keys 'data' (and optionally 'headers'), or `str` path to a csv, which is rendered as the spreadsheet.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

##### Your function should return one of these types:

    def predict(···) -> pd.DataFrame | Styler | np.ndarray | pl.DataFrame | list | list[list] | dict | str | None
    	...	
    	return value

### Initialization[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#initialization)

Parameters ▼

    value: pd.DataFrame | Styler | np.ndarray | pl.DataFrame | list | list[list] | dict | str | Callable | None

default `= None`

Default value to display in the DataFrame. If a Styler is provided, it will be used to set the displayed value in the DataFrame (e.g. to set precision of numbers) if the \`interactive\` is False. If a Callable function is provided, the function will be called whenever the app loads to set the initial value of the component.

    headers: list[str] | None

default `= None`

List of str header names. If None, no headers are shown.

    row_count: int | tuple[int, str]

default `= (1, 'dynamic')`

Limit number of rows for input and decide whether user can create new rows or delete existing rows. The first element of the tuple is an \`int\`, the row count; the second should be 'fixed' or 'dynamic', the new row behaviour. If an \`int\` is passed the rows default to 'dynamic'

    col_count: int | tuple[int, str] | None

default `= None`

Limit number of columns for input and decide whether user can create new columns or delete existing columns. The first element of the tuple is an \`int\`, the number of columns; the second should be 'fixed' or 'dynamic', the new column behaviour. If an \`int\` is passed the columns default to 'dynamic'

    datatype: str | list[str]

default `= "str"`

Datatype of values in sheet. Can be provided per column as a list of strings, or for the entire sheet as a single string. Valid datatypes are "str", "number", "bool", "date", and "markdown".

    type: Literal['pandas', 'numpy', 'array', 'polars']

default `= "pandas"`

Type of value to be returned by component. "pandas" for pandas dataframe, "numpy" for numpy array, "polars" for polars dataframe, or "array" for a Python list of lists.

    latex_delimiters: list[dict[str, str | bool]] | None

default `= None`

A list of dicts of the form {"left": open delimiter (str), "right": close delimiter (str), "display": whether to display in newline (bool)} that will be used to render LaTeX expressions. If not provided, \`latex\_delimiters\` is set to \`\[{ "left": "$$", "right": "$$", "display": True }\]\`, so only expressions enclosed in $$ delimiters will be rendered as LaTeX, and in a new line. Pass in an empty list to disable LaTeX rendering. For more information, see the [KaTeX documentation](https://katex.org/docs/autorender.html). Only applies to columns whose datatype is "markdown".

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

    max_height: int | str

default `= 500`

The maximum height of the dataframe, specified in pixels if a number is passed, or in CSS units if a string is passed. If more rows are created than can fit in the height, a scrollbar will appear.

    scale: int | None

default `= None`

relative size compared to adjacent Components. For example if Components A and B are in a Row, and A has scale=2, and B has scale=1, A will be twice as wide as B. Should be an integer. scale applies in Rows, and to top-level Components in Blocks where fill\_height=True.

    min_width: int

default `= 160`

minimum pixel width, will wrap if not sufficient screen space to satisfy this value. If a certain scale value results in this Component being narrower than min\_width, the min\_width parameter will be respected first.

    interactive: bool | None

default `= None`

if True, will allow users to edit the dataframe; if False, can only be used to display data. If not provided, this is inferred based on whether the component is used as an input or output.

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

    wrap: bool

default `= False`

If True, the text in table cells will wrap when appropriate. If False and the \`column\_width\` parameter is not set, the column widths will expand based on the cell contents and the table may need to be horizontally scrolled. If \`column\_width\` is set, then any overflow text will be hidden.

    line_breaks: bool

default `= True`

If True (default), will enable Github-flavored Markdown line breaks in chatbot messages. If False, single new lines will be ignored. Only applies for columns of type "markdown."

    column_widths: list[str | int] | None

default `= None`

An optional list representing the width of each column. The elements of the list should be in the format "100px" (ints are also accepted and converted to pixel values) or "10%". If not provided, the column widths will be automatically determined based on the content of the cells. Setting this parameter will cause the browser to try to fit the table within the page width.

    show_fullscreen_button: bool

default `= False`

If True, will show a button to view the values in the table in fullscreen mode.

    show_copy_button: bool

default `= False`

If True, will show a button to copy the table data to the clipboard.

    show_row_numbers: bool

default `= False`

If True, will display row numbers in a separate column.

### Shortcuts[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#shortcuts)

Class

Interface String Shortcut

Initialization

`gradio.Dataframe`

"dataframe"

Uses default values

`gradio.Numpy`

"numpy"

Uses type="numpy"

`gradio.Matrix`

"matrix"

Uses type="array"

`gradio.List`

"list"

Uses type="array", col\_count=1

### Demos[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#demos)

filter\_recordsmatrix\_transposetax\_calculatorsort\_records

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

›

⌄

⌄

⌄

import gradio as gr

  

def filter\_records(records, gender):

return records\[records\["gender"\] \== gender\]

  

demo \= gr.Interface(

filter\_records,

\[

gr.Dataframe(

headers\=\["name", "age", "gender"\],

datatype\=\["str", "number", "str"\],

row\_count\=5,

col\_count\=(3, "fixed"),

),

gr.Dropdown(\["M", "F", "O"\]),

\],

"dataframe",

description\="Enter gender as 'M', 'F', or 'O' for other.",

)

  

if \_\_name\_\_ \== "\_\_main\_\_":

demo.launch()

Enter gender as 'M', 'F', or 'O' for other.

records

records

name

age

gender

name

⋮

age

⋮

gender

⋮

gender

Clear Submit

output

output

1

2

3

1

2

3

Flag

[Built with Gradio ![logo](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='576'%20height='576'%20viewBox='0%200%20576%20576'%20fill='none'%3e%3cpath%20d='M287.5%20229L86%20344.5L287.5%20460L489%20344.5L287.5%20229Z'%20stroke='url(%23paint0_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M287.5%20116L86%20231.5L287.5%20347L489%20231.5L287.5%20116Z'%20stroke='url(%23paint1_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M86%20344L288%20229'%20stroke='url(%23paint2_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='bevel'/%3e%3cdefs%3e%3clinearGradient%20id='paint0_linear_102_7'%20x1='60'%20y1='341'%20x2='429.5'%20y2='344'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint1_linear_102_7'%20x1='513.5'%20y1='231'%20x2='143.5'%20y2='231'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint2_linear_102_7'%20x1='60'%20y1='344'%20x2='428.987'%20y2='341.811'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3c/defs%3e%3c/svg%3e)](https://gradio.app) ·  

Settings ![Settings](data:image/svg+xml,%3csvg%20width='24'%20height='24'%20viewBox='0%200%2024%2024'%20xmlns='http://www.w3.org/2000/svg'%3e%3c!--%20Outer%20gear%20teeth%20(gray)%20--%3e%3cpath%20d='M19.14%2012.94c.04-.3.06-.61.06-.94%200-.32-.02-.64-.07-.94l2.03-1.58c.18-.14.23-.41.12-.61l-1.92-3.32c-.12-.22-.37-.29-.59-.22l-2.39.96c-.5-.38-1.03-.7-1.62-.94l-.36-2.54c-.04-.24-.24-.41-.48-.41h-3.84c-.24%200-.43.17-.47.41l-.36%202.54c-.59.24-1.13.57-1.62.94l-2.39-.96c-.22-.08-.47%200-.59.22L2.74%208.87c-.12.21-.08.47.12.61l2.03%201.58c-.05.3-.07.62-.07.94s.02.64.07.94l-2.03%201.58c-.18.14-.23.41-.12.61l1.92%203.32c.12.22.37.29.59.22l2.39-.96c.5.38%201.03.7%201.62.94l.36%202.54c.05.24.24.41.48.41h3.84c.24%200%20.44-.17.47-.41l.36-2.54c.59-.24%201.13-.56%201.62-.94l2.39.96c.22.08.47%200%20.59-.22l1.92-3.32c.12-.22.07-.47-.12-.61l-2.01-1.58zM12%2015.6c-1.98%200-3.6-1.62-3.6-3.6s1.62-3.6%203.6-3.6%203.6%201.62%203.6%203.6-1.62%203.6-3.6%203.6z'%20fill='%23808080'/%3e%3c!--%20Inner%20circle%20(now%20gray)%20--%3e%3ccircle%20cx='12'%20cy='12'%20r='2.5'%20fill='%23808080'/%3e%3c/svg%3e) 

    import gradio as gr
    
    def filter_records(records, gender):
        return records[records["gender"] == gender]
    
    demo = gr.Interface(
        filter_records,
        [
            gr.Dataframe(
                headers=["name", "age", "gender"],
                datatype=["str", "number", "str"],
                row_count=5,
                col_count=(3, "fixed"),
            ),
            gr.Dropdown(["M", "F", "O"]),
        ],
        "dataframe",
        description="Enter gender as 'M', 'F', or 'O' for other.",
    )
    
    if __name__ == "__main__":
        demo.launch()
    

Loading...

[gradio/filter\_records](https://huggingface.co/spaces/gradio/filter_records) built with [Gradio](https://gradio.app). Hosted on [![Hugging Face Space](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='10'%20height='10'%20fill='none'%3e%3cpath%20fill='%23FF3270'%20d='M1.93%206.03v2.04h2.04V6.03H1.93Z'/%3e%3cpath%20fill='%23861FFF'%20d='M6.03%206.03v2.04h2.04V6.03H6.03Z'/%3e%3cpath%20fill='%23097EFF'%20d='M1.93%201.93v2.04h2.04V1.93H1.93Z'/%3e%3cpath%20fill='%23000'%20fill-rule='evenodd'%20d='M.5%201.4c0-.5.4-.9.9-.9h3.1a.9.9%200%200%201%20.87.67A2.44%202.44%200%200%201%209.5%202.95c0%20.65-.25%201.24-.67%201.68.39.1.67.46.67.88v3.08c0%20.5-.4.91-.9.91H1.4a.9.9%200%200%201-.9-.9V1.4Zm1.43.53v2.04h2.04V1.93H1.93Zm0%206.14V6.03h2.04v2.04H1.93Zm4.1%200V6.03h2.04v2.04H6.03Zm0-5.12a1.02%201.02%200%201%201%202.04%200%201.02%201.02%200%200%201-2.04%200Z'%20clip-rule='evenodd'/%3e%3cpath%20fill='%23FFD702'%20d='M7.05%201.93a1.02%201.02%200%201%200%200%202.04%201.02%201.02%200%200%200%200-2.04Z'/%3e%3c/svg%3e) Spaces](https://huggingface.co/spaces)

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

›

⌄

⌄

⌄

import numpy as np

  

import gradio as gr

  

def transpose(matrix):

return matrix.T

  

demo \= gr.Interface(

transpose,

gr.Dataframe(type\="numpy", datatype\="number", row\_count\=5, col\_count\=3, show\_fullscreen\_button\=True),

"numpy",

examples\=\[

\[np.zeros((3, 3)).tolist()\],

\[np.ones((2, 2)).tolist()\],

\[np.random.randint(0, 10, (3, 10)).tolist()\],

\[np.random.randint(0, 10, (10, 3)).tolist()\],

\[np.random.randint(0, 10, (10, 10)).tolist()\],

\],

cache\_examples\=False

)

  

if \_\_name\_\_ \== "\_\_main\_\_":

demo.launch()

matrix

matrix

1

2

3

1

⋮

2

⋮

3

⋮

Clear Submit

output

output

1

2

3

1

2

3

Flag

Examples

0

0

0

0

0

0

0

0

0

1

1

1

1

3

4

0

…

5

4

2

…

6

9

9

…

3

8

1

2

7

6

1

1

7

2

3

4

…

5

4

9

…

6

6

6

…

[Built with Gradio ![logo](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='576'%20height='576'%20viewBox='0%200%20576%20576'%20fill='none'%3e%3cpath%20d='M287.5%20229L86%20344.5L287.5%20460L489%20344.5L287.5%20229Z'%20stroke='url(%23paint0_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M287.5%20116L86%20231.5L287.5%20347L489%20231.5L287.5%20116Z'%20stroke='url(%23paint1_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M86%20344L288%20229'%20stroke='url(%23paint2_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='bevel'/%3e%3cdefs%3e%3clinearGradient%20id='paint0_linear_102_7'%20x1='60'%20y1='341'%20x2='429.5'%20y2='344'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint1_linear_102_7'%20x1='513.5'%20y1='231'%20x2='143.5'%20y2='231'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint2_linear_102_7'%20x1='60'%20y1='344'%20x2='428.987'%20y2='341.811'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3c/defs%3e%3c/svg%3e)](https://gradio.app) ·  

Settings ![Settings](data:image/svg+xml,%3csvg%20width='24'%20height='24'%20viewBox='0%200%2024%2024'%20xmlns='http://www.w3.org/2000/svg'%3e%3c!--%20Outer%20gear%20teeth%20(gray)%20--%3e%3cpath%20d='M19.14%2012.94c.04-.3.06-.61.06-.94%200-.32-.02-.64-.07-.94l2.03-1.58c.18-.14.23-.41.12-.61l-1.92-3.32c-.12-.22-.37-.29-.59-.22l-2.39.96c-.5-.38-1.03-.7-1.62-.94l-.36-2.54c-.04-.24-.24-.41-.48-.41h-3.84c-.24%200-.43.17-.47.41l-.36%202.54c-.59.24-1.13.57-1.62.94l-2.39-.96c-.22-.08-.47%200-.59.22L2.74%208.87c-.12.21-.08.47.12.61l2.03%201.58c-.05.3-.07.62-.07.94s.02.64.07.94l-2.03%201.58c-.18.14-.23.41-.12.61l1.92%203.32c.12.22.37.29.59.22l2.39-.96c.5.38%201.03.7%201.62.94l.36%202.54c.05.24.24.41.48.41h3.84c.24%200%20.44-.17.47-.41l.36-2.54c.59-.24%201.13-.56%201.62-.94l2.39.96c.22.08.47%200%20.59-.22l1.92-3.32c.12-.22.07-.47-.12-.61l-2.01-1.58zM12%2015.6c-1.98%200-3.6-1.62-3.6-3.6s1.62-3.6%203.6-3.6%203.6%201.62%203.6%203.6-1.62%203.6-3.6%203.6z'%20fill='%23808080'/%3e%3c!--%20Inner%20circle%20(now%20gray)%20--%3e%3ccircle%20cx='12'%20cy='12'%20r='2.5'%20fill='%23808080'/%3e%3c/svg%3e) 

    import numpy as np
    
    import gradio as gr
    
    def transpose(matrix):
        return matrix.T
    
    demo = gr.Interface(
        transpose,
        gr.Dataframe(type="numpy", datatype="number", row_count=5, col_count=3, show_fullscreen_button=True),
        "numpy",
        examples=[
            [np.zeros((3, 3)).tolist()],
            [np.ones((2, 2)).tolist()],
            [np.random.randint(0, 10, (3, 10)).tolist()],
            [np.random.randint(0, 10, (10, 3)).tolist()],
            [np.random.randint(0, 10, (10, 10)).tolist()],
        ],
        cache_examples=False
    )
    
    if __name__ == "__main__":
        demo.launch()
    

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

⌄

⌄

⌄

⌄

import gradio as gr

  

def tax\_calculator(income, marital\_status, assets):

tax\_brackets \= \[(10, 0), (25, 8), (60, 12), (120, 20), (250, 30)\]

total\_deductible \= sum(assets\["Cost"\])

taxable\_income \= income \- total\_deductible

  

total\_tax \= 0

for bracket, rate in tax\_brackets:

if taxable\_income \> bracket:

total\_tax += (taxable\_income \- bracket) \* rate / 100

  

if marital\_status \== "Married":

total\_tax \*= 0.75

elif marital\_status \== "Divorced":

total\_tax \*= 0.8

  

return round(total\_tax)

  

demo \= gr.Interface(

tax\_calculator,

\[

"number",

gr.Radio(\["Single", "Married", "Divorced"\]),

gr.Dataframe(

headers\=\["Item", "Cost"\],

datatype\=\["str", "number"\],

label\="Assets Purchased this Year",

),

\],

"number",

examples\=\[

\[10000, "Married", \[\["Suit", 5000\], \["Laptop", 800\], \["Car", 1800\]\]\],

\[80000, "Single", \[\["Suit", 800\], \["Watch", 1800\], \["Car", 800\]\]\],

\],

)

income 

marital\_status

 Single Married Divorced

Assets Purchased this Year

Assets Purchased this Year

Item

Cost

Item

⋮

Cost

⋮

Clear Submit

output 

Flag

Examples

income

marital\_status

Assets Purchased this Year

10000

Married

Suit

5000

Laptop

800

Car

1800

80000

Single

Suit

800

Watch

1800

Car

800

[Built with Gradio ![logo](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='576'%20height='576'%20viewBox='0%200%20576%20576'%20fill='none'%3e%3cpath%20d='M287.5%20229L86%20344.5L287.5%20460L489%20344.5L287.5%20229Z'%20stroke='url(%23paint0_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M287.5%20116L86%20231.5L287.5%20347L489%20231.5L287.5%20116Z'%20stroke='url(%23paint1_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='round'/%3e%3cpath%20d='M86%20344L288%20229'%20stroke='url(%23paint2_linear_102_7)'%20stroke-width='59'%20stroke-linejoin='bevel'/%3e%3cdefs%3e%3clinearGradient%20id='paint0_linear_102_7'%20x1='60'%20y1='341'%20x2='429.5'%20y2='344'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint1_linear_102_7'%20x1='513.5'%20y1='231'%20x2='143.5'%20y2='231'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3clinearGradient%20id='paint2_linear_102_7'%20x1='60'%20y1='344'%20x2='428.987'%20y2='341.811'%20gradientUnits='userSpaceOnUse'%3e%3cstop%20stop-color='%23F9D100'/%3e%3cstop%20offset='1'%20stop-color='%23F97700'/%3e%3c/linearGradient%3e%3c/defs%3e%3c/svg%3e)](https://gradio.app) ·  

Settings ![Settings](data:image/svg+xml,%3csvg%20width='24'%20height='24'%20viewBox='0%200%2024%2024'%20xmlns='http://www.w3.org/2000/svg'%3e%3c!--%20Outer%20gear%20teeth%20(gray)%20--%3e%3cpath%20d='M19.14%2012.94c.04-.3.06-.61.06-.94%200-.32-.02-.64-.07-.94l2.03-1.58c.18-.14.23-.41.12-.61l-1.92-3.32c-.12-.22-.37-.29-.59-.22l-2.39.96c-.5-.38-1.03-.7-1.62-.94l-.36-2.54c-.04-.24-.24-.41-.48-.41h-3.84c-.24%200-.43.17-.47.41l-.36%202.54c-.59.24-1.13.57-1.62.94l-2.39-.96c-.22-.08-.47%200-.59.22L2.74%208.87c-.12.21-.08.47.12.61l2.03%201.58c-.05.3-.07.62-.07.94s.02.64.07.94l-2.03%201.58c-.18.14-.23.41-.12.61l1.92%203.32c.12.22.37.29.59.22l2.39-.96c.5.38%201.03.7%201.62.94l.36%202.54c.05.24.24.41.48.41h3.84c.24%200%20.44-.17.47-.41l.36-2.54c.59-.24%201.13-.56%201.62-.94l2.39.96c.22.08.47%200%20.59-.22l1.92-3.32c.12-.22.07-.47-.12-.61l-2.01-1.58zM12%2015.6c-1.98%200-3.6-1.62-3.6-3.6s1.62-3.6%203.6-3.6%203.6%201.62%203.6%203.6-1.62%203.6-3.6%203.6z'%20fill='%23808080'/%3e%3c!--%20Inner%20circle%20(now%20gray)%20--%3e%3ccircle%20cx='12'%20cy='12'%20r='2.5'%20fill='%23808080'/%3e%3c/svg%3e) 

    import gradio as gr
    
    def tax_calculator(income, marital_status, assets):
        tax_brackets = [(10, 0), (25, 8), (60, 12), (120, 20), (250, 30)]
        total_deductible = sum(assets["Cost"])
        taxable_income = income - total_deductible
    
        total_tax = 0
        for bracket, rate in tax_brackets:
            if taxable_income > bracket:
                total_tax += (taxable_income - bracket) * rate / 100
    
        if marital_status == "Married":
            total_tax *= 0.75
        elif marital_status == "Divorced":
            total_tax *= 0.8
    
        return round(total_tax)
    
    demo = gr.Interface(
        tax_calculator,
        [
            "number",
            gr.Radio(["Single", "Married", "Divorced"]),
            gr.Dataframe(
                headers=["Item", "Cost"],
                datatype=["str", "number"],
                label="Assets Purchased this Year",
            ),
        ],
        "number",
        examples=[
            [10000, "Married", [["Suit", 5000], ["Laptop", 800], ["Car", 1800]]],
            [80000, "Single", [["Suit", 800], ["Watch", 1800], ["Car", 800]]],
        ],
    )
    
    demo.launch()
    

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

›

⌄

⌄

import gradio as gr

  

def sort\_records(records):

return records.sort("Quantity")

  

demo \= gr.Interface(

sort\_records,

gr.Dataframe(

headers\=\["Item", "Quantity"\],

datatype\=\["str", "number"\],

row\_count\=3,

col\_count\=(2, "fixed"),

type\="polars"

),

"dataframe",

description\="Sort by Quantity"

)

  

if \_\_name\_\_ \== "\_\_main\_\_":

demo.launch()

Error

Traceback (most recent call last): File "<exec>", line 149, in \_run\_code File "<string>", line 8, in <module> File "/lib/python3.12/site-packages/gradio/component\_meta.py", line 179, in wrapper return fn(self, \*\*kwargs) ^^^^^^^^^^^^^^^^^^ File "/lib/python3.12/site-packages/gradio/components/dataframe.py", line 154, in \_\_init\_\_ raise ImportError( ImportError: Polars is not installed. Please install using \`pip install polars\`.

    PythonError: Traceback (most recent call last):
      File "<exec>", line 149, in _run_code
      File "<string>", line 8, in <module>
      File "/lib/python3.12/site-packages/gradio/component_meta.py", line 179, in wrapper
        return fn(self, **kwargs)
               ^^^^^^^^^^^^^^^^^^
      File "/lib/python3.12/site-packages/gradio/components/dataframe.py", line 154, in __init__
        raise ImportError(
    ImportError: Polars is not installed. Please install using `pip install polars`.
    
        at new_error (https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.js:10:10009)
        at https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.wasm:wasm-function[307]:0x16e356
        at https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.wasm:wasm-function[504]:0x17849f
        at https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.wasm:wasm-function[4583]:0x328567
        at https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.wasm:wasm-function[1148]:0x1c441a
        at https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.wasm:wasm-function[3619]:0x2ca2cc
        at https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.wasm:wasm-function[2181]:0x20c217
        at https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.wasm:wasm-function[1156]:0x1c4b01
        at https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.wasm:wasm-function[1159]:0x1c4e10
        at https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.wasm:wasm-function[1160]:0x1c4e8e
        at https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.wasm:wasm-function[3425]:0x2a0ca0
        at https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.wasm:wasm-function[3426]:0x2a71fe
        at https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.wasm:wasm-function[1162]:0x1c4fce
        at https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.wasm:wasm-function[1157]:0x1c4c37
        at https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.wasm:wasm-function[491]:0x177aff
        at https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.wasm:wasm-function[492]:0x177c21
        at wrapper (https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.js:10:120177)
        at Object.promisingApply (https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.js:10:119922)
        at callPyObjectKwargsPromising (https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.js:10:63452)
        at Module.callPyObjectMaybePromising (https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.js:10:63952)
        at wrapper (https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.js:10:27341)
        at Zn.e.port1.onmessage (https://cdn.jsdelivr.net/pyodide/v0.27.2/full/pyodide.asm.js:10:101745)

    import gradio as gr
    
    def sort_records(records):
        return records.sort("Quantity")
    
    demo = gr.Interface(
        sort_records,
        gr.Dataframe(
            headers=["Item", "Quantity"],
            datatype=["str", "number"],
            row_count=3,
            col_count=(2, "fixed"),
            type="polars"
        ),
        "dataframe",
        description="Sort by Quantity"
    )
    
    if __name__ == "__main__":
        demo.launch()
    

### Event Listeners[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#event-listeners)

#### Description

Event listeners allow you to respond to user interactions with the UI components you've defined in a Gradio Blocks app. When a user interacts with an element, such as changing a slider value or uploading an image, a function is called.

#### Supported Event Listeners

The Dataframe component supports the following event listeners. Each event listener takes the same parameters, which are listed in the [Event Parameters](#event-listeners-arguments) table below.

Listener

Description

`Dataframe.change(fn, ···)`

Triggered when the value of the Dataframe changes either because of user input (e.g. a user types in a textbox) OR because of a function update (e.g. an image receives a value from the output of an event trigger). See `.input()` for a listener that is only triggered by user input.

`Dataframe.input(fn, ···)`

This listener is triggered when the user changes the value of the Dataframe.

`Dataframe.select(fn, ···)`

Event listener for when the user selects or deselects the Dataframe. Uses event data gradio.SelectData to carry `value` referring to the label of the Dataframe, and `selected` to refer to state of the Dataframe. See EventData documentation on how to use this event data

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