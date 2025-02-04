fal.ai Python client
====================

This is a Python client library for interacting with ML models deployed on [fal.ai](https://fal.ai).

Getting started
---------------

To install the client, run:

pip install fal-client

To use the client, you need to have an API key. You can get one by signing up at [fal.ai](https://fal.ai). Once you have it, set it as an environment variable:

export FAL\_KEY\=your-api-key

Now you can use the client to interact with your models. Here's an example of how to use it:

import fal\_client

response \= fal\_client.run("fal-ai/fast-sdxl", arguments\={"prompt": "a cute cat, realistic, orange"})
print(response\["images"\]\[0\]\["url"\])

Asynchronous requests
---------------------

The client also supports asynchronous requests out of the box. Here's an example:

import asyncio
import fal\_client

async def main():
    response \= await fal\_client.run\_async("fal-ai/fast-sdxl", arguments\={"prompt": "a cute cat, realistic, orange"})
    print(response\["images"\]\[0\]\["url"\])

asyncio.run(main())

Uploading files
---------------

If the model requires files as input, you can upload them directly to fal.media (our CDN) and pass the URLs to the client. Here's an example:

import fal\_client

audio\_url \= fal\_client.upload\_file("path/to/audio.wav")
response \= fal\_client.run("fal-ai/whisper", arguments\={"audio\_url": audio\_url})
print(response\["text"\])

Encoding files as in-memory data URLs
-------------------------------------

If you don't want to upload your file to our CDN service (for latency reasons, for example), you can encode it as a data URL and pass it directly to the client. Here's an example:

import fal\_client

audio\_data\_url \= fal\_client.encode\_file("path/to/audio.wav")
response \= fal\_client.run("fal-ai/whisper", arguments\={"audio\_url": audio\_data\_url})
print(response\["text"\])

Queuing requests
----------------

When you want to send a request and keep receiving updates on its status, you can use the `submit` method. Here's an example:

import asyncio
import fal\_client

async def main():
    response \= await fal\_client.submit\_async("fal-ai/fast-sdxl", arguments\={"prompt": "a cute cat, realistic, orange"})

    logs\_index \= 0
    async for event in response.iter\_events(with\_logs\=True):
        if isinstance(event, fal\_client.Queued):
            print("Queued. Position:", event.position)
        elif isinstance(event, (fal\_client.InProgress, fal\_client.Completed)):
            new\_logs \= event.logs\[logs\_index:\]
            for log in new\_logs:
                print(log\["message"\])
            logs\_index \= len(event.logs)

    result \= await response.get()
    print(result\["images"\]\[0\]\["url"\])

asyncio.run(main())