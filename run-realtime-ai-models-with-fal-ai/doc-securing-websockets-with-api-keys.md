Documentation

Real Time Models ⚡️

Keeping fal API Key and Secret Safe

Keeping fal API Secrets Safe[](#keeping-fal-api-secrets-safe)
-------------------------------------------------------------

Real-time models using WebSockets present challenges in ensuring the security of API secrets.

The WebSocket connection is established directly from the browser or native mobile application, making it unsafe to embed API keys and secrets directly into the client. To address this, we have developed additional tools to enable secure authentication with our servers without introducing unnecessary intermediaries between the client and our GPU servers. Instead of using traditional API keys, we recommend utilizing short-lived [JWT (opens in a new tab)](https://jwt.io/) tokens for authentication.

Easiest way to communicate with fal using websockets is through our [javascript (opens in a new tab)](https://github.com/fal-ai/fal-js) and [swift (opens in a new tab)](https://github.com/fal-ai/fal-swift) clients and a [server proxy](/docs/model-endpoints/server-side).

##### Server Side Proxy

Checkout our [Server Side Integration](/docs/model-endpoints/server-side#ready-to-use-proxy-implementations) section to learn more about using a ready made proxy with your Node.js or Next.js app or implement your own.

When `fal.realtime.connect` is invoked the fal client gets a short lived [JWT (opens in a new tab)](https://jwt.io/) token through a server proxy to authenticate with fal services. This token is refreshed automatically by the client when it is needed.

JavaScriptSWIFT

    import * as fal from "@fal-ai/serverless-client";

    fal.config({
      proxyUrl: "/api/fal/proxy",
    });
    const { send } = fal.realtime.connect("fal-ai/fast-lcm-diffusion", {
      connectionKey: "realtime-demo",
      throttleInterval: 128,
      onResult(result) {
        // display
      },
    });

Checkout the [FalRealtimeSampleApp (swift) (opens in a new tab)](https://github.com/fal-ai/fal-swift/tree/main/Sources/Samples/FalRealtimeSampleApp) and [realtime demo (js) (opens in a new tab)](https://github.com/fal-ai/fal-js/blob/main/apps/demo-nextjs-app-router/app/realtime/page.tsx) for more details.

Last updated on October 4, 2024

[Quickstart](/docs/real-time/quickstart "Quickstart")[Introduction](/docs/model-endpoints "Introduction")
