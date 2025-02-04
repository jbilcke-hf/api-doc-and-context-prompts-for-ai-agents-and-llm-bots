FileData
========

    gradio.FileData(···)

### Description[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#description)

The FileData class is a subclass of the GradioModel class that represents a file object within a Gradio interface. It is used to store file data and metadata when a file is uploaded.  

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Example Usage[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#example-usage)

    from gradio_client import Client, FileData, handle_file
    
    def get_url_on_server(data: FileData):
        print(data['url'])
    
    client = Client("gradio/gif_maker_main", download_files=False)
    job = client.submit([handle_file("./cheetah.jpg")], api_name="/predict")
    data = job.result()
    video: FileData = data['video']
    
    get_url_on_server(video)

### Attributes[![](https://raw.githubusercontent.com/gradio-app/gradio/main/js/_website/src/lib/assets/img/anchor.svg)](#attributes)

Parameters ▼

    path: str

The server file path where the file is stored.

    url: Optional[str]

The normalized server URL pointing to the file.

    size: Optional[int]

The size of the file in bytes.

    orig_name: Optional[str]

The original filename before upload.

    mime_type: Optional[str]

The MIME type of the file.

    is_stream: bool

Indicates whether the file is a stream.

    meta: dict

Additional metadata used internally (should not be changed).