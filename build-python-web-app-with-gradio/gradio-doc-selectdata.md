SelectData
==========

    gradio.SelectData(···)

### Description[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#description)

The gr.SelectData class is a subclass of gr.EventData that specifically carries information about the `.select()` event. When gr.SelectData is added as a type hint to an argument of an event listener method, a gr.SelectData object will automatically be passed as the value of that argument. The attributes of this object contains information about the event that triggered the listener.  

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Example Usage[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#example-usage)

    import gradio as gr
    
    with gr.Blocks() as demo:
        table = gr.Dataframe([[1, 2, 3], [4, 5, 6]])
        gallery = gr.Gallery([("cat.jpg", "Cat"), ("dog.jpg", "Dog")])
        textbox = gr.Textbox("Hello World!")
        statement = gr.Textbox()
    
        def on_select(evt: gr.SelectData):
            return f"You selected {evt.value} at {evt.index} from {evt.target}"
    
        table.select(on_select, table, statement)
        gallery.select(on_select, gallery, statement)
        textbox.select(on_select, textbox, statement)
    
    demo.launch()

### Attributes[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#attributes)

Parameters ▼

    index: int | tuple[int, int]

The index of the selected item. Is a tuple if the component is two dimensional or selection is a range.

    value: Any

The value of the selected item.

    selected: bool

True if the item was selected, False if deselected.

### Demos[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#demos)

gallery\_selectionstictactoe

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

import gradio as gr

import numpy as np

  

with gr.Blocks() as demo:

imgs \= gr.State()

gallery \= gr.Gallery(allow\_preview\=False)

  

def deselect\_images():

return gr.Gallery(selected\_index\=None)

  

def generate\_images():

images \= \[\]

for \_ in range(9):

image \= np.ones((100, 100, 3), dtype\=np.uint8) \* np.random.randint(

0, 255, 3

) \# image is a solid single color

images.append(image)

return images, images

  

demo.load(generate\_images, None, \[gallery, imgs\])

  

with gr.Row():

selected \= gr.Number(show\_label\=False)

darken\_btn \= gr.Button("Darken selected")

deselect\_button \= gr.Button("Deselect")

  

deselect\_button.click(deselect\_images, None, gallery)

  

def get\_select\_index(evt: gr.SelectData):

return evt.index

  

gallery.select(get\_select\_index, None, selected)

  

def darken\_img(imgs, index):

index \= int(index)

imgs\[index\] \= np.round(imgs\[index\] \* 0.8).astype(np.uint8)

Loading...

    import gradio as gr
    import numpy as np
    
    with gr.Blocks() as demo:
        imgs = gr.State()
        gallery = gr.Gallery(allow_preview=False)
    
        def deselect_images():
            return gr.Gallery(selected_index=None)
    
        def generate_images():
            images = []
            for _ in range(9):
                image = np.ones((100, 100, 3), dtype=np.uint8) * np.random.randint(
                    0, 255, 3
                )  # image is a solid single color
                images.append(image)
            return images, images
    
        demo.load(generate_images, None, [gallery, imgs])
    
        with gr.Row():
            selected = gr.Number(show_label=False)
            darken_btn = gr.Button("Darken selected")
        deselect_button = gr.Button("Deselect")
    
        deselect_button.click(deselect_images, None, gallery)
    
        def get_select_index(evt: gr.SelectData):
            return evt.index
    
        gallery.select(get_select_index, None, selected)
    
        def darken_img(imgs, index):
            index = int(index)
            imgs[index] = np.round(imgs[index] * 0.8).astype(np.uint8)
            return imgs, imgs
    
        darken_btn.click(darken_img, [imgs, selected], [imgs, gallery])
    
    if __name__ == "__main__":
        demo.launch()
    

Loading...

[gradio/gallery\_selections](https://huggingface.co/spaces/gradio/gallery_selections) built with [Gradio](https://gradio.app). Hosted on [![Hugging Face Space](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='10'%20height='10'%20fill='none'%3e%3cpath%20fill='%23FF3270'%20d='M1.93%206.03v2.04h2.04V6.03H1.93Z'/%3e%3cpath%20fill='%23861FFF'%20d='M6.03%206.03v2.04h2.04V6.03H6.03Z'/%3e%3cpath%20fill='%23097EFF'%20d='M1.93%201.93v2.04h2.04V1.93H1.93Z'/%3e%3cpath%20fill='%23000'%20fill-rule='evenodd'%20d='M.5%201.4c0-.5.4-.9.9-.9h3.1a.9.9%200%200%201%20.87.67A2.44%202.44%200%200%201%209.5%202.95c0%20.65-.25%201.24-.67%201.68.39.1.67.46.67.88v3.08c0%20.5-.4.91-.9.91H1.4a.9.9%200%200%201-.9-.9V1.4Zm1.43.53v2.04h2.04V1.93H1.93Zm0%206.14V6.03h2.04v2.04H1.93Zm4.1%200V6.03h2.04v2.04H6.03Zm0-5.12a1.02%201.02%200%201%201%202.04%200%201.02%201.02%200%200%201-2.04%200Z'%20clip-rule='evenodd'/%3e%3cpath%20fill='%23FFD702'%20d='M7.05%201.93a1.02%201.02%200%201%200%200%202.04%201.02%201.02%200%200%200%200-2.04Z'/%3e%3c/svg%3e) Spaces](https://huggingface.co/spaces)

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

⌄

import gradio as gr

  

with gr.Blocks() as demo:

turn \= gr.Textbox("X", interactive\=False, label\="Turn")

board \= gr.Dataframe(value\=\[\["", "", ""\]\] \* 3, interactive\=False, type\="array")

  

def place(board: list\[list\[int\]\], turn, evt: gr.SelectData):

if evt.value:

return board, turn

board\[evt.index\[0\]\]\[evt.index\[1\]\] \= turn

turn \= "O" if turn \== "X" else "X"

return board, turn

  

board.select(place, \[board, turn\], \[board, turn\], show\_progress\="hidden")

  

if \_\_name\_\_ \== "\_\_main\_\_":

demo.launch()

Loading...

    import gradio as gr
    
    with gr.Blocks() as demo:
        turn = gr.Textbox("X", interactive=False, label="Turn")
        board = gr.Dataframe(value=[["", "", ""]] * 3, interactive=False, type="array")
    
        def place(board: list[list[int]], turn, evt: gr.SelectData):  
            if evt.value:
                return board, turn
            board[evt.index[0]][evt.index[1]] = turn
            turn = "O" if turn == "X" else "X"
            return board, turn
    
        board.select(place, [board, turn], [board, turn], show_progress="hidden")
    
    if __name__ == "__main__":
        demo.launch()
    

Loading...

[gradio/tictactoe](https://huggingface.co/spaces/gradio/tictactoe) built with [Gradio](https://gradio.app). Hosted on [![Hugging Face Space](data:image/svg+xml,%3csvg%20xmlns='http://www.w3.org/2000/svg'%20width='10'%20height='10'%20fill='none'%3e%3cpath%20fill='%23FF3270'%20d='M1.93%206.03v2.04h2.04V6.03H1.93Z'/%3e%3cpath%20fill='%23861FFF'%20d='M6.03%206.03v2.04h2.04V6.03H6.03Z'/%3e%3cpath%20fill='%23097EFF'%20d='M1.93%201.93v2.04h2.04V1.93H1.93Z'/%3e%3cpath%20fill='%23000'%20fill-rule='evenodd'%20d='M.5%201.4c0-.5.4-.9.9-.9h3.1a.9.9%200%200%201%20.87.67A2.44%202.44%200%200%201%209.5%202.95c0%20.65-.25%201.24-.67%201.68.39.1.67.46.67.88v3.08c0%20.5-.4.91-.9.91H1.4a.9.9%200%200%201-.9-.9V1.4Zm1.43.53v2.04h2.04V1.93H1.93Zm0%206.14V6.03h2.04v2.04H1.93Zm4.1%200V6.03h2.04v2.04H6.03Zm0-5.12a1.02%201.02%200%201%201%202.04%200%201.02%201.02%200%200%201-2.04%200Z'%20clip-rule='evenodd'/%3e%3cpath%20fill='%23FFD702'%20d='M7.05%201.93a1.02%201.02%200%201%200%200%202.04%201.02%201.02%200%200%200%200-2.04Z'/%3e%3c/svg%3e) Spaces](https://huggingface.co/spaces)