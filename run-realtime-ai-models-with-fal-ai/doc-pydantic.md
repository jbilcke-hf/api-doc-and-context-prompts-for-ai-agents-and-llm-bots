Documentation

Private Serverless Models on GPUs

Data Validation with Pydantic

### Passing arguments and leveraging Pydantic[](#passing-arguments-and-leveraging-pydantic)

fal Applications and FAST API are fully compatible with Pydantic. Any features of Pydantic used in fal endpoint arguments will also work.

Pydantic features can be used for data validation in your endpoint. In the example below, you can set some of the parameters as optional, set default values, and apply other types of validation such as constraints and types.

    import fal
    from pydantic import BaseModel
    from fal.toolkit import Image

    class ImageModelInput(BaseModel):
        seed: int | None = Field(
            default=None,
            description="""
                The same seed and the same prompt given to the same version of Stable Diffusion
                will output the same image every time.
            """,
            examples=[176400],
        )
        num_inference_steps: int = Field(
            default=25,
            description="""
                Increasing the amount of steps tell the model that it should take more steps
                to generate your final result which can increase the amount of detail in your image.
            """,
            gt=0,
            le=100,
        )

    class MyApp(fal.App(keep_alive=300)):
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
        def generate_image(self, request: ImageModelInput) -> Image:
            result = self.pipe(request.prompt, num_inference_steps=7, guidance_scale=3)
            image = Image.from_pil(result.images[0])
            return image


Last updated on October 4, 2024

[Setting Secrets](/docs/private-serverless-models/setting-secrets "Setting Secrets")[Optimizing Routing Behavior](/docs/private-serverless-models/hot-model-routing "Optimizing Routing Behavior")
