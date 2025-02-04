Documentation

Private Serverless Models on GPUs

Real-time endpoints & WebSockets

Real-time endpoints & WebSockets[](#real-time-endpoints--websockets)
--------------------------------------------------------------------

For applications deployed on fal runtime; in addition to regular HTTP endpoints, developers might choose to implement auxiliary interfaces on top of raw WebSockets or fal's (stateless) real-time application framework.

Under a `fal.App`, for any endpoint that deal with real-time connectivity, `@fal.realtime()` decorator can be used instead of `@fal.endpoint` to automatically make the interface compatible with [fal's real-time clients (opens in a new tab)](https://www.fal.ai/docs/real-time#real-time-models). The functions do not provide any session state, and are meant to be used for reducing the overall latency (with fal's binary protocol) and eliminating fixed connection establishing overheads.

For power users who want to build stateful applications with their own real-time protocol, a `@fal.endpoint` can be initialized with `is_websocket=True` flag and the underlying function will receive the raw WebSocket connection and can choose to use it however it wants.

    import fal
    from pydantic import BaseModel

    class Input(BaseModel):
        prompt: str = Field()


    class Output(BaseModel):
        output: str = Field()


    class RealtimeApp(fal.App):
        @fal.endpoint("/")
        def generate(self, input: Input) -> Output:
            return Output(output=input.prompt)

        @fal.endpoint("/ws", is_websocket=True)
        async def generate_ws(self, websocket: WebSocket) -> None:
            await websocket.accept()
            for _ in range(3):
                await websocket.send_json({"message": "Hello world!"})
            await websocket.close()

        @fal.realtime("/realtime")
        def generate_rt(self, input: Input) -> Output:
            return Output(output=input.prompt)

Last updated on October 4, 2024

[Optimizing Routing Behavior](/docs/private-serverless-models/hot-model-routing "Optimizing Routing Behavior")[Optimize Models Using fal's Inference Engine](/docs/private-serverless-models/runtime-optimization "Optimize Models Using fal's Inference Engine")
