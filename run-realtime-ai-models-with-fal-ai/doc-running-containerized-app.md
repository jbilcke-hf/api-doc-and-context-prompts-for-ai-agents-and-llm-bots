Documentation

Private Serverless Models on GPUs

Running a Containerized Model

Running a containerized application[](#running-a-containerized-application)
---------------------------------------------------------------------------

The easiest way to understand how to run a containerized application is to see an example. Let's convert the example from the [previous section](/docs/private-serverless-models/runtime-optimization) into a containerized application.

##### Container support basics

Check out the [running a fal function in a container](/docs/examples/running-a-container) example for understanding the basics of running a containerized application.

    import fal
    import fal.toolkit
    from fal.container import ContainerImage
    from fal.toolkit import Image

    from pydantic import BaseModel, Field

    dockerfile_str = """
    FROM python:3.11

    RUN apt-get update && apt-get install -y ffmpeg
    RUN pip install "accelerate" "transformers>=4.30.2" "diffusers>=0.26" "torch>=2.2.0"
    """


    class Input(BaseModel):
        prompt: str = Field(
            description="The prompt to generate an image from.",
            examples=[
                "A cinematic shot of a baby racoon wearing an intricate italian priest robe.",
            ],
        )


    class Output(BaseModel):
        image: Image = Field(
            description="The generated image.",
        )


    class FalModel(
        fal.App,
        image=ContainerImage.from_dockerfile_str(dockerfile_str),
        kind="container",
      ):
        machine_type = "GPU"

        def setup(self) -> None:
            import torch
            from diffusers import AutoPipelineForText2Image

            # Load SDXL
            self.pipeline = AutoPipelineForText2Image.from_pretrained(
                "stabilityai/stable-diffusion-xl-base-1.0",
                torch_dtype=torch.float16,
                variant="fp16",
            )
            self.pipeline.to("cuda")

            # Apply fal's spatial optimizer to the pipeline.
            self.pipeline.unet = fal.toolkit.optimize(self.pipeline.unet)
            self.pipeline.vae = fal.toolkit.optimize(self.pipeline.vae)

            # Warm up the model.
            self.pipeline(
                prompt="a cat",
                num_inference_steps=30,
            )

        @fal.endpoint("/")
        def text_to_image(self, input: Input) -> Output:
            result = self.pipeline(
                prompt=input.prompt,
                num_inference_steps=30,
            )
            [image] = result.images
            return Output(image=Image.from_pil(image))

Voila! 🎉 The highlighted changes are the only modifications you need to make; the rest remains your familiar fal application.

##### Dockerfile Keywords

Please check our [Dockerfile best practices](/docs/guidelines/dockerfile) for more information on how to optimize your Dockerfile.

Last updated on October 4, 2024

[Optimize Models Using fal's Inference Engine](/docs/private-serverless-models/runtime-optimization "Optimize Models Using fal's Inference Engine")[Auth methods](/docs/authentication "Auth methods")
