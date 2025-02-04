DeletedFileData
===============

    gradio.DeletedFileData(···)

### Description[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#description)

The gr.DeletedFileData class is a subclass of gr.EventData that specifically carries information about the `.delete()` event. When gr.DeletedFileData is added as a type hint to an argument of an event listener method, a gr.DeletedFileData object will automatically be passed as the value of that argument. The attributes of this object contains information about the event that triggered the listener.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Example Usage[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#example-usage)

    import gradio as gr
    
    def test(delete_data: gr.DeletedFileData):
        return delete_data.file.path
    
    with gr.Blocks() as demo:
        files = gr.File(file_count="multiple")
        deleted_file = gr.File()
        files.delete(test, None, deleted_file)
    
    demo.launch()

### Attributes[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#attributes)

Parameters ▼

    file: FileData

The file that was deleted, as a FileData object. The str path to the file can be retrieved with the .path attribute.

### Demos[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#demos)

file\_component\_events

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

⌄

import gradio as gr

  

def delete\_file(n: int, file: gr.DeletedFileData):

return \[file.file.path, n + 1\]

  

with gr.Blocks() as demo:

  

with gr.Row():

with gr.Column():

file\_component \= gr.File(label\="Upload Single File", file\_count\="single")

with gr.Column():

output\_file\_1 \= gr.File(

label\="Upload Single File Output", file\_count\="single"

)

num\_load\_btn\_1 \= gr.Number(label\="# Load Upload Single File", value\=0)

file\_component.upload(

lambda s, n: (s, n + 1),

\[file\_component, num\_load\_btn\_1\],

\[output\_file\_1, num\_load\_btn\_1\],

)

with gr.Row():

with gr.Column():

file\_component\_multiple \= gr.File(

label\="Upload Multiple Files", file\_count\="multiple"

)

with gr.Column():

output\_file\_2 \= gr.File(

label\="Upload Multiple Files Output", file\_count\="multiple"

)

num\_load\_btn\_2 \= gr.Number(label\="# Load Upload Multiple Files", value\=0)

file\_component\_multiple.upload(

lambda s, n: (s, n + 1),

\[file\_component\_multiple, num\_load\_btn\_2\],

\[output\_file\_2, num\_load\_btn\_2\],

)

with gr.Row():

Chargement...

    import gradio as gr
    
    def delete_file(n: int, file: gr.DeletedFileData):
        return [file.file.path, n + 1]
    
    with gr.Blocks() as demo:
    
        with gr.Row():
            with gr.Column():
                file_component = gr.File(label="Upload Single File", file_count="single")
            with gr.Column():
                output_file_1 = gr.File(
                    label="Upload Single File Output", file_count="single"
                )
                num_load_btn_1 = gr.Number(label="# Load Upload Single File", value=0)
                file_component.upload(
                    lambda s, n: (s, n + 1),
                    [file_component, num_load_btn_1],
                    [output_file_1, num_load_btn_1],
                )
        with gr.Row():
            with gr.Column():
                file_component_multiple = gr.File(
                    label="Upload Multiple Files", file_count="multiple"
                )
            with gr.Column():
                output_file_2 = gr.File(
                    label="Upload Multiple Files Output", file_count="multiple"
                )
                num_load_btn_2 = gr.Number(label="# Load Upload Multiple Files", value=0)
                file_component_multiple.upload(
                    lambda s, n: (s, n + 1),
                    [file_component_multiple, num_load_btn_2],
                    [output_file_2, num_load_btn_2],
                )
        with gr.Row():
            with gr.Column():
                file_component_specific = gr.File(
                    label="Upload Multiple Files Image/Video",
                    file_count="multiple",
                    file_types=["image", "video"],
                )
            with gr.Column():
                output_file_3 = gr.File(
                    label="Upload Multiple Files Output Image/Video", file_count="multiple"
                )
                num_load_btn_3 = gr.Number(
                    label="# Load Upload Multiple Files Image/Video", value=0
                )
                file_component_specific.upload(
                    lambda s, n: (s, n + 1),
                    [file_component_specific, num_load_btn_3],
                    [output_file_3, num_load_btn_3],
                )
        with gr.Row():
            with gr.Column():
                file_component_pdf = gr.File(label="Upload PDF File", file_types=[".pdf"])
            with gr.Column():
                output_file_4 = gr.File(label="Upload PDF File Output")
                num_load_btn_4 = gr.Number(label="# Load Upload PDF File", value=0)
                file_component_pdf.upload(
                    lambda s, n: (s, n + 1),
                    [file_component_pdf, num_load_btn_4],
                    [output_file_4, num_load_btn_4],
                )
        with gr.Row():
            with gr.Column():
                file_component_invalid = gr.File(
                    label="Upload File with Invalid file_types",
                    file_types=["invalid file_type"],
                )
            with gr.Column():
                output_file_5 = gr.File(label="Upload File with Invalid file_types Output")
                num_load_btn_5 = gr.Number(
                    label="# Load Upload File with Invalid file_types", value=0
                )
                file_component_invalid.upload(
                    lambda s, n: (s, n + 1),
                    [file_component_invalid, num_load_btn_5],
                    [output_file_5, num_load_btn_5],
                )
        with gr.Row():
            with gr.Column():
                del_file_input = gr.File(label="Delete File", file_count="multiple")
            with gr.Column():
                del_file_data = gr.Textbox(label="Delete file data")
                num_load_btn_6 = gr.Number(label="# Deleted File", value=0)
                del_file_input.delete(
                    delete_file,
                    [num_load_btn_6],
                    [del_file_data, num_load_btn_6],
                )
        # f = gr.File(label="Upload many File", file_count="multiple")
        # # f.delete(delete_file)
        # f.delete(delete_file, inputs=None, outputs=None)
    
    if __name__ == "__main__":
        demo.launch()
    

Chargement...

[gradio/file\_component\_events](https://huggingface.co/spaces/gradio/file_component_events) Construit avec [Gradio](https://gradio.app). Hosted on [![Hugging Face Space](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='10'%20height='10'%20fill='none'%3e%3cpath%20fill='%23FF3270'%20d='M1.93%206.03v2.04h2.04V6.03H1.93Z'/%3e%3cpath%20fill='%23861FFF'%20d='M6.03%206.03v2.04h2.04V6.03H6.03Z'/%3e%3cpath%20fill='%23097EFF'%20d='M1.93%201.93v2.04h2.04V1.93H1.93Z'/%3e%3cpath%20fill='%23000'%20fill-rule='evenodd'%20d='M.5%201.4c0-.5.4-.9.9-.9h3.1a.9.9%200%200%201%20.87.67A2.44%202.44%200%200%201%209.5%202.95c0%20.65-.25%201.24-.67%201.68.39.1.67.46.67.88v3.08c0%20.5-.4.91-.9.91H1.4a.9.9%200%200%201-.9-.9V1.4Zm1.43.53v2.04h2.04V1.93H1.93Zm0%206.14V6.03h2.04v2.04H1.93Zm4.1%200V6.03h2.04v2.04H6.03Zm0-5.12a1.02%201.02%200%201%201%202.04%200%201.02%201.02%200%200%201-2.04%200Z'%20clip-rule='evenodd'/%3e%3cpath%20fill='%23FFD702'%20d='M7.05%201.93a1.02%201.02%200%201%200%200%202.04%201.02%201.02%200%200%200%200-2.04Z'/%3e%3c/svg%3e) Spaces](https://huggingface.co/spaces)