Documentation

Private Serverless Models on GPUs

Optimize Models Using fal's Inference Engine

Runtime Model Optimizations[](#runtime-model-optimizations)
-----------------------------------------------------------

fal's inference engine bindings takes a torch module and applies all relevant dynamic compilation and quantization techniques to make it faster out of the box without leaking any of the complexity to the user.

This API is currently experimental, and might be subject to change in the future.

Example usage:

    import fal
    import fal.toolkit
    from fal.toolkit import Image
    from pydantic import BaseModel, Field


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


    class FalModel(fal.App):
        machine_type = "GPU"
        requirements = [
            "accelerate",
            "transformers>=4.30.2",
            "diffusers>=0.26",
            "torch>=2.2.0",
        ]

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

Last updated on October 4, 2024

[Real-time endpoints & WebSockets](/docs/private-serverless-models/real-time-endpoints "Real-time endpoints & WebSockets")[Running a Containerized Model](/docs/private-serverless-models/running-containerized-model "Running a Containerized Model")
