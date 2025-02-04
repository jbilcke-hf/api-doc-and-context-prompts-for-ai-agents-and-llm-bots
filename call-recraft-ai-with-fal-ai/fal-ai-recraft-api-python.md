1.  [Back to Gallery](/models)

Recraft V3 Text to Image
========================

Recraft V3

`fal-ai/recraft-v3`

Inference

Commercial use

Training

PlaygroundAPIExamplesMoreRequestsAnalytics

### Table of contents

Python

[

#### 1\. Calling the API

](/models/fal-ai/recraft-v3/api#api-call)

*   [Install the client](/models/fal-ai/recraft-v3/api#api-call-install)
*   [Setup your API Key](/models/fal-ai/recraft-v3/api#api-call-setup)
*   [Submit a request](/models/fal-ai/recraft-v3/api#api-call-submit-request)

[

#### 2\. Authentication

](/models/fal-ai/recraft-v3/api#auth)

*   [API Key](/models/fal-ai/recraft-v3/api#auth-api-key)

[

#### 3\. Queue

](/models/fal-ai/recraft-v3/api#queue)

*   [Submit a request](/models/fal-ai/recraft-v3/api#queue-submit)
*   [Fetch request status](/models/fal-ai/recraft-v3/api#queue-status)
*   [Get the result](/models/fal-ai/recraft-v3/api#queue-result)

[

#### 4\. Files

](/models/fal-ai/recraft-v3/api#files)

*   [Data URI (base64)](/models/fal-ai/recraft-v3/api#files-data-uri)
*   [Hosted files (URL)](/models/fal-ai/recraft-v3/api#files-from-url)
*   [Uploading files](/models/fal-ai/recraft-v3/api#files-upload)

[

#### 5\. Schema

](/models/fal-ai/recraft-v3/api#schema)

*   [Input](/models/fal-ai/recraft-v3/api#schema-input)
*   [Output](/models/fal-ai/recraft-v3/api#schema-output)
*   [Other](/models/fal-ai/recraft-v3/api#schema-other)

### About

State of the art Recraft V3 model by recraft.ai, use it as an API directly through fal.

### 1\. Calling the API[#](#api-call-install)

### Install the client[#](#api-call-install)

The client provides a convenient way to interact with the model API.

    pip install fal-client

### Setup your API Key[#](#api-call-setup)

Set `FAL_KEY` as an environment variable in your runtime.

    export FAL_KEY="YOUR_API_KEY"

### Submit a request[#](#api-call-submit-request)

The client API handles the API submit protocol. It will handle the request status updates and return the result when the request is completed.

PythonPython (async)

    import fal_client
    
    def on_queue_update(update):
        if isinstance(update, fal_client.InProgress):
            for log in update.logs:
               print(log["message"])
    
    result = fal_client.subscribe(
        "fal-ai/recraft-v3",
        arguments={
            "prompt": "a red panda eating a bamboo in front of a poster that says \"recraft V3 now available at fal\""
        },
        with_logs=True,
        on_queue_update=on_queue_update,
    )
    print(result)

2\. Authentication[#](#auth)
----------------------------

The API uses an API Key for authentication. It is recommended you set the `FAL_KEY` environment variable in your runtime when possible.

### API Key[#](#auth-api-key)

##### Protect your API Key

When running code on the client-side (e.g. in a browser, mobile app or GUI applications), make sure to not expose your `FAL_KEY`. Instead, **use a server-side proxy** to make requests to the API. For more information, check out our [server-side integration guide](https://docs.fal.ai/model-endpoints/server-side).

3\. Queue[#](#queue)
--------------------

##### Long-running requests

For long-running requests, such as _training_ jobs or models with slower inference times, it is recommended to check the [Queue](https://docs.fal.ai/model-endpoints/queue) status and rely on [Webhooks](https://docs.fal.ai/model-endpoints/webhooks) instead of blocking while waiting for the result.

### Submit a request[#](#queue-submit)

The client API provides a convenient way to submit requests to the model.

PythonPython (async)

    import fal_client
    
    handler = fal_client.submit(
        "fal-ai/recraft-v3",
        arguments={
            "prompt": "a red panda eating a bamboo in front of a poster that says \"recraft V3 now available at fal\""
        },
        webhook_url="https://optional.webhook.url/for/results",
    )
    
    request_id = handler.request_id

### Fetch request status[#](#queue-status)

You can fetch the status of a request to check if it is completed or still in progress.

PythonPython (async)

    status = fal_client.status("fal-ai/recraft-v3", request_id, with_logs=True)

### Get the result[#](#queue-result)

Once the request is completed, you can fetch the result. See the [Output Schema](#schema-output) for the expected result format.

PythonPython (async)

    result = fal_client.result("fal-ai/recraft-v3", request_id)

4\. Files[#](#files)
--------------------

Some attributes in the API accept file URLs as input. Whenever that's the case you can pass your own URL or a Base64 data URI.

### Data URI (base64)[#](#files-data-uri)

You can pass a Base64 data URI as a file input. The API will handle the file decoding for you. Keep in mind that for large files, this alternative although convenient can impact the request performance.

### Hosted files (URL)[#](#files-from-url)

You can also pass your own URLs as long as they are publicly accessible. Be aware that some hosts might block cross-site requests, rate-limit, or consider the request as a bot.

### Uploading files[#](#files-upload)

We provide a convenient file storage that allows you to upload files and use them in your requests. You can upload files using the client API and use the returned URL in your requests.

PythonPython (async)

    url = fal_client.upload_file("path/to/file")

Read more about file handling in our [file upload guide](https://docs.fal.ai/model-endpoints#file-uploads).

5\. Schema[#](#schema)
----------------------

### Input[#](#schema-input)

`prompt` `string`\* required

`image_size` `[ImageSize](#type-ImageSize) | [Enum](#type-Enum)`

Default value: `square_hd`

Possible enum values: `square_hd, square, portrait_4_3, portrait_16_9, landscape_4_3, landscape_16_9`

**Note:** For custom image sizes, you can pass the `width` and `height` as an object:

    "image_size": {
      "width": 1280,
      "height": 720
    }

`style` `StyleEnum`

The style of the generated images. Vector images cost 2X as much. Default value: `"realistic_image"`

Possible enum values: `any, realistic_image, digital_illustration, vector_illustration, realistic_image/b_and_w, realistic_image/hard_flash, realistic_image/hdr, realistic_image/natural_light, realistic_image/studio_portrait, realistic_image/enterprise, realistic_image/motion_blur, digital_illustration/pixel_art, digital_illustration/hand_drawn, digital_illustration/grain, digital_illustration/infantile_sketch, digital_illustration/2d_art_poster, digital_illustration/handmade_3d, digital_illustration/hand_drawn_outline, digital_illustration/engraving_color, digital_illustration/2d_art_poster_2, vector_illustration/engraving, vector_illustration/line_art, vector_illustration/line_circuit, vector_illustration/linocut`

`colors` `list<[RGBColor](#type-RGBColor)>`

An array of preferable colors Default value: \`\`

`style_id` `[string](#type-string) | [null](#type-null)`

The ID of the custom style reference (optional)

    {
      "prompt": "a red panda eating a bamboo in front of a poster that says \"recraft V3 now available at fal\"",
      "image_size": "square_hd",
      "style": "realistic_image",
      "colors": []
    }

### Output[#](#schema-output)

`images` `list<[File](#type-File)>`\* required

    {
      "images": [
        {
          "url": "https://fal.media/files/penguin/852yy3l5DGLmrwAK42RTB_image.webp"
        }
      ]
    }

### Other types[#](#schema-other)

#### ImageSize[#](#type-ImageSize)

`width` `integer`

The width of the generated image. Default value: `512`

`height` `integer`

The height of the generated image. Default value: `512`

#### RGBColor[#](#type-RGBColor)

`r` `integer`

Red color value

`g` `integer`

Green color value

`b` `integer`

Blue color value

#### File[#](#type-File)

`url` `string`\* required

The URL where the file can be downloaded from.

`content_type` `[string](#type-string) | [null](#type-null)`

The mime type of the file.

`file_name` `[string](#type-string) | [null](#type-null)`

The name of the file. It will be auto-generated if not provided.

`file_size` `[integer](#type-integer) | [null](#type-null)`

The size of the file in bytes.

### Related Models

[

fal-ai/flux-pro/v1.1

text-to-image

FLUX1.1 \[pro\] is an enhanced version of FLUX.1 \[pro\], improved image generation capabilities, delivering superior composition, detail, and artistic fidelity compared to its predecessor.

flux

pro

enhanced







](/models/fal-ai/flux-pro/v1.1)[

fal-ai/flux-general

text-to-image

A versatile endpoint for the FLUX.1 \[dev\] model that supports multiple AI extensions including LoRA, ControlNet conditioning, and IP-Adapter integration, enabling comprehensive control over image generation through various guidance methods.

flux

dev

lora







](/models/fal-ai/flux-general)[

fal-ai/fooocus/image-prompt

text-to-image

Default parameters with automated optimizations and quality improvements.

text to image

fooocus

image prompt







](/models/fal-ai/fooocus/image-prompt)