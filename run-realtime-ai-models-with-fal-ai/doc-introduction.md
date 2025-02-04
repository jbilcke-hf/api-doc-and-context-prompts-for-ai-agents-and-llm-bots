Documentation

Private Serverless Models on GPUs

Introduction

Introduction to Private Serverless Models[](#introduction-to-private-serverless-models)
---------------------------------------------------------------------------------------

In addition to using our blazing-fast public API endpoints you can also take advantage of fal's infrastructure for your private AI models. This section explains how to deploy a custom private AI model to fal's infrastructure.

##### Enterprise

Private Models are an Enterprise feature, please email [support@fal.ai](mailto:support@fal.ai) to get access.

#### Install the fal sdk python package[](#install-the-fal-sdk-python-package)

    pip install fal

### Speed run Stable Diffusion[](#speed-run-stable-diffusion)

The example below uses the `diffusers` library to run a simple stable diffusion pipeline.

    import fal
    from pydantic import BaseModel
    from fal.toolkit import Image


    class Input(BaseModel):
        prompt: str


    class Output(BaseModel):
        image: Image


    class MyApp(fal.App, keep_alive=300):
        machine_type = "GPU-A100"
        requirements = [
            "diffusers==0.28.0",
            "torch==2.3.0",
            "accelerate",
            "transformers",
        ]

        def setup(self):
            import torch
            from diffusers import StableDiffusionXLPipeline, DPMSolverSinglestepScheduler

            self.pipe = StableDiffusionXLPipeline.from_pretrained(
                "sd-community/sdxl-flash",
                torch_dtype=torch.float16,
            ).to("cuda")
            self.pipe.scheduler = DPMSolverSinglestepScheduler.from_config(
                self.pipe.scheduler.config,
                timestep_spacing="trailing",
            )

        @fal.endpoint("/")
        def run(self, request: Input) -> Output:
            result = self.pipe(request.prompt, num_inference_steps=7, guidance_scale=3)
            image = Image.from_pil(result.images[0])
            return Output(image=image)

    fal run example.py::MyApp

First time you run this application, `fal` will create a virtual environment that satisfies the requirements specified in the `requirements` variable. This environment will be cached and used for each subsequent invocation of the API.

    Access your exposed service at https://fal.run/1714827/4c5223d8-6943-47cb-8401-76c031ea222e

Once you see the message above, your application is ready to accept requests!

    curl -X POST https://fal.run/1714827/4c5223d8-6943-47cb-8401-76c031ea222e -H "Content-Type: application/json" -d '{"prompt":"rhino"}'

In this code:

*   `MyApp` is a class that inherits from `fal.App`. This structure allows the creation of a complex application with multiple endpoints, which are defined using the `@fal.endpoint` decorator.

*   `machine_type` is a class attribute that specifies the type of machine on which this application will run. Here, `"GPU-A100"` is specified.

*   `requirements` is another class attribute that lists the dependencies needed for the application to run. In this case, `"my_requirements"` is a placeholder for actual dependencies.

*   The `setup()` method is overridden to initialize the models used in the application. This method is executed once when the application is started.

*   The `@fal.endpoint` decorator is used to define the routes or endpoints of the application. In this example, only one endpoint is defined: `"/"`.


### Deploying your application[](#deploying-your-application)

Once your application is ready for deployment, you can use the fal CLI to deploy it:

    fal deploy example.py::MyApp

In this command, we instruct fal to deploy the `MyApp` class from example.py as an application.

Upon successful deployment, fal will provide a URL, for example, [https://fal.run/777/my\_app (opens in a new tab)](https://fal.run/777/my_app). This URL is the public access point to your deployed application, allowing you to interact with the API endpoints defined within your `MyApp` class.

### Setup Functions and `keep_alive`[](#setup-functions-and-keep_alive)

#### `keep_alive`[](#keep_alive)

"keep\_alive" is a configuration setting that enables the server to continue running even when there are no active requests. By setting `keep_alive`, you can ensure that if you hit the same application within the specified time frame, you can avoid incurring any overhead at all. "keep\_alive" is measured in seconds, in the example below the application will keep running for at least 300 seconds after the last request.

    class MyApp(fal.App, keep_alive=300):
       ...

#### setup()[](#setup)

When managing AI workloads, it's vital to prevent the same model from being reloaded into memory each time the serverless application is invoked. Each application can define a setup() function. This function is invoked once during application startup, and its result is cached in memory for the entire server lifecycle.

    class MyApp(fal.App, keep_alive=300):
        machine_type = "GPU-A100"
        requirements = [
            "diffusers==0.28.0",
            "torch==2.3.0",
            "accelerate",
            "transformers",
        ]

        def setup(self):
            import torch
            from diffusers import StableDiffusionXLPipeline, DPMSolverSinglestepScheduler

            self.pipe = StableDiffusionXLPipeline.from_pretrained(
                "sd-community/sdxl-flash",
                torch_dtype=torch.float16,
            ).to("cuda")
            self.pipe.scheduler = DPMSolverSinglestepScheduler.from_config(
                self.pipe.scheduler.config,
                timestep_spacing="trailing",
            )

### Min/Max Concurrency[](#minmax-concurrency)

fal applications have a simple managed autoscaling system. You can configure the autoscaling behavior through `min_concurrency` and `max_concurrency`.

    class MyApp(fal.App, keep_alive=300, min_concurrency=1, max_concurrency=5):
       ...

`min_concurrency` - indicated the number of replicas the system should maintain when there are no requests. `max_concurrency` - indicates the maximum number of replicas the system should have. Once this limit is reached, all subsequent requests are placed in a managed queue.

Last updated on October 4, 2024

[Dart (Flutter)](/docs/clients/dart "Dart (Flutter)")[Accessing Persistent Storage](/docs/private-serverless-models/accessing-persistent-storage "Accessing Persistent Storage")
