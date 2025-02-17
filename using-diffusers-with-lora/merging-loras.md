[](#merge-loras)Merge LoRAs
===========================

It can be fun and creative to use multiple [LoRAs]((https://huggingface.co/docs/peft/conceptual_guides/adapter#low-rank-adaptation-lora)) together to generate something entirely new and unique. This works by merging multiple LoRA weights together to produce images that are a blend of different styles. Diffusers provides a few methods to merge LoRAs depending on _how_ you want to merge their weights, which can affect image quality.

This guide will show you how to merge LoRAs using the [set\_adapters()](/docs/diffusers/v0.32.2/en/api/loaders/peft#diffusers.loaders.PeftAdapterMixin.set_adapters) and [add\_weighted\_adapter](https://huggingface.co/docs/peft/package_reference/lora#peft.LoraModel.add_weighted_adapter) methods. To improve inference speed and reduce memory-usage of merged LoRAs, you’ll also see how to use the `fuse_lora()` method to fuse the LoRA weights with the original weights of the underlying model.

For this guide, load a Stable Diffusion XL (SDXL) checkpoint and the [KappaNeuro/studio-ghibli-style](https://huggingface.co/KappaNeuro/studio-ghibli-style) and [Norod78/sdxl-chalkboarddrawing-lora](https://huggingface.co/Norod78/sdxl-chalkboarddrawing-lora) LoRAs with the [load\_lora\_weights()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_weights) method. You’ll need to assign each LoRA an `adapter_name` to combine them later.

Copied

from diffusers import DiffusionPipeline
import torch

pipeline = DiffusionPipeline.from\_pretrained("stabilityai/stable-diffusion-xl-base-1.0", torch\_dtype=torch.float16).to("cuda")
pipeline.load\_lora\_weights("ostris/ikea-instructions-lora-sdxl", weight\_name="ikea\_instructions\_xl\_v1\_5.safetensors", adapter\_name="ikea")
pipeline.load\_lora\_weights("lordjia/by-feng-zikai", weight\_name="fengzikai\_v1.0\_XL.safetensors", adapter\_name="feng")

[](#setadapters)set\_adapters
-----------------------------

The [set\_adapters()](/docs/diffusers/v0.32.2/en/api/loaders/peft#diffusers.loaders.PeftAdapterMixin.set_adapters) method merges LoRA adapters by concatenating their weighted matrices. Use the adapter name to specify which LoRAs to merge, and the `adapter_weights` parameter to control the scaling for each LoRA. For example, if `adapter_weights=[0.5, 0.5]`, then the merged LoRA output is an average of both LoRAs. Try adjusting the adapter weights to see how it affects the generated image!

Copied

pipeline.set\_adapters(\["ikea", "feng"\], adapter\_weights=\[0.7, 0.8\])

generator = torch.manual\_seed(0)
prompt = "A bowl of ramen shaped like a cute kawaii bear, by Feng Zikai"
image = pipeline(prompt, generator=generator, cross\_attention\_kwargs={"scale": 1.0}).images\[0\]
image

![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/diffusers/lora_merge_set_adapters.png)

[](#addweightedadapter)add\_weighted\_adapter
---------------------------------------------

This is an experimental method that adds PEFTs [add\_weighted\_adapter](https://huggingface.co/docs/peft/package_reference/lora#peft.LoraModel.add_weighted_adapter) method to Diffusers to enable more efficient merging methods. Check out this [issue](https://github.com/huggingface/diffusers/issues/6892) if you’re interested in learning more about the motivation and design behind this integration.

The [add\_weighted\_adapter](https://huggingface.co/docs/peft/package_reference/lora#peft.LoraModel.add_weighted_adapter) method provides access to more efficient merging method such as [TIES and DARE](https://huggingface.co/docs/peft/developer_guides/model_merging). To use these merging methods, make sure you have the latest stable version of Diffusers and PEFT installed.

Copied

pip install -U diffusers peft

There are three steps to merge LoRAs with the [add\_weighted\_adapter](https://huggingface.co/docs/peft/package_reference/lora#peft.LoraModel.add_weighted_adapter) method:

1.  Create a [PeftModel](https://huggingface.co/docs/peft/package_reference/peft_model#peft.PeftModel) from the underlying model and LoRA checkpoint.
2.  Load a base UNet model and the LoRA adapters.
3.  Merge the adapters using the [add\_weighted\_adapter](https://huggingface.co/docs/peft/package_reference/lora#peft.LoraModel.add_weighted_adapter) method and the merging method of your choice.

Let’s dive deeper into what these steps entail.

1.  Load a UNet that corresponds to the UNet in the LoRA checkpoint. In this case, both LoRAs use the SDXL UNet as their base model.

Copied

from diffusers import UNet2DConditionModel
import torch

unet = UNet2DConditionModel.from\_pretrained(
    "stabilityai/stable-diffusion-xl-base-1.0",
    torch\_dtype=torch.float16,
    use\_safetensors=True,
    variant="fp16",
    subfolder="unet",
).to("cuda")

Load the SDXL pipeline and the LoRA checkpoints, starting with the [ostris/ikea-instructions-lora-sdxl](https://huggingface.co/ostris/ikea-instructions-lora-sdxl) LoRA.

Copied

from diffusers import DiffusionPipeline

pipeline = DiffusionPipeline.from\_pretrained(
    "stabilityai/stable-diffusion-xl-base-1.0",
    variant="fp16",
    torch\_dtype=torch.float16,
    unet=unet
).to("cuda")
pipeline.load\_lora\_weights("ostris/ikea-instructions-lora-sdxl", weight\_name="ikea\_instructions\_xl\_v1\_5.safetensors", adapter\_name="ikea")

Now you’ll create a [PeftModel](https://huggingface.co/docs/peft/package_reference/peft_model#peft.PeftModel) from the loaded LoRA checkpoint by combining the SDXL UNet and the LoRA UNet from the pipeline.

Copied

from peft import get\_peft\_model, LoraConfig
import copy

sdxl\_unet = copy.deepcopy(unet)
ikea\_peft\_model = get\_peft\_model(
    sdxl\_unet,
    pipeline.unet.peft\_config\["ikea"\],
    adapter\_name="ikea"
)

original\_state\_dict = {f"base\_model.model.{k}": v for k, v in pipeline.unet.state\_dict().items()}
ikea\_peft\_model.load\_state\_dict(original\_state\_dict, strict=True)

You can optionally push the ikea\_peft\_model to the Hub by calling `ikea_peft_model.push_to_hub("ikea_peft_model", token=TOKEN)`.

Repeat this process to create a [PeftModel](https://huggingface.co/docs/peft/package_reference/peft_model#peft.PeftModel) from the [lordjia/by-feng-zikai](https://huggingface.co/lordjia/by-feng-zikai) LoRA.

Copied

pipeline.delete\_adapters("ikea")
sdxl\_unet.delete\_adapters("ikea")

pipeline.load\_lora\_weights("lordjia/by-feng-zikai", weight\_name="fengzikai\_v1.0\_XL.safetensors", adapter\_name="feng")
pipeline.set\_adapters(adapter\_names="feng")

feng\_peft\_model = get\_peft\_model(
    sdxl\_unet,
    pipeline.unet.peft\_config\["feng"\],
    adapter\_name="feng"
)

original\_state\_dict = {f"base\_model.model.{k}": v for k, v in pipe.unet.state\_dict().items()}
feng\_peft\_model.load\_state\_dict(original\_state\_dict, strict=True)

2.  Load a base UNet model and then load the adapters onto it.

Copied

from peft import PeftModel

base\_unet = UNet2DConditionModel.from\_pretrained(
    "stabilityai/stable-diffusion-xl-base-1.0",
    torch\_dtype=torch.float16,
    use\_safetensors=True,
    variant="fp16",
    subfolder="unet",
).to("cuda")

model = PeftModel.from\_pretrained(base\_unet, "stevhliu/ikea\_peft\_model", use\_safetensors=True, subfolder="ikea", adapter\_name="ikea")
model.load\_adapter("stevhliu/feng\_peft\_model", use\_safetensors=True, subfolder="feng", adapter\_name="feng")

3.  Merge the adapters using the [add\_weighted\_adapter](https://huggingface.co/docs/peft/package_reference/lora#peft.LoraModel.add_weighted_adapter) method and the merging method of your choice (learn more about other merging methods in this [blog post](https://huggingface.co/blog/peft_merging)). For this example, let’s use the `"dare_linear"` method to merge the LoRAs.

Keep in mind the LoRAs need to have the same rank to be merged!

Copied

model.add\_weighted\_adapter(
    adapters=\["ikea", "feng"\],
    weights=\[1.0, 1.0\],
    combination\_type="dare\_linear",
    adapter\_name="ikea-feng"
)
model.set\_adapters("ikea-feng")

Now you can generate an image with the merged LoRA.

Copied

model = model.to(dtype=torch.float16, device="cuda")

pipeline = DiffusionPipeline.from\_pretrained(
    "stabilityai/stable-diffusion-xl-base-1.0", unet=model, variant="fp16", torch\_dtype=torch.float16,
).to("cuda")

image = pipeline("A bowl of ramen shaped like a cute kawaii bear, by Feng Zikai", generator=torch.manual\_seed(0)).images\[0\]
image

![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/diffusers/ikea-feng-dare-linear.png)

[](#fuselora)fuse\_lora
-----------------------

Both the [set\_adapters()](/docs/diffusers/v0.32.2/en/api/loaders/peft#diffusers.loaders.PeftAdapterMixin.set_adapters) and [add\_weighted\_adapter](https://huggingface.co/docs/peft/package_reference/lora#peft.LoraModel.add_weighted_adapter) methods require loading the base model and the LoRA adapters separately which incurs some overhead. The [fuse\_lora()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.lora_base.LoraBaseMixin.fuse_lora) method allows you to fuse the LoRA weights directly with the original weights of the underlying model. This way, you’re only loading the model once which can increase inference and lower memory-usage.

You can use PEFT to easily fuse/unfuse multiple adapters directly into the model weights (both UNet and text encoder) using the [fuse\_lora()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.lora_base.LoraBaseMixin.fuse_lora) method, which can lead to a speed-up in inference and lower VRAM usage.

For example, if you have a base model and adapters loaded and set as active with the following adapter weights:

Copied

from diffusers import DiffusionPipeline
import torch

pipeline = DiffusionPipeline.from\_pretrained("stabilityai/stable-diffusion-xl-base-1.0", torch\_dtype=torch.float16).to("cuda")
pipeline.load\_lora\_weights("ostris/ikea-instructions-lora-sdxl", weight\_name="ikea\_instructions\_xl\_v1\_5.safetensors", adapter\_name="ikea")
pipeline.load\_lora\_weights("lordjia/by-feng-zikai", weight\_name="fengzikai\_v1.0\_XL.safetensors", adapter\_name="feng")

pipeline.set\_adapters(\["ikea", "feng"\], adapter\_weights=\[0.7, 0.8\])

Fuse these LoRAs into the UNet with the [fuse\_lora()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.lora_base.LoraBaseMixin.fuse_lora) method. The `lora_scale` parameter controls how much to scale the output by with the LoRA weights. It is important to make the `lora_scale` adjustments in the [fuse\_lora()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.lora_base.LoraBaseMixin.fuse_lora) method because it won’t work if you try to pass `scale` to the `cross_attention_kwargs` in the pipeline.

Copied

pipeline.fuse\_lora(adapter\_names=\["ikea", "feng"\], lora\_scale=1.0)

Then you should use [unload\_lora\_weights()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.lora_base.LoraBaseMixin.unload_lora_weights) to unload the LoRA weights since they’ve already been fused with the underlying base model. Finally, call [save\_pretrained()](/docs/diffusers/v0.32.2/en/api/pipelines/overview#diffusers.DiffusionPipeline.save_pretrained) to save the fused pipeline locally or you could call [push\_to\_hub()](/docs/diffusers/v0.32.2/en/api/pipelines/overview#diffusers.utils.PushToHubMixin.push_to_hub) to push the fused pipeline to the Hub.

Copied

pipeline.unload\_lora\_weights()
\# save locally
pipeline.save\_pretrained("path/to/fused-pipeline")
\# save to the Hub
pipeline.push\_to\_hub("fused-ikea-feng")

Now you can quickly load the fused pipeline and use it for inference without needing to separately load the LoRA adapters.

Copied

pipeline = DiffusionPipeline.from\_pretrained(
    "username/fused-ikea-feng", torch\_dtype=torch.float16,
).to("cuda")

image = pipeline("A bowl of ramen shaped like a cute kawaii bear, by Feng Zikai", generator=torch.manual\_seed(0)).images\[0\]
image

You can call `~~loaders.lora_base.LoraBaseMixin.unfuse_lora` to restore the original model’s weights (for example, if you want to use a different `lora_scale` value). However, this only works if you’ve only fused one LoRA adapter to the original model. If you’ve fused multiple LoRAs, you’ll need to reload the model.

Copied

pipeline.unfuse\_lora()

### [](#torchcompile)torch.compile

[torch.compile](../optimization/torch2.0#torchcompile) can speed up your pipeline even more, but the LoRA weights must be fused first and then unloaded. Typically, the UNet is compiled because it is such a computationally intensive component of the pipeline.

Copied

from diffusers import DiffusionPipeline
import torch

\# load base model and LoRAs
pipeline = DiffusionPipeline.from\_pretrained("stabilityai/stable-diffusion-xl-base-1.0", torch\_dtype=torch.float16).to("cuda")
pipeline.load\_lora\_weights("ostris/ikea-instructions-lora-sdxl", weight\_name="ikea\_instructions\_xl\_v1\_5.safetensors", adapter\_name="ikea")
pipeline.load\_lora\_weights("lordjia/by-feng-zikai", weight\_name="fengzikai\_v1.0\_XL.safetensors", adapter\_name="feng")

\# activate both LoRAs and set adapter weights
pipeline.set\_adapters(\["ikea", "feng"\], adapter\_weights=\[0.7, 0.8\])

\# fuse LoRAs and unload weights
pipeline.fuse\_lora(adapter\_names=\["ikea", "feng"\], lora\_scale=1.0)
pipeline.unload\_lora\_weights()

\# torch.compile
pipeline.unet.to(memory\_format=torch.channels\_last)
pipeline.unet = torch.compile(pipeline.unet, mode="reduce-overhead", fullgraph=True)

image = pipeline("A bowl of ramen shaped like a cute kawaii bear, by Feng Zikai", generator=torch.manual\_seed(0)).images\[0\]

Learn more about torch.compile in the [Accelerate inference of text-to-image diffusion models](../tutorials/fast_diffusion#torchcompile) guide.

[](#next-steps)Next steps
-------------------------

For more conceptual details about how each merging method works, take a look at the [🤗 PEFT welcomes new merging methods](https://huggingface.co/blog/peft_merging#concatenation-cat) blog post!

[< \> Update on GitHub](https://github.com/huggingface/diffusers/blob/main/docs/source/en/using-diffusers/merge_loras.md)