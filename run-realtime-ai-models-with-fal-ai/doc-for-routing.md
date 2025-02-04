Documentation

Private Serverless Models on GPUs

Optimizing Routing Behavior

Optimizing Routing Behavior[](#optimizing-routing-behavior)
-----------------------------------------------------------

When there are multiple available replicas of the same application, there isn't a defined behavior for picking which one to use for a particular request with the assumption that all replicas would behave identically for the given set of inputs.

This might not be true for applications which hold state and might include an in-memory cache for certain sets of parameters. For example, if you are serving an application that can run any diffusion model but only can keep 3 distinct models in memory, you want to minimize the number of cache misses (because loading that model from scratch incurs a significant performance penalty) depending on a user provided input.

This is where the semantically-aware routing hints come into play. Instead of treating each replica equally, applications can provide hints for specialization and allow fal's router to select the appropriate replica for a specific request. For this logic to work as efficiently, the user needs to provide a `X-Fal-Runner-Hint` header with a semantically identifying string hint and the application should implement a `provide_hints()` method that returns a list of hints. If there is a match in any of the replicas, fal's router will send the request to that replica. However, if there is no match, it will fall back to the standard routing algorithm.

    from typing import Any

    import fal
    from fal.toolkit import Image
    from pydantic import BaseModel

    class Input(BaseModel):
        model: str = Field()
        prompt: str = Field()


    class Output(BaseModel):
        image: Image = Field()


    class AnyModelRunner(fal.App):
        def setup(self) -> None:
            self.models = {}

        def provide_hints(self) -> list[str]:
            # Choose to specialize on already loaded models; at first this will be empty
            # so we'll be picked for any request, but as slowly the cache builds up, the
            # replica will be more preferable compared to others.
            return self.models.keys()

        def load_model(self, name: str) -> Any:
            from diffusers import DiffusionPipeline

            if name in self.models:
                return self.models[name]

            pipeline = DiffusionPipeline.from_pretrained(name)
            pipeline.to("cuda")

            self.models[name] = pipeline
            return pipeline

        @fal.endpoint("/")
        def run_model(self, input: Input) -> Output:
            model = self.load_model(input.model)
            result = model(input.prompt)
            return Output(image=Image.from_pil(result.images[0]))

Last updated on October 4, 2024

[Data Validation with Pydantic](/docs/private-serverless-models/pydantic "Data Validation with Pydantic")[Real-time endpoints & WebSockets](/docs/private-serverless-models/real-time-endpoints "Real-time endpoints & WebSockets")
