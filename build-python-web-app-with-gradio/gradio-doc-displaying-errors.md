Error
=====

    raise gradio.Error("An error occurred 💥!", duration=5)

### Description[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#description)

This class allows you to pass custom error messages to the user. You can do so by raising a gr.Error("custom message") anywhere in the code, and when that line is executed the custom message will appear in a modal on the demo.
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

You can control for how long the error message is displayed with the `duration` parameter. If it’s `None`, the message will be displayed forever until the user closes it. If it’s a number, it will be shown for that many seconds.
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

You can also hide the error modal from being shown in the UI by setting `visible=False`.
----------------------------------------------------------------------------------------

Below is a demo of how different values of duration control the error, info, and warning messages. You can see the code [here](https://huggingface.co/spaces/freddyaboulton/gradio-error-duration/blob/244331cf53f6b5fa2fd406ece3bf55c6ccb9f5f2/app.py#L17).
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

![modal_control](https://github.com/gradio-app/gradio/assets/41651716/f0977bcd-eaec-4eca-a2fd-ede95fdb8fd2)

### Example Usage[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#example-usage)

    import gradio as gr
    def divide(numerator, denominator):
        if denominator == 0:
            raise gr.Error("Cannot divide by zero!")
    gr.Interface(divide, ["number", "number"], "number").launch()

### Initialization[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#initialization)

Parameters ▼

    message: str

default `= "Error raised."`

The error message to be displayed to the user. Can be HTML, which will be rendered in the modal.

    duration: float | None

default `= 10`

The duration in seconds to display the error message. If None or 0, the error message will be displayed until the user closes it.

    visible: bool

default `= True`

Whether the error message should be displayed in the UI.

    title: str

default `= "Error"`

The title to be displayed to the user at the top of the error modal.

    print_exception: bool

default `= True`

Whether to print traceback of the error to the console when the error is raised.

### Demos[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#demos)

calculatorblocks\_chained\_events

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

›

⌄

⌄

⌄

⌄

⌄

⌄

⌄

⌄

⌄

import gradio as gr

  

def calculator(num1, operation, num2):

if operation \== "add":

return num1 + num2

elif operation \== "subtract":

return num1 \- num2

elif operation \== "multiply":

return num1 \* num2

elif operation \== "divide":

if num2 \== 0:

raise gr.Error("Cannot divide by zero!")

return num1 / num2

  

demo \= gr.Interface(

calculator,

\[

"number",

gr.Radio(\["add", "subtract", "multiply", "divide"\]),

"number"

\],

"number",

examples\=\[

\[45, "add", 3\],

\[3.14, "divide", 2\],

\[144, "multiply", 2.5\],

\[0, "subtract", 1.2\],

\],

title\="Toy Calculator",

description\="Here's a sample toy calculator.",

)

  

if \_\_name\_\_ \== "\_\_main\_\_":

demo.launch()

    import gradio as gr
    
    def calculator(num1, operation, num2):
        if operation == "add":
            return num1 + num2
        elif operation == "subtract":
            return num1 - num2
        elif operation == "multiply":
            return num1 * num2
        elif operation == "divide":
            if num2 == 0:
                raise gr.Error("Cannot divide by zero!")
            return num1 / num2
    
    demo = gr.Interface(
        calculator,
        [
            "number",
            gr.Radio(["add", "subtract", "multiply", "divide"]),
            "number"
        ],
        "number",
        examples=[
            [45, "add", 3],
            [3.14, "divide", 2],
            [144, "multiply", 2.5],
            [0, "subtract", 1.2],
        ],
        title="Toy Calculator",
        description="Here's a sample toy calculator.",
    )
    
    if __name__ == "__main__":
        demo.launch()
    

Chargement...

[gradio/calculator](https://huggingface.co/spaces/gradio/calculator) Construit avec [Gradio](https://gradio.app). Hosted on [![Hugging Face Space](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='10'%20height='10'%20fill='none'%3e%3cpath%20fill='%23FF3270'%20d='M1.93%206.03v2.04h2.04V6.03H1.93Z'/%3e%3cpath%20fill='%23861FFF'%20d='M6.03%206.03v2.04h2.04V6.03H6.03Z'/%3e%3cpath%20fill='%23097EFF'%20d='M1.93%201.93v2.04h2.04V1.93H1.93Z'/%3e%3cpath%20fill='%23000'%20fill-rule='evenodd'%20d='M.5%201.4c0-.5.4-.9.9-.9h3.1a.9.9%200%200%201%20.87.67A2.44%202.44%200%200%201%209.5%202.95c0%20.65-.25%201.24-.67%201.68.39.1.67.46.67.88v3.08c0%20.5-.4.91-.9.91H1.4a.9.9%200%200%201-.9-.9V1.4Zm1.43.53v2.04h2.04V1.93H1.93Zm0%206.14V6.03h2.04v2.04H1.93Zm4.1%200V6.03h2.04v2.04H6.03Zm0-5.12a1.02%201.02%200%201%201%202.04%200%201.02%201.02%200%200%201-2.04%200Z'%20clip-rule='evenodd'/%3e%3cpath%20fill='%23FFD702'%20d='M7.05%201.93a1.02%201.02%200%201%200%200%202.04%201.02%201.02%200%200%200%200-2.04Z'/%3e%3c/svg%3e) Spaces](https://huggingface.co/spaces)

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

⌄

import gradio as gr

  

def failure():

raise gr.Error("This should fail!")

  

def exception():

raise ValueError("Something went wrong")

  

def success():

return True

  

def warning\_fn():

gr.Warning("This is a warning!")

  

def info\_fn():

gr.Info("This is some info")

  

with gr.Blocks() as demo:

gr.Markdown("Used in E2E tests of success event trigger. The then event covered in chatbot E2E tests."

" Also testing that the status modals show up.")

with gr.Row():

result \= gr.Textbox(label\="Result")

result\_2 \= gr.Textbox(label\="Consecutive Event")

with gr.Row():

success\_btn \= gr.Button(value\="Trigger Success")

success\_btn\_2 \= gr.Button(value\="Trigger Consecutive Success")

failure\_btn \= gr.Button(value\="Trigger Failure")

failure\_exception \= gr.Button(value\="Trigger Failure With ValueError")

with gr.Row():

trigger\_warning \= gr.Button(value\="Trigger Warning")

trigger\_info \= gr.Button(value\="Trigger Info")

  

success\_btn\_2.click(success, None, None).success(lambda: "First Event Trigered", None, result).success(lambda: "Consecutive Event Triggered", None, result\_2)

success\_btn.click(success, None, None).success(lambda: "Success event triggered", inputs\=None, outputs\=result)

failure\_btn.click(failure, None, None).success(lambda: "Should not be triggered", inputs\=None, outputs\=result)

failure\_exception.click(exception, None, None)

    import gradio as gr
    
    def failure():
        raise gr.Error("This should fail!")
    
    def exception():
        raise ValueError("Something went wrong")
    
    def success():
        return True
    
    def warning_fn():
        gr.Warning("This is a warning!")
    
    def info_fn():
        gr.Info("This is some info")
    
    with gr.Blocks() as demo:
        gr.Markdown("Used in E2E tests of success event trigger. The then event covered in chatbot E2E tests."
                    " Also testing that the status modals show up.")
        with gr.Row():
            result = gr.Textbox(label="Result")
            result_2 = gr.Textbox(label="Consecutive Event")
        with gr.Row():
            success_btn = gr.Button(value="Trigger Success")
            success_btn_2 = gr.Button(value="Trigger Consecutive Success")
            failure_btn = gr.Button(value="Trigger Failure")
            failure_exception = gr.Button(value="Trigger Failure With ValueError")
        with gr.Row():
            trigger_warning = gr.Button(value="Trigger Warning")
            trigger_info = gr.Button(value="Trigger Info")
    
            success_btn_2.click(success, None, None).success(lambda: "First Event Trigered", None, result).success(lambda: "Consecutive Event Triggered", None, result_2)
            success_btn.click(success, None, None).success(lambda: "Success event triggered", inputs=None, outputs=result)
            failure_btn.click(failure, None, None).success(lambda: "Should not be triggered", inputs=None, outputs=result)
            failure_exception.click(exception, None, None)
            trigger_warning.click(warning_fn, None, None)
            trigger_info.click(info_fn, None, None)
    
    if __name__ == "__main__":
        demo.launch(show_error=True)
    

Chargement...

[gradio/blocks\_chained\_events](https://huggingface.co/spaces/gradio/blocks_chained_events) Construit avec [Gradio](https://gradio.app). Hosted on [![Hugging Face Space](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='10'%20height='10'%20fill='none'%3e%3cpath%20fill='%23FF3270'%20d='M1.93%206.03v2.04h2.04V6.03H1.93Z'/%3e%3cpath%20fill='%23861FFF'%20d='M6.03%206.03v2.04h2.04V6.03H6.03Z'/%3e%3cpath%20fill='%23097EFF'%20d='M1.93%201.93v2.04h2.04V1.93H1.93Z'/%3e%3cpath%20fill='%23000'%20fill-rule='evenodd'%20d='M.5%201.4c0-.5.4-.9.9-.9h3.1a.9.9%200%200%201%20.87.67A2.44%202.44%200%200%201%209.5%202.95c0%20.65-.25%201.24-.67%201.68.39.1.67.46.67.88v3.08c0%20.5-.4.91-.9.91H1.4a.9.9%200%200%201-.9-.9V1.4Zm1.43.53v2.04h2.04V1.93H1.93Zm0%206.14V6.03h2.04v2.04H1.93Zm4.1%200V6.03h2.04v2.04H6.03Zm0-5.12a1.02%201.02%200%201%201%202.04%200%201.02%201.02%200%200%201-2.04%200Z'%20clip-rule='evenodd'/%3e%3cpath%20fill='%23FFD702'%20d='M7.05%201.93a1.02%201.02%200%201%200%200%202.04%201.02%201.02%200%200%200%200-2.04Z'/%3e%3c/svg%3e) Spaces](https://huggingface.co/spaces)