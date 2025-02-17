[](#lora)LoRA
=============

LoRA is a fast and lightweight training method that inserts and trains a significantly smaller number of parameters instead of all the model parameters. This produces a smaller file (~100 MBs) and makes it easier to quickly train a model to learn a new concept. LoRA weights are typically loaded into the denoiser, text encoder or both. The denoiser usually corresponds to a UNet ([UNet2DConditionModel](/docs/diffusers/v0.32.2/en/api/models/unet2d-cond#diffusers.UNet2DConditionModel), for example) or a Transformer ([SD3Transformer2DModel](/docs/diffusers/v0.32.2/en/api/models/sd3_transformer2d#diffusers.SD3Transformer2DModel), for example). There are several classes for loading LoRA weights:

*   `StableDiffusionLoraLoaderMixin` provides functions for loading and unloading, fusing and unfusing, enabling and disabling, and more functions for managing LoRA weights. This class can be used with any model.
*   `StableDiffusionXLLoraLoaderMixin` is a [Stable Diffusion (SDXL)](../../api/pipelines/stable_diffusion/stable_diffusion_xl) version of the `StableDiffusionLoraLoaderMixin` class for loading and saving LoRA weights. It can only be used with the SDXL model.
*   `SD3LoraLoaderMixin` provides similar functions for [Stable Diffusion 3](https://huggingface.co/blog/sd3).
*   `FluxLoraLoaderMixin` provides similar functions for [Flux](https://huggingface.co/docs/diffusers/main/en/api/pipelines/flux).
*   `CogVideoXLoraLoaderMixin` provides similar functions for [CogVideoX](https://huggingface.co/docs/diffusers/main/en/api/pipelines/cogvideox).
*   `Mochi1LoraLoaderMixin` provides similar functions for [Mochi](https://huggingface.co/docs/diffusers/main/en/api/pipelines/mochi).
*   `AmusedLoraLoaderMixin` is for the [AmusedPipeline](/docs/diffusers/v0.32.2/en/api/pipelines/amused#diffusers.AmusedPipeline).
*   `LoraBaseMixin` provides a base class with several utility methods to fuse, unfuse, unload, LoRAs and more.

To learn more about how to load LoRA weights, see the [LoRA](../../using-diffusers/loading_adapters#lora) loading guide.

[](#diffusers.loaders.StableDiffusionLoraLoaderMixin)StableDiffusionLoraLoaderMixin
-----------------------------------------------------------------------------------

### class diffusers.loaders.StableDiffusionLoraLoaderMixin

[](#diffusers.loaders.StableDiffusionLoraLoaderMixin)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L69)

( )

Load LoRA layers into Stable Diffusion [UNet2DConditionModel](/docs/diffusers/v0.32.2/en/api/models/unet2d-cond#diffusers.UNet2DConditionModel) and [`CLIPTextModel`](https://huggingface.co/docs/transformers/model_doc/clip#transformers.CLIPTextModel).

#### load\_lora\_into\_text\_encoder

[](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_into_text_encoder)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L314)

( state\_dictnetwork\_alphastext\_encoderprefix = Nonelora\_scale = 1.0adapter\_name = None\_pipeline = Nonelow\_cpu\_mem\_usage = False )

Parameters

*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_into_text_encoder.state_dict)**state\_dict** (`dict`) — A standard state dict containing the lora layer parameters. The key should be prefixed with an additional `text_encoder` to distinguish between unet lora layers.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_into_text_encoder.network_alphas)**network\_alphas** (`Dict[str, float]`) — The value of the network alpha used for stable learning and preventing underflow. This value has the same meaning as the `--network_alpha` option in the kohya-ss trainer script. Refer to [this link](https://github.com/darkstorm2150/sd-scripts/blob/main/docs/train_network_README-en.md#execute-learning).
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_into_text_encoder.text_encoder)**text\_encoder** (`CLIPTextModel`) — The text encoder model to load the LoRA layers into.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_into_text_encoder.prefix)**prefix** (`str`) — Expected prefix of the `text_encoder` in the `state_dict`.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_into_text_encoder.lora_scale)**lora\_scale** (`float`) — How much to scale the output of the lora linear layer before it is added with the output of the regular lora layer.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_into_text_encoder.adapter_name)**adapter\_name** (`str`, _optional_) — Adapter name to be used for referencing the loaded adapter model. If not specified, it will use `default_{i}` where i is the total number of adapters being loaded.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_into_text_encoder.low_cpu_mem_usage)**low\_cpu\_mem\_usage** (`bool`, _optional_) — Speed up model loading by only loading the pretrained LoRA weights and not initializing the random weights.

This will load the LoRA layers specified in `state_dict` into `text_encoder`

#### load\_lora\_into\_unet

[](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_into_unet)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L264)

( state\_dictnetwork\_alphasunetadapter\_name = None\_pipeline = Nonelow\_cpu\_mem\_usage = False )

Parameters

*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_into_unet.state_dict)**state\_dict** (`dict`) — A standard state dict containing the lora layer parameters. The keys can either be indexed directly into the unet or prefixed with an additional `unet` which can be used to distinguish between text encoder lora layers.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_into_unet.network_alphas)**network\_alphas** (`Dict[str, float]`) — The value of the network alpha used for stable learning and preventing underflow. This value has the same meaning as the `--network_alpha` option in the kohya-ss trainer script. Refer to [this link](https://github.com/darkstorm2150/sd-scripts/blob/main/docs/train_network_README-en.md#execute-learning).
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_into_unet.unet)**unet** (`UNet2DConditionModel`) — The UNet model to load the LoRA layers into.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_into_unet.adapter_name)**adapter\_name** (`str`, _optional_) — Adapter name to be used for referencing the loaded adapter model. If not specified, it will use `default_{i}` where i is the total number of adapters being loaded.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_into_unet.low_cpu_mem_usage)**low\_cpu\_mem\_usage** (`bool`, _optional_) — Speed up model loading only loading the pretrained LoRA weights and not initializing the random weights.

This will load the LoRA layers specified in `state_dict` into `unet`.

#### load\_lora\_weights

[](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_weights)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L79)

( pretrained\_model\_name\_or\_path\_or\_dict: typing.Union\[str, typing.Dict\[str, torch.Tensor\]\]adapter\_name = None\*\*kwargs )

Parameters

*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_weights.pretrained_model_name_or_path_or_dict)**pretrained\_model\_name\_or\_path\_or\_dict** (`str` or `os.PathLike` or `dict`) — See [lora\_state\_dict()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict).
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_weights.adapter_name)**adapter\_name** (`str`, _optional_) — Adapter name to be used for referencing the loaded adapter model. If not specified, it will use `default_{i}` where i is the total number of adapters being loaded.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_weights.low_cpu_mem_usage)**low\_cpu\_mem\_usage** (`bool`, _optional_) — Speed up model loading by only loading the pretrained LoRA weights and not initializing the random weights.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_weights.kwargs)**kwargs** (`dict`, _optional_) — See [lora\_state\_dict()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict).

Load LoRA weights specified in `pretrained_model_name_or_path_or_dict` into `self.unet` and `self.text_encoder`.

All kwargs are forwarded to `self.lora_state_dict`.

See [lora\_state\_dict()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict) for more details on how the state dict is loaded.

See [load\_lora\_into\_unet()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_into_unet) for more details on how the state dict is loaded into `self.unet`.

See [load\_lora\_into\_text\_encoder()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_into_text_encoder) for more details on how the state dict is loaded into `self.text_encoder`.

#### lora\_state\_dict

[](#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L149)

( pretrained\_model\_name\_or\_path\_or\_dict: typing.Union\[str, typing.Dict\[str, torch.Tensor\]\]\*\*kwargs )

Expand 9 parameters

Parameters

*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict.pretrained_model_name_or_path_or_dict)**pretrained\_model\_name\_or\_path\_or\_dict** (`str` or `os.PathLike` or `dict`) — Can be either:
    
    *   A string, the _model id_ (for example `google/ddpm-celebahq-256`) of a pretrained model hosted on the Hub.
    *   A path to a _directory_ (for example `./my_model_directory`) containing the model weights saved with [ModelMixin.save\_pretrained()](/docs/diffusers/v0.32.2/en/api/models/overview#diffusers.ModelMixin.save_pretrained).
    *   A [torch state dict](https://pytorch.org/tutorials/beginner/saving_loading_models.html#what-is-a-state-dict).
    
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict.cache_dir)**cache\_dir** (`Union[str, os.PathLike]`, _optional_) — Path to a directory where a downloaded pretrained model configuration is cached if the standard cache is not used.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict.force_download)**force\_download** (`bool`, _optional_, defaults to `False`) — Whether or not to force the (re-)download of the model weights and configuration files, overriding the cached versions if they exist.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict.proxies)**proxies** (`Dict[str, str]`, _optional_) — A dictionary of proxy servers to use by protocol or endpoint, for example, `{'http': 'foo.bar:3128', 'http://hostname': 'foo.bar:4012'}`. The proxies are used on each request.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict.local_files_only)**local\_files\_only** (`bool`, _optional_, defaults to `False`) — Whether to only load local model weights and configuration files or not. If set to `True`, the model won’t be downloaded from the Hub.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict.token)**token** (`str` or _bool_, _optional_) — The token to use as HTTP bearer authorization for remote files. If `True`, the token generated from `diffusers-cli login` (stored in `~/.huggingface`) is used.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict.revision)**revision** (`str`, _optional_, defaults to `"main"`) — The specific model version to use. It can be a branch name, a tag name, a commit id, or any identifier allowed by Git.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict.subfolder)**subfolder** (`str`, _optional_, defaults to `""`) — The subfolder location of a model file within a larger model repository on the Hub or locally.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict.weight_name)**weight\_name** (`str`, _optional_, defaults to None) — Name of the serialized state dict file.

Return state dict for lora weights and the network alphas.

We support loading A1111 formatted LoRA checkpoints in a limited capacity.

This function is experimental and might change in the future.

#### save\_lora\_weights

[](#diffusers.loaders.StableDiffusionLoraLoaderMixin.save_lora_weights)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L363)

( save\_directory: typing.Union\[str, os.PathLike\]unet\_lora\_layers: typing.Dict\[str, typing.Union\[torch.nn.modules.module.Module, torch.Tensor\]\] = Nonetext\_encoder\_lora\_layers: typing.Dict\[str, torch.nn.modules.module.Module\] = Noneis\_main\_process: bool = Trueweight\_name: str = Nonesave\_function: typing.Callable = Nonesafe\_serialization: bool = True )

Parameters

*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.save_lora_weights.save_directory)**save\_directory** (`str` or `os.PathLike`) — Directory to save LoRA parameters to. Will be created if it doesn’t exist.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.save_lora_weights.unet_lora_layers)**unet\_lora\_layers** (`Dict[str, torch.nn.Module]` or `Dict[str, torch.Tensor]`) — State dict of the LoRA layers corresponding to the `unet`.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.save_lora_weights.text_encoder_lora_layers)**text\_encoder\_lora\_layers** (`Dict[str, torch.nn.Module]` or `Dict[str, torch.Tensor]`) — State dict of the LoRA layers corresponding to the `text_encoder`. Must explicitly pass the text encoder LoRA state dict because it comes from 🤗 Transformers.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.save_lora_weights.is_main_process)**is\_main\_process** (`bool`, _optional_, defaults to `True`) — Whether the process calling this is the main process or not. Useful during distributed training and you need to call this function on all processes. In this case, set `is_main_process=True` only on the main process to avoid race conditions.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.save_lora_weights.save_function)**save\_function** (`Callable`) — The function to use to save the state dictionary. Useful during distributed training when you need to replace `torch.save` with another method. Can be configured with the environment variable `DIFFUSERS_SAVE_MODE`.
*   [](#diffusers.loaders.StableDiffusionLoraLoaderMixin.save_lora_weights.safe_serialization)**safe\_serialization** (`bool`, _optional_, defaults to `True`) — Whether to save the model using `safetensors` or the traditional PyTorch way with `pickle`.

Save the LoRA parameters corresponding to the UNet and text encoder.

[](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin)StableDiffusionXLLoraLoaderMixin
---------------------------------------------------------------------------------------

### class diffusers.loaders.StableDiffusionXLLoraLoaderMixin

[](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L481)

( )

Load LoRA layers into Stable Diffusion XL [UNet2DConditionModel](/docs/diffusers/v0.32.2/en/api/models/unet2d-cond#diffusers.UNet2DConditionModel), [`CLIPTextModel`](https://huggingface.co/docs/transformers/model_doc/clip#transformers.CLIPTextModel), and [`CLIPTextModelWithProjection`](https://huggingface.co/docs/transformers/model_doc/clip#transformers.CLIPTextModelWithProjection).

#### load\_lora\_into\_text\_encoder

[](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_into_text_encoder)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L754)

( state\_dictnetwork\_alphastext\_encoderprefix = Nonelora\_scale = 1.0adapter\_name = None\_pipeline = Nonelow\_cpu\_mem\_usage = False )

Parameters

*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_into_text_encoder.state_dict)**state\_dict** (`dict`) — A standard state dict containing the lora layer parameters. The key should be prefixed with an additional `text_encoder` to distinguish between unet lora layers.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_into_text_encoder.network_alphas)**network\_alphas** (`Dict[str, float]`) — The value of the network alpha used for stable learning and preventing underflow. This value has the same meaning as the `--network_alpha` option in the kohya-ss trainer script. Refer to [this link](https://github.com/darkstorm2150/sd-scripts/blob/main/docs/train_network_README-en.md#execute-learning).
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_into_text_encoder.text_encoder)**text\_encoder** (`CLIPTextModel`) — The text encoder model to load the LoRA layers into.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_into_text_encoder.prefix)**prefix** (`str`) — Expected prefix of the `text_encoder` in the `state_dict`.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_into_text_encoder.lora_scale)**lora\_scale** (`float`) — How much to scale the output of the lora linear layer before it is added with the output of the regular lora layer.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_into_text_encoder.adapter_name)**adapter\_name** (`str`, _optional_) — Adapter name to be used for referencing the loaded adapter model. If not specified, it will use `default_{i}` where i is the total number of adapters being loaded.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_into_text_encoder.low_cpu_mem_usage)**low\_cpu\_mem\_usage** (`bool`, _optional_) — Speed up model loading by only loading the pretrained LoRA weights and not initializing the random weights.

This will load the LoRA layers specified in `state_dict` into `text_encoder`

#### load\_lora\_into\_unet

[](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_into_unet)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L703)

( state\_dictnetwork\_alphasunetadapter\_name = None\_pipeline = Nonelow\_cpu\_mem\_usage = False )

Parameters

*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_into_unet.state_dict)**state\_dict** (`dict`) — A standard state dict containing the lora layer parameters. The keys can either be indexed directly into the unet or prefixed with an additional `unet` which can be used to distinguish between text encoder lora layers.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_into_unet.network_alphas)**network\_alphas** (`Dict[str, float]`) — The value of the network alpha used for stable learning and preventing underflow. This value has the same meaning as the `--network_alpha` option in the kohya-ss trainer script. Refer to [this link](https://github.com/darkstorm2150/sd-scripts/blob/main/docs/train_network_README-en.md#execute-learning).
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_into_unet.unet)**unet** (`UNet2DConditionModel`) — The UNet model to load the LoRA layers into.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_into_unet.adapter_name)**adapter\_name** (`str`, _optional_) — Adapter name to be used for referencing the loaded adapter model. If not specified, it will use `default_{i}` where i is the total number of adapters being loaded.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_into_unet.low_cpu_mem_usage)**low\_cpu\_mem\_usage** (`bool`, _optional_) — Speed up model loading only loading the pretrained LoRA weights and not initializing the random weights.

This will load the LoRA layers specified in `state_dict` into `unet`.

#### load\_lora\_weights

[](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_weights)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L492)

( pretrained\_model\_name\_or\_path\_or\_dict: typing.Union\[str, typing.Dict\[str, torch.Tensor\]\]adapter\_name: typing.Optional\[str\] = None\*\*kwargs )

Parameters

*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_weights.pretrained_model_name_or_path_or_dict)**pretrained\_model\_name\_or\_path\_or\_dict** (`str` or `os.PathLike` or `dict`) — See [lora\_state\_dict()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict).
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_weights.adapter_name)**adapter\_name** (`str`, _optional_) — Adapter name to be used for referencing the loaded adapter model. If not specified, it will use `default_{i}` where i is the total number of adapters being loaded.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_weights.low_cpu_mem_usage)**low\_cpu\_mem\_usage** (`bool`, _optional_) — Speed up model loading by only loading the pretrained LoRA weights and not initializing the random weights.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.load_lora_weights.kwargs)**kwargs** (`dict`, _optional_) — See [lora\_state\_dict()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict).

Load LoRA weights specified in `pretrained_model_name_or_path_or_dict` into `self.unet` and `self.text_encoder`.

All kwargs are forwarded to `self.lora_state_dict`.

See [lora\_state\_dict()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict) for more details on how the state dict is loaded.

See [load\_lora\_into\_unet()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_into_unet) for more details on how the state dict is loaded into `self.unet`.

See [load\_lora\_into\_text\_encoder()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.load_lora_into_text_encoder) for more details on how the state dict is loaded into `self.text_encoder`.

#### lora\_state\_dict

[](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.lora_state_dict)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L587)

( pretrained\_model\_name\_or\_path\_or\_dict: typing.Union\[str, typing.Dict\[str, torch.Tensor\]\]\*\*kwargs )

Expand 9 parameters

Parameters

*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.lora_state_dict.pretrained_model_name_or_path_or_dict)**pretrained\_model\_name\_or\_path\_or\_dict** (`str` or `os.PathLike` or `dict`) — Can be either:
    
    *   A string, the _model id_ (for example `google/ddpm-celebahq-256`) of a pretrained model hosted on the Hub.
    *   A path to a _directory_ (for example `./my_model_directory`) containing the model weights saved with [ModelMixin.save\_pretrained()](/docs/diffusers/v0.32.2/en/api/models/overview#diffusers.ModelMixin.save_pretrained).
    *   A [torch state dict](https://pytorch.org/tutorials/beginner/saving_loading_models.html#what-is-a-state-dict).
    
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.lora_state_dict.cache_dir)**cache\_dir** (`Union[str, os.PathLike]`, _optional_) — Path to a directory where a downloaded pretrained model configuration is cached if the standard cache is not used.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.lora_state_dict.force_download)**force\_download** (`bool`, _optional_, defaults to `False`) — Whether or not to force the (re-)download of the model weights and configuration files, overriding the cached versions if they exist.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.lora_state_dict.proxies)**proxies** (`Dict[str, str]`, _optional_) — A dictionary of proxy servers to use by protocol or endpoint, for example, `{'http': 'foo.bar:3128', 'http://hostname': 'foo.bar:4012'}`. The proxies are used on each request.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.lora_state_dict.local_files_only)**local\_files\_only** (`bool`, _optional_, defaults to `False`) — Whether to only load local model weights and configuration files or not. If set to `True`, the model won’t be downloaded from the Hub.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.lora_state_dict.token)**token** (`str` or _bool_, _optional_) — The token to use as HTTP bearer authorization for remote files. If `True`, the token generated from `diffusers-cli login` (stored in `~/.huggingface`) is used.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.lora_state_dict.revision)**revision** (`str`, _optional_, defaults to `"main"`) — The specific model version to use. It can be a branch name, a tag name, a commit id, or any identifier allowed by Git.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.lora_state_dict.subfolder)**subfolder** (`str`, _optional_, defaults to `""`) — The subfolder location of a model file within a larger model repository on the Hub or locally.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.lora_state_dict.weight_name)**weight\_name** (`str`, _optional_, defaults to None) — Name of the serialized state dict file.

Return state dict for lora weights and the network alphas.

We support loading A1111 formatted LoRA checkpoints in a limited capacity.

This function is experimental and might change in the future.

#### save\_lora\_weights

[](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.save_lora_weights)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L804)

( save\_directory: typing.Union\[str, os.PathLike\]unet\_lora\_layers: typing.Dict\[str, typing.Union\[torch.nn.modules.module.Module, torch.Tensor\]\] = Nonetext\_encoder\_lora\_layers: typing.Dict\[str, typing.Union\[torch.nn.modules.module.Module, torch.Tensor\]\] = Nonetext\_encoder\_2\_lora\_layers: typing.Dict\[str, typing.Union\[torch.nn.modules.module.Module, torch.Tensor\]\] = Noneis\_main\_process: bool = Trueweight\_name: str = Nonesave\_function: typing.Callable = Nonesafe\_serialization: bool = True )

Expand 7 parameters

Parameters

*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.save_lora_weights.save_directory)**save\_directory** (`str` or `os.PathLike`) — Directory to save LoRA parameters to. Will be created if it doesn’t exist.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.save_lora_weights.unet_lora_layers)**unet\_lora\_layers** (`Dict[str, torch.nn.Module]` or `Dict[str, torch.Tensor]`) — State dict of the LoRA layers corresponding to the `unet`.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.save_lora_weights.text_encoder_lora_layers)**text\_encoder\_lora\_layers** (`Dict[str, torch.nn.Module]` or `Dict[str, torch.Tensor]`) — State dict of the LoRA layers corresponding to the `text_encoder`. Must explicitly pass the text encoder LoRA state dict because it comes from 🤗 Transformers.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.save_lora_weights.text_encoder_2_lora_layers)**text\_encoder\_2\_lora\_layers** (`Dict[str, torch.nn.Module]` or `Dict[str, torch.Tensor]`) — State dict of the LoRA layers corresponding to the `text_encoder_2`. Must explicitly pass the text encoder LoRA state dict because it comes from 🤗 Transformers.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.save_lora_weights.is_main_process)**is\_main\_process** (`bool`, _optional_, defaults to `True`) — Whether the process calling this is the main process or not. Useful during distributed training and you need to call this function on all processes. In this case, set `is_main_process=True` only on the main process to avoid race conditions.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.save_lora_weights.save_function)**save\_function** (`Callable`) — The function to use to save the state dictionary. Useful during distributed training when you need to replace `torch.save` with another method. Can be configured with the environment variable `DIFFUSERS_SAVE_MODE`.
*   [](#diffusers.loaders.StableDiffusionXLLoraLoaderMixin.save_lora_weights.safe_serialization)**safe\_serialization** (`bool`, _optional_, defaults to `True`) — Whether to save the model using `safetensors` or the traditional PyTorch way with `pickle`.

Save the LoRA parameters corresponding to the UNet and text encoder.

[](#diffusers.loaders.SD3LoraLoaderMixin)SD3LoraLoaderMixin
-----------------------------------------------------------

### class diffusers.loaders.SD3LoraLoaderMixin

[](#diffusers.loaders.SD3LoraLoaderMixin)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L930)

( )

Load LoRA layers into [SD3Transformer2DModel](/docs/diffusers/v0.32.2/en/api/models/sd3_transformer2d#diffusers.SD3Transformer2DModel), [`CLIPTextModel`](https://huggingface.co/docs/transformers/model_doc/clip#transformers.CLIPTextModel), and [`CLIPTextModelWithProjection`](https://huggingface.co/docs/transformers/model_doc/clip#transformers.CLIPTextModelWithProjection).

Specific to [StableDiffusion3Pipeline](/docs/diffusers/v0.32.2/en/api/pipelines/stable_diffusion/stable_diffusion_3#diffusers.StableDiffusion3Pipeline).

#### load\_lora\_into\_text\_encoder

[](#diffusers.loaders.SD3LoraLoaderMixin.load_lora_into_text_encoder)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L1161)

( state\_dictnetwork\_alphastext\_encoderprefix = Nonelora\_scale = 1.0adapter\_name = None\_pipeline = Nonelow\_cpu\_mem\_usage = False )

Parameters

*   [](#diffusers.loaders.SD3LoraLoaderMixin.load_lora_into_text_encoder.state_dict)**state\_dict** (`dict`) — A standard state dict containing the lora layer parameters. The key should be prefixed with an additional `text_encoder` to distinguish between unet lora layers.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.load_lora_into_text_encoder.network_alphas)**network\_alphas** (`Dict[str, float]`) — The value of the network alpha used for stable learning and preventing underflow. This value has the same meaning as the `--network_alpha` option in the kohya-ss trainer script. Refer to [this link](https://github.com/darkstorm2150/sd-scripts/blob/main/docs/train_network_README-en.md#execute-learning).
*   [](#diffusers.loaders.SD3LoraLoaderMixin.load_lora_into_text_encoder.text_encoder)**text\_encoder** (`CLIPTextModel`) — The text encoder model to load the LoRA layers into.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.load_lora_into_text_encoder.prefix)**prefix** (`str`) — Expected prefix of the `text_encoder` in the `state_dict`.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.load_lora_into_text_encoder.lora_scale)**lora\_scale** (`float`) — How much to scale the output of the lora linear layer before it is added with the output of the regular lora layer.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.load_lora_into_text_encoder.adapter_name)**adapter\_name** (`str`, _optional_) — Adapter name to be used for referencing the loaded adapter model. If not specified, it will use `default_{i}` where i is the total number of adapters being loaded.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.load_lora_into_text_encoder.low_cpu_mem_usage)**low\_cpu\_mem\_usage** (`bool`, _optional_) — Speed up model loading by only loading the pretrained LoRA weights and not initializing the random weights.

This will load the LoRA layers specified in `state_dict` into `text_encoder`

#### load\_lora\_into\_transformer

[](#diffusers.loaders.SD3LoraLoaderMixin.load_lora_into_transformer)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L1125)

( state\_dicttransformeradapter\_name = None\_pipeline = Nonelow\_cpu\_mem\_usage = False )

Parameters

*   [](#diffusers.loaders.SD3LoraLoaderMixin.load_lora_into_transformer.state_dict)**state\_dict** (`dict`) — A standard state dict containing the lora layer parameters. The keys can either be indexed directly into the unet or prefixed with an additional `unet` which can be used to distinguish between text encoder lora layers.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.load_lora_into_transformer.transformer)**transformer** (`SD3Transformer2DModel`) — The Transformer model to load the LoRA layers into.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.load_lora_into_transformer.adapter_name)**adapter\_name** (`str`, _optional_) — Adapter name to be used for referencing the loaded adapter model. If not specified, it will use `default_{i}` where i is the total number of adapters being loaded.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.load_lora_into_transformer.low_cpu_mem_usage)**low\_cpu\_mem\_usage** (`bool`, _optional_) — Speed up model loading by only loading the pretrained LoRA weights and not initializing the random weights.

This will load the LoRA layers specified in `state_dict` into `transformer`.

#### load\_lora\_weights

[](#diffusers.loaders.SD3LoraLoaderMixin.load_lora_weights)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L1040)

( pretrained\_model\_name\_or\_path\_or\_dict: typing.Union\[str, typing.Dict\[str, torch.Tensor\]\]adapter\_name = None\*\*kwargs )

Parameters

*   [](#diffusers.loaders.SD3LoraLoaderMixin.load_lora_weights.pretrained_model_name_or_path_or_dict)**pretrained\_model\_name\_or\_path\_or\_dict** (`str` or `os.PathLike` or `dict`) — See [lora\_state\_dict()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict).
*   [](#diffusers.loaders.SD3LoraLoaderMixin.load_lora_weights.adapter_name)**adapter\_name** (`str`, _optional_) — Adapter name to be used for referencing the loaded adapter model. If not specified, it will use `default_{i}` where i is the total number of adapters being loaded.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.load_lora_weights.low_cpu_mem_usage)**low\_cpu\_mem\_usage** (`bool`, _optional_) — Speed up model loading by only loading the pretrained LoRA weights and not initializing the random weights.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.load_lora_weights.kwargs)**kwargs** (`dict`, _optional_) — See [lora\_state\_dict()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict).

Load LoRA weights specified in `pretrained_model_name_or_path_or_dict` into `self.unet` and `self.text_encoder`.

All kwargs are forwarded to `self.lora_state_dict`.

See [lora\_state\_dict()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict) for more details on how the state dict is loaded.

See `~loaders.StableDiffusionLoraLoaderMixin.load_lora_into_transformer` for more details on how the state dict is loaded into `self.transformer`.

#### lora\_state\_dict

[](#diffusers.loaders.SD3LoraLoaderMixin.lora_state_dict)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L943)

( pretrained\_model\_name\_or\_path\_or\_dict: typing.Union\[str, typing.Dict\[str, torch.Tensor\]\]\*\*kwargs )

Expand 8 parameters

Parameters

*   [](#diffusers.loaders.SD3LoraLoaderMixin.lora_state_dict.pretrained_model_name_or_path_or_dict)**pretrained\_model\_name\_or\_path\_or\_dict** (`str` or `os.PathLike` or `dict`) — Can be either:
    
    *   A string, the _model id_ (for example `google/ddpm-celebahq-256`) of a pretrained model hosted on the Hub.
    *   A path to a _directory_ (for example `./my_model_directory`) containing the model weights saved with [ModelMixin.save\_pretrained()](/docs/diffusers/v0.32.2/en/api/models/overview#diffusers.ModelMixin.save_pretrained).
    *   A [torch state dict](https://pytorch.org/tutorials/beginner/saving_loading_models.html#what-is-a-state-dict).
    
*   [](#diffusers.loaders.SD3LoraLoaderMixin.lora_state_dict.cache_dir)**cache\_dir** (`Union[str, os.PathLike]`, _optional_) — Path to a directory where a downloaded pretrained model configuration is cached if the standard cache is not used.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.lora_state_dict.force_download)**force\_download** (`bool`, _optional_, defaults to `False`) — Whether or not to force the (re-)download of the model weights and configuration files, overriding the cached versions if they exist.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.lora_state_dict.proxies)**proxies** (`Dict[str, str]`, _optional_) — A dictionary of proxy servers to use by protocol or endpoint, for example, `{'http': 'foo.bar:3128', 'http://hostname': 'foo.bar:4012'}`. The proxies are used on each request.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.lora_state_dict.local_files_only)**local\_files\_only** (`bool`, _optional_, defaults to `False`) — Whether to only load local model weights and configuration files or not. If set to `True`, the model won’t be downloaded from the Hub.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.lora_state_dict.token)**token** (`str` or _bool_, _optional_) — The token to use as HTTP bearer authorization for remote files. If `True`, the token generated from `diffusers-cli login` (stored in `~/.huggingface`) is used.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.lora_state_dict.revision)**revision** (`str`, _optional_, defaults to `"main"`) — The specific model version to use. It can be a branch name, a tag name, a commit id, or any identifier allowed by Git.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.lora_state_dict.subfolder)**subfolder** (`str`, _optional_, defaults to `""`) — The subfolder location of a model file within a larger model repository on the Hub or locally.

Return state dict for lora weights and the network alphas.

We support loading A1111 formatted LoRA checkpoints in a limited capacity.

This function is experimental and might change in the future.

#### save\_lora\_weights

[](#diffusers.loaders.SD3LoraLoaderMixin.save_lora_weights)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L1211)

( save\_directory: typing.Union\[str, os.PathLike\]transformer\_lora\_layers: typing.Dict\[str, torch.nn.modules.module.Module\] = Nonetext\_encoder\_lora\_layers: typing.Dict\[str, typing.Union\[torch.nn.modules.module.Module, torch.Tensor\]\] = Nonetext\_encoder\_2\_lora\_layers: typing.Dict\[str, typing.Union\[torch.nn.modules.module.Module, torch.Tensor\]\] = Noneis\_main\_process: bool = Trueweight\_name: str = Nonesave\_function: typing.Callable = Nonesafe\_serialization: bool = True )

Expand 7 parameters

Parameters

*   [](#diffusers.loaders.SD3LoraLoaderMixin.save_lora_weights.save_directory)**save\_directory** (`str` or `os.PathLike`) — Directory to save LoRA parameters to. Will be created if it doesn’t exist.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.save_lora_weights.transformer_lora_layers)**transformer\_lora\_layers** (`Dict[str, torch.nn.Module]` or `Dict[str, torch.Tensor]`) — State dict of the LoRA layers corresponding to the `transformer`.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.save_lora_weights.text_encoder_lora_layers)**text\_encoder\_lora\_layers** (`Dict[str, torch.nn.Module]` or `Dict[str, torch.Tensor]`) — State dict of the LoRA layers corresponding to the `text_encoder`. Must explicitly pass the text encoder LoRA state dict because it comes from 🤗 Transformers.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.save_lora_weights.text_encoder_2_lora_layers)**text\_encoder\_2\_lora\_layers** (`Dict[str, torch.nn.Module]` or `Dict[str, torch.Tensor]`) — State dict of the LoRA layers corresponding to the `text_encoder_2`. Must explicitly pass the text encoder LoRA state dict because it comes from 🤗 Transformers.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.save_lora_weights.is_main_process)**is\_main\_process** (`bool`, _optional_, defaults to `True`) — Whether the process calling this is the main process or not. Useful during distributed training and you need to call this function on all processes. In this case, set `is_main_process=True` only on the main process to avoid race conditions.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.save_lora_weights.save_function)**save\_function** (`Callable`) — The function to use to save the state dictionary. Useful during distributed training when you need to replace `torch.save` with another method. Can be configured with the environment variable `DIFFUSERS_SAVE_MODE`.
*   [](#diffusers.loaders.SD3LoraLoaderMixin.save_lora_weights.safe_serialization)**safe\_serialization** (`bool`, _optional_, defaults to `True`) — Whether to save the model using `safetensors` or the traditional PyTorch way with `pickle`.

Save the LoRA parameters corresponding to the UNet and text encoder.

[](#diffusers.loaders.FluxLoraLoaderMixin)FluxLoraLoaderMixin
-------------------------------------------------------------

### class diffusers.loaders.FluxLoraLoaderMixin

[](#diffusers.loaders.FluxLoraLoaderMixin)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L1338)

( )

Load LoRA layers into [FluxTransformer2DModel](/docs/diffusers/v0.32.2/en/api/models/flux_transformer#diffusers.FluxTransformer2DModel), [`CLIPTextModel`](https://huggingface.co/docs/transformers/model_doc/clip#transformers.CLIPTextModel).

Specific to [StableDiffusion3Pipeline](/docs/diffusers/v0.32.2/en/api/pipelines/stable_diffusion/stable_diffusion_3#diffusers.StableDiffusion3Pipeline).

#### load\_lora\_into\_text\_encoder

[](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_into_text_encoder)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L1691)

( state\_dictnetwork\_alphastext\_encoderprefix = Nonelora\_scale = 1.0adapter\_name = None\_pipeline = Nonelow\_cpu\_mem\_usage = False )

Parameters

*   [](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_into_text_encoder.state_dict)**state\_dict** (`dict`) — A standard state dict containing the lora layer parameters. The key should be prefixed with an additional `text_encoder` to distinguish between unet lora layers.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_into_text_encoder.network_alphas)**network\_alphas** (`Dict[str, float]`) — The value of the network alpha used for stable learning and preventing underflow. This value has the same meaning as the `--network_alpha` option in the kohya-ss trainer script. Refer to [this link](https://github.com/darkstorm2150/sd-scripts/blob/main/docs/train_network_README-en.md#execute-learning).
*   [](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_into_text_encoder.text_encoder)**text\_encoder** (`CLIPTextModel`) — The text encoder model to load the LoRA layers into.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_into_text_encoder.prefix)**prefix** (`str`) — Expected prefix of the `text_encoder` in the `state_dict`.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_into_text_encoder.lora_scale)**lora\_scale** (`float`) — How much to scale the output of the lora linear layer before it is added with the output of the regular lora layer.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_into_text_encoder.adapter_name)**adapter\_name** (`str`, _optional_) — Adapter name to be used for referencing the loaded adapter model. If not specified, it will use `default_{i}` where i is the total number of adapters being loaded.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_into_text_encoder.low_cpu_mem_usage)**low\_cpu\_mem\_usage** (`bool`, _optional_) — Speed up model loading by only loading the pretrained LoRA weights and not initializing the random weights.

This will load the LoRA layers specified in `state_dict` into `text_encoder`

#### load\_lora\_into\_transformer

[](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_into_transformer)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L1594)

( state\_dictnetwork\_alphastransformeradapter\_name = None\_pipeline = Nonelow\_cpu\_mem\_usage = False )

Parameters

*   [](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_into_transformer.state_dict)**state\_dict** (`dict`) — A standard state dict containing the lora layer parameters. The keys can either be indexed directly into the unet or prefixed with an additional `unet` which can be used to distinguish between text encoder lora layers.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_into_transformer.network_alphas)**network\_alphas** (`Dict[str, float]`) — The value of the network alpha used for stable learning and preventing underflow. This value has the same meaning as the `--network_alpha` option in the kohya-ss trainer script. Refer to [this link](https://github.com/darkstorm2150/sd-scripts/blob/main/docs/train_network_README-en.md#execute-learning).
*   [](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_into_transformer.transformer)**transformer** (`FluxTransformer2DModel`) — The Transformer model to load the LoRA layers into.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_into_transformer.adapter_name)**adapter\_name** (`str`, _optional_) — Adapter name to be used for referencing the loaded adapter model. If not specified, it will use `default_{i}` where i is the total number of adapters being loaded.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_into_transformer.low_cpu_mem_usage)**low\_cpu\_mem\_usage** (`bool`, _optional_) — Speed up model loading by only loading the pretrained LoRA weights and not initializing the random weights.

This will load the LoRA layers specified in `state_dict` into `transformer`.

#### load\_lora\_weights

[](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_weights)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L1485)

( pretrained\_model\_name\_or\_path\_or\_dict: typing.Union\[str, typing.Dict\[str, torch.Tensor\]\]adapter\_name = None\*\*kwargs )

Parameters

*   [](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_weights.pretrained_model_name_or_path_or_dict)**pretrained\_model\_name\_or\_path\_or\_dict** (`str` or `os.PathLike` or `dict`) — See [lora\_state\_dict()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict).
*   [](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_weights.kwargs)**kwargs** (`dict`, _optional_) — See [lora\_state\_dict()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict).
*   [](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_weights.adapter_name)**adapter\_name** (`str`, _optional_) — Adapter name to be used for referencing the loaded adapter model. If not specified, it will use `default_{i}` where i is the total number of adapters being loaded.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.load_lora_weights.low_cpu_mem_usage)**low\_cpu\_mem\_usage** (`bool`, _optional_) — \`Speed up model loading by only loading the pretrained LoRA weights and not initializing the random weights.

Load LoRA weights specified in `pretrained_model_name_or_path_or_dict` into `self.transformer` and `self.text_encoder`.

All kwargs are forwarded to `self.lora_state_dict`.

See [lora\_state\_dict()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict) for more details on how the state dict is loaded.

See `~loaders.StableDiffusionLoraLoaderMixin.load_lora_into_transformer` for more details on how the state dict is loaded into `self.transformer`.

#### lora\_state\_dict

[](#diffusers.loaders.FluxLoraLoaderMixin.lora_state_dict)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L1351)

( pretrained\_model\_name\_or\_path\_or\_dict: typing.Union\[str, typing.Dict\[str, torch.Tensor\]\]return\_alphas: bool = False\*\*kwargs )

Expand 8 parameters

Parameters

*   [](#diffusers.loaders.FluxLoraLoaderMixin.lora_state_dict.pretrained_model_name_or_path_or_dict)**pretrained\_model\_name\_or\_path\_or\_dict** (`str` or `os.PathLike` or `dict`) — Can be either:
    
    *   A string, the _model id_ (for example `google/ddpm-celebahq-256`) of a pretrained model hosted on the Hub.
    *   A path to a _directory_ (for example `./my_model_directory`) containing the model weights saved with [ModelMixin.save\_pretrained()](/docs/diffusers/v0.32.2/en/api/models/overview#diffusers.ModelMixin.save_pretrained).
    *   A [torch state dict](https://pytorch.org/tutorials/beginner/saving_loading_models.html#what-is-a-state-dict).
    
*   [](#diffusers.loaders.FluxLoraLoaderMixin.lora_state_dict.cache_dir)**cache\_dir** (`Union[str, os.PathLike]`, _optional_) — Path to a directory where a downloaded pretrained model configuration is cached if the standard cache is not used.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.lora_state_dict.force_download)**force\_download** (`bool`, _optional_, defaults to `False`) — Whether or not to force the (re-)download of the model weights and configuration files, overriding the cached versions if they exist.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.lora_state_dict.proxies)**proxies** (`Dict[str, str]`, _optional_) — A dictionary of proxy servers to use by protocol or endpoint, for example, `{'http': 'foo.bar:3128', 'http://hostname': 'foo.bar:4012'}`. The proxies are used on each request.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.lora_state_dict.local_files_only)**local\_files\_only** (`bool`, _optional_, defaults to `False`) — Whether to only load local model weights and configuration files or not. If set to `True`, the model won’t be downloaded from the Hub.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.lora_state_dict.token)**token** (`str` or _bool_, _optional_) — The token to use as HTTP bearer authorization for remote files. If `True`, the token generated from `diffusers-cli login` (stored in `~/.huggingface`) is used.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.lora_state_dict.revision)**revision** (`str`, _optional_, defaults to `"main"`) — The specific model version to use. It can be a branch name, a tag name, a commit id, or any identifier allowed by Git.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.lora_state_dict.subfolder)**subfolder** (`str`, _optional_, defaults to `""`) — The subfolder location of a model file within a larger model repository on the Hub or locally.

Return state dict for lora weights and the network alphas.

We support loading A1111 formatted LoRA checkpoints in a limited capacity.

This function is experimental and might change in the future.

#### save\_lora\_weights

[](#diffusers.loaders.FluxLoraLoaderMixin.save_lora_weights)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L1741)

( save\_directory: typing.Union\[str, os.PathLike\]transformer\_lora\_layers: typing.Dict\[str, typing.Union\[torch.nn.modules.module.Module, torch.Tensor\]\] = Nonetext\_encoder\_lora\_layers: typing.Dict\[str, torch.nn.modules.module.Module\] = Noneis\_main\_process: bool = Trueweight\_name: str = Nonesave\_function: typing.Callable = Nonesafe\_serialization: bool = True )

Parameters

*   [](#diffusers.loaders.FluxLoraLoaderMixin.save_lora_weights.save_directory)**save\_directory** (`str` or `os.PathLike`) — Directory to save LoRA parameters to. Will be created if it doesn’t exist.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.save_lora_weights.transformer_lora_layers)**transformer\_lora\_layers** (`Dict[str, torch.nn.Module]` or `Dict[str, torch.Tensor]`) — State dict of the LoRA layers corresponding to the `transformer`.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.save_lora_weights.text_encoder_lora_layers)**text\_encoder\_lora\_layers** (`Dict[str, torch.nn.Module]` or `Dict[str, torch.Tensor]`) — State dict of the LoRA layers corresponding to the `text_encoder`. Must explicitly pass the text encoder LoRA state dict because it comes from 🤗 Transformers.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.save_lora_weights.is_main_process)**is\_main\_process** (`bool`, _optional_, defaults to `True`) — Whether the process calling this is the main process or not. Useful during distributed training and you need to call this function on all processes. In this case, set `is_main_process=True` only on the main process to avoid race conditions.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.save_lora_weights.save_function)**save\_function** (`Callable`) — The function to use to save the state dictionary. Useful during distributed training when you need to replace `torch.save` with another method. Can be configured with the environment variable `DIFFUSERS_SAVE_MODE`.
*   [](#diffusers.loaders.FluxLoraLoaderMixin.save_lora_weights.safe_serialization)**safe\_serialization** (`bool`, _optional_, defaults to `True`) — Whether to save the model using `safetensors` or the traditional PyTorch way with `pickle`.

Save the LoRA parameters corresponding to the UNet and text encoder.

#### unfuse\_lora

[](#diffusers.loaders.FluxLoraLoaderMixin.unfuse_lora)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L1852)

( components: typing.List\[str\] = \['transformer', 'text\_encoder'\]\*\*kwargs )

Parameters

*   [](#diffusers.loaders.FluxLoraLoaderMixin.unfuse_lora.components)**components** (`List[str]`) — List of LoRA-injectable components to unfuse LoRA from.

Reverses the effect of [`pipe.fuse_lora()`](https://huggingface.co/docs/diffusers/main/en/api/loaders#diffusers.loaders.LoraBaseMixin.fuse_lora).

This is an experimental API.

#### unload\_lora\_weights

[](#diffusers.loaders.FluxLoraLoaderMixin.unload_lora_weights)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L1873)

( reset\_to\_overwritten\_params = False )

Parameters

*   [](#diffusers.loaders.FluxLoraLoaderMixin.unload_lora_weights.reset_to_overwritten_params)**reset\_to\_overwritten\_params** (`bool`, defaults to `False`) — Whether to reset the LoRA-loaded modules to their original params. Refer to the [Flux documentation](https://huggingface.co/docs/diffusers/main/en/api/pipelines/flux) to learn more.

Unloads the LoRA parameters.

[](#diffusers.loaders.FluxLoraLoaderMixin.unload_lora_weights.example)

Examples:

Copied

\>>> \# Assuming \`pipeline\` is already loaded with the LoRA parameters.
\>>> pipeline.unload\_lora\_weights()
\>>> ...

[](#diffusers.loaders.CogVideoXLoraLoaderMixin)CogVideoXLoraLoaderMixin
-----------------------------------------------------------------------

### class diffusers.loaders.CogVideoXLoraLoaderMixin

[](#diffusers.loaders.CogVideoXLoraLoaderMixin)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L2291)

( )

Load LoRA layers into [CogVideoXTransformer3DModel](/docs/diffusers/v0.32.2/en/api/models/cogvideox_transformer3d#diffusers.CogVideoXTransformer3DModel). Specific to [CogVideoXPipeline](/docs/diffusers/v0.32.2/en/api/pipelines/cogvideox#diffusers.CogVideoXPipeline).

#### load\_lora\_into\_transformer

[](#diffusers.loaders.CogVideoXLoraLoaderMixin.load_lora_into_transformer)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L2447)

( state\_dicttransformeradapter\_name = None\_pipeline = Nonelow\_cpu\_mem\_usage = False )

Parameters

*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.load_lora_into_transformer.state_dict)**state\_dict** (`dict`) — A standard state dict containing the lora layer parameters. The keys can either be indexed directly into the unet or prefixed with an additional `unet` which can be used to distinguish between text encoder lora layers.
*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.load_lora_into_transformer.transformer)**transformer** (`CogVideoXTransformer3DModel`) — The Transformer model to load the LoRA layers into.
*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.load_lora_into_transformer.adapter_name)**adapter\_name** (`str`, _optional_) — Adapter name to be used for referencing the loaded adapter model. If not specified, it will use `default_{i}` where i is the total number of adapters being loaded.
*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.load_lora_into_transformer.low_cpu_mem_usage)**low\_cpu\_mem\_usage** (`bool`, _optional_) — Speed up model loading by only loading the pretrained LoRA weights and not initializing the random weights.

This will load the LoRA layers specified in `state_dict` into `transformer`.

#### load\_lora\_weights

[](#diffusers.loaders.CogVideoXLoraLoaderMixin.load_lora_weights)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L2397)

( pretrained\_model\_name\_or\_path\_or\_dict: typing.Union\[str, typing.Dict\[str, torch.Tensor\]\]adapter\_name = None\*\*kwargs )

Parameters

*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.load_lora_weights.pretrained_model_name_or_path_or_dict)**pretrained\_model\_name\_or\_path\_or\_dict** (`str` or `os.PathLike` or `dict`) — See [lora\_state\_dict()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict).
*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.load_lora_weights.adapter_name)**adapter\_name** (`str`, _optional_) — Adapter name to be used for referencing the loaded adapter model. If not specified, it will use `default_{i}` where i is the total number of adapters being loaded.
*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.load_lora_weights.low_cpu_mem_usage)**low\_cpu\_mem\_usage** (`bool`, _optional_) — Speed up model loading by only loading the pretrained LoRA weights and not initializing the random weights.
*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.load_lora_weights.kwargs)**kwargs** (`dict`, _optional_) — See [lora\_state\_dict()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict).

Load LoRA weights specified in `pretrained_model_name_or_path_or_dict` into `self.transformer` and `self.text_encoder`. All kwargs are forwarded to `self.lora_state_dict`. See [lora\_state\_dict()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict) for more details on how the state dict is loaded. See `~loaders.StableDiffusionLoraLoaderMixin.load_lora_into_transformer` for more details on how the state dict is loaded into `self.transformer`.

#### lora\_state\_dict

[](#diffusers.loaders.CogVideoXLoraLoaderMixin.lora_state_dict)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L2299)

( pretrained\_model\_name\_or\_path\_or\_dict: typing.Union\[str, typing.Dict\[str, torch.Tensor\]\]\*\*kwargs )

Expand 8 parameters

Parameters

*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.lora_state_dict.pretrained_model_name_or_path_or_dict)**pretrained\_model\_name\_or\_path\_or\_dict** (`str` or `os.PathLike` or `dict`) — Can be either:
    
    *   A string, the _model id_ (for example `google/ddpm-celebahq-256`) of a pretrained model hosted on the Hub.
    *   A path to a _directory_ (for example `./my_model_directory`) containing the model weights saved with [ModelMixin.save\_pretrained()](/docs/diffusers/v0.32.2/en/api/models/overview#diffusers.ModelMixin.save_pretrained).
    *   A [torch state dict](https://pytorch.org/tutorials/beginner/saving_loading_models.html#what-is-a-state-dict).
    
*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.lora_state_dict.cache_dir)**cache\_dir** (`Union[str, os.PathLike]`, _optional_) — Path to a directory where a downloaded pretrained model configuration is cached if the standard cache is not used.
*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.lora_state_dict.force_download)**force\_download** (`bool`, _optional_, defaults to `False`) — Whether or not to force the (re-)download of the model weights and configuration files, overriding the cached versions if they exist.
*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.lora_state_dict.proxies)**proxies** (`Dict[str, str]`, _optional_) — A dictionary of proxy servers to use by protocol or endpoint, for example, `{'http': 'foo.bar:3128', 'http://hostname': 'foo.bar:4012'}`. The proxies are used on each request.
*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.lora_state_dict.local_files_only)**local\_files\_only** (`bool`, _optional_, defaults to `False`) — Whether to only load local model weights and configuration files or not. If set to `True`, the model won’t be downloaded from the Hub.
*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.lora_state_dict.token)**token** (`str` or _bool_, _optional_) — The token to use as HTTP bearer authorization for remote files. If `True`, the token generated from `diffusers-cli login` (stored in `~/.huggingface`) is used.
*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.lora_state_dict.revision)**revision** (`str`, _optional_, defaults to `"main"`) — The specific model version to use. It can be a branch name, a tag name, a commit id, or any identifier allowed by Git.
*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.lora_state_dict.subfolder)**subfolder** (`str`, _optional_, defaults to `""`) — The subfolder location of a model file within a larger model repository on the Hub or locally.

Return state dict for lora weights and the network alphas.

We support loading A1111 formatted LoRA checkpoints in a limited capacity.

This function is experimental and might change in the future.

#### save\_lora\_weights

[](#diffusers.loaders.CogVideoXLoraLoaderMixin.save_lora_weights)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L2484)

( save\_directory: typing.Union\[str, os.PathLike\]transformer\_lora\_layers: typing.Dict\[str, typing.Union\[torch.nn.modules.module.Module, torch.Tensor\]\] = Noneis\_main\_process: bool = Trueweight\_name: str = Nonesave\_function: typing.Callable = Nonesafe\_serialization: bool = True )

Parameters

*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.save_lora_weights.save_directory)**save\_directory** (`str` or `os.PathLike`) — Directory to save LoRA parameters to. Will be created if it doesn’t exist.
*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.save_lora_weights.transformer_lora_layers)**transformer\_lora\_layers** (`Dict[str, torch.nn.Module]` or `Dict[str, torch.Tensor]`) — State dict of the LoRA layers corresponding to the `transformer`.
*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.save_lora_weights.is_main_process)**is\_main\_process** (`bool`, _optional_, defaults to `True`) — Whether the process calling this is the main process or not. Useful during distributed training and you need to call this function on all processes. In this case, set `is_main_process=True` only on the main process to avoid race conditions.
*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.save_lora_weights.save_function)**save\_function** (`Callable`) — The function to use to save the state dictionary. Useful during distributed training when you need to replace `torch.save` with another method. Can be configured with the environment variable `DIFFUSERS_SAVE_MODE`.
*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.save_lora_weights.safe_serialization)**safe\_serialization** (`bool`, _optional_, defaults to `True`) — Whether to save the model using `safetensors` or the traditional PyTorch way with `pickle`.

Save the LoRA parameters corresponding to the UNet and text encoder.

#### unfuse\_lora

[](#diffusers.loaders.CogVideoXLoraLoaderMixin.unfuse_lora)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L2575)

( components: typing.List\[str\] = \['transformer'\]\*\*kwargs )

Parameters

*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.unfuse_lora.components)**components** (`List[str]`) — List of LoRA-injectable components to unfuse LoRA from.
*   [](#diffusers.loaders.CogVideoXLoraLoaderMixin.unfuse_lora.unfuse_transformer)**unfuse\_transformer** (`bool`, defaults to `True`) — Whether to unfuse the UNet LoRA parameters.

Reverses the effect of [`pipe.fuse_lora()`](https://huggingface.co/docs/diffusers/main/en/api/loaders#diffusers.loaders.LoraBaseMixin.fuse_lora).

This is an experimental API.

[](#diffusers.loaders.Mochi1LoraLoaderMixin)Mochi1LoraLoaderMixin
-----------------------------------------------------------------

### class diffusers.loaders.Mochi1LoraLoaderMixin

[](#diffusers.loaders.Mochi1LoraLoaderMixin)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L2593)

( )

Load LoRA layers into [MochiTransformer3DModel](/docs/diffusers/v0.32.2/en/api/models/mochi_transformer3d#diffusers.MochiTransformer3DModel). Specific to [MochiPipeline](/docs/diffusers/v0.32.2/en/api/pipelines/mochi#diffusers.MochiPipeline).

#### load\_lora\_into\_transformer

[](#diffusers.loaders.Mochi1LoraLoaderMixin.load_lora_into_transformer)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L2750)

( state\_dicttransformeradapter\_name = None\_pipeline = Nonelow\_cpu\_mem\_usage = False )

Parameters

*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.load_lora_into_transformer.state_dict)**state\_dict** (`dict`) — A standard state dict containing the lora layer parameters. The keys can either be indexed directly into the unet or prefixed with an additional `unet` which can be used to distinguish between text encoder lora layers.
*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.load_lora_into_transformer.transformer)**transformer** (`MochiTransformer3DModel`) — The Transformer model to load the LoRA layers into.
*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.load_lora_into_transformer.adapter_name)**adapter\_name** (`str`, _optional_) — Adapter name to be used for referencing the loaded adapter model. If not specified, it will use `default_{i}` where i is the total number of adapters being loaded.
*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.load_lora_into_transformer.low_cpu_mem_usage)**low\_cpu\_mem\_usage** (`bool`, _optional_) — Speed up model loading by only loading the pretrained LoRA weights and not initializing the random weights.

This will load the LoRA layers specified in `state_dict` into `transformer`.

#### load\_lora\_weights

[](#diffusers.loaders.Mochi1LoraLoaderMixin.load_lora_weights)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L2700)

( pretrained\_model\_name\_or\_path\_or\_dict: typing.Union\[str, typing.Dict\[str, torch.Tensor\]\]adapter\_name = None\*\*kwargs )

Parameters

*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.load_lora_weights.pretrained_model_name_or_path_or_dict)**pretrained\_model\_name\_or\_path\_or\_dict** (`str` or `os.PathLike` or `dict`) — See [lora\_state\_dict()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict).
*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.load_lora_weights.adapter_name)**adapter\_name** (`str`, _optional_) — Adapter name to be used for referencing the loaded adapter model. If not specified, it will use `default_{i}` where i is the total number of adapters being loaded.
*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.load_lora_weights.low_cpu_mem_usage)**low\_cpu\_mem\_usage** (`bool`, _optional_) — Speed up model loading by only loading the pretrained LoRA weights and not initializing the random weights.
*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.load_lora_weights.kwargs)**kwargs** (`dict`, _optional_) — See [lora\_state\_dict()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict).

Load LoRA weights specified in `pretrained_model_name_or_path_or_dict` into `self.transformer` and `self.text_encoder`. All kwargs are forwarded to `self.lora_state_dict`. See [lora\_state\_dict()](/docs/diffusers/v0.32.2/en/api/loaders/lora#diffusers.loaders.StableDiffusionLoraLoaderMixin.lora_state_dict) for more details on how the state dict is loaded. See `~loaders.StableDiffusionLoraLoaderMixin.load_lora_into_transformer` for more details on how the state dict is loaded into `self.transformer`.

#### lora\_state\_dict

[](#diffusers.loaders.Mochi1LoraLoaderMixin.lora_state_dict)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L2601)

( pretrained\_model\_name\_or\_path\_or\_dict: typing.Union\[str, typing.Dict\[str, torch.Tensor\]\]\*\*kwargs )

Expand 8 parameters

Parameters

*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.lora_state_dict.pretrained_model_name_or_path_or_dict)**pretrained\_model\_name\_or\_path\_or\_dict** (`str` or `os.PathLike` or `dict`) — Can be either:
    
    *   A string, the _model id_ (for example `google/ddpm-celebahq-256`) of a pretrained model hosted on the Hub.
    *   A path to a _directory_ (for example `./my_model_directory`) containing the model weights saved with [ModelMixin.save\_pretrained()](/docs/diffusers/v0.32.2/en/api/models/overview#diffusers.ModelMixin.save_pretrained).
    *   A [torch state dict](https://pytorch.org/tutorials/beginner/saving_loading_models.html#what-is-a-state-dict).
    
*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.lora_state_dict.cache_dir)**cache\_dir** (`Union[str, os.PathLike]`, _optional_) — Path to a directory where a downloaded pretrained model configuration is cached if the standard cache is not used.
*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.lora_state_dict.force_download)**force\_download** (`bool`, _optional_, defaults to `False`) — Whether or not to force the (re-)download of the model weights and configuration files, overriding the cached versions if they exist.
*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.lora_state_dict.proxies)**proxies** (`Dict[str, str]`, _optional_) — A dictionary of proxy servers to use by protocol or endpoint, for example, `{'http': 'foo.bar:3128', 'http://hostname': 'foo.bar:4012'}`. The proxies are used on each request.
*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.lora_state_dict.local_files_only)**local\_files\_only** (`bool`, _optional_, defaults to `False`) — Whether to only load local model weights and configuration files or not. If set to `True`, the model won’t be downloaded from the Hub.
*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.lora_state_dict.token)**token** (`str` or _bool_, _optional_) — The token to use as HTTP bearer authorization for remote files. If `True`, the token generated from `diffusers-cli login` (stored in `~/.huggingface`) is used.
*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.lora_state_dict.revision)**revision** (`str`, _optional_, defaults to `"main"`) — The specific model version to use. It can be a branch name, a tag name, a commit id, or any identifier allowed by Git.
*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.lora_state_dict.subfolder)**subfolder** (`str`, _optional_, defaults to `""`) — The subfolder location of a model file within a larger model repository on the Hub or locally.

Return state dict for lora weights and the network alphas.

We support loading A1111 formatted LoRA checkpoints in a limited capacity.

This function is experimental and might change in the future.

#### save\_lora\_weights

[](#diffusers.loaders.Mochi1LoraLoaderMixin.save_lora_weights)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L2787)

( save\_directory: typing.Union\[str, os.PathLike\]transformer\_lora\_layers: typing.Dict\[str, typing.Union\[torch.nn.modules.module.Module, torch.Tensor\]\] = Noneis\_main\_process: bool = Trueweight\_name: str = Nonesave\_function: typing.Callable = Nonesafe\_serialization: bool = True )

Parameters

*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.save_lora_weights.save_directory)**save\_directory** (`str` or `os.PathLike`) — Directory to save LoRA parameters to. Will be created if it doesn’t exist.
*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.save_lora_weights.transformer_lora_layers)**transformer\_lora\_layers** (`Dict[str, torch.nn.Module]` or `Dict[str, torch.Tensor]`) — State dict of the LoRA layers corresponding to the `transformer`.
*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.save_lora_weights.is_main_process)**is\_main\_process** (`bool`, _optional_, defaults to `True`) — Whether the process calling this is the main process or not. Useful during distributed training and you need to call this function on all processes. In this case, set `is_main_process=True` only on the main process to avoid race conditions.
*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.save_lora_weights.save_function)**save\_function** (`Callable`) — The function to use to save the state dictionary. Useful during distributed training when you need to replace `torch.save` with another method. Can be configured with the environment variable `DIFFUSERS_SAVE_MODE`.
*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.save_lora_weights.safe_serialization)**safe\_serialization** (`bool`, _optional_, defaults to `True`) — Whether to save the model using `safetensors` or the traditional PyTorch way with `pickle`.

Save the LoRA parameters corresponding to the UNet and text encoder.

#### unfuse\_lora

[](#diffusers.loaders.Mochi1LoraLoaderMixin.unfuse_lora)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L2878)

( components: typing.List\[str\] = \['transformer'\]\*\*kwargs )

Parameters

*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.unfuse_lora.components)**components** (`List[str]`) — List of LoRA-injectable components to unfuse LoRA from.
*   [](#diffusers.loaders.Mochi1LoraLoaderMixin.unfuse_lora.unfuse_transformer)**unfuse\_transformer** (`bool`, defaults to `True`) — Whether to unfuse the UNet LoRA parameters.

Reverses the effect of [`pipe.fuse_lora()`](https://huggingface.co/docs/diffusers/main/en/api/loaders#diffusers.loaders.LoraBaseMixin.fuse_lora).

This is an experimental API.

[](#diffusers.loaders.AmusedLoraLoaderMixin)AmusedLoraLoaderMixin
-----------------------------------------------------------------

### class diffusers.loaders.AmusedLoraLoaderMixin

[](#diffusers.loaders.AmusedLoraLoaderMixin)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L2137)

( )

#### load\_lora\_into\_transformer

[](#diffusers.loaders.AmusedLoraLoaderMixin.load_lora_into_transformer)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_pipeline.py#L2142)

( state\_dictnetwork\_alphastransformeradapter\_name = None\_pipeline = Nonelow\_cpu\_mem\_usage = False )

Parameters

*   [](#diffusers.loaders.AmusedLoraLoaderMixin.load_lora_into_transformer.state_dict)**state\_dict** (`dict`) — A standard state dict containing the lora layer parameters. The keys can either be indexed directly into the unet or prefixed with an additional `unet` which can be used to distinguish between text encoder lora layers.
*   [](#diffusers.loaders.AmusedLoraLoaderMixin.load_lora_into_transformer.network_alphas)**network\_alphas** (`Dict[str, float]`) — The value of the network alpha used for stable learning and preventing underflow. This value has the same meaning as the `--network_alpha` option in the kohya-ss trainer script. Refer to [this link](https://github.com/darkstorm2150/sd-scripts/blob/main/docs/train_network_README-en.md#execute-learning).
*   [](#diffusers.loaders.AmusedLoraLoaderMixin.load_lora_into_transformer.transformer)**transformer** (`UVit2DModel`) — The Transformer model to load the LoRA layers into.
*   [](#diffusers.loaders.AmusedLoraLoaderMixin.load_lora_into_transformer.adapter_name)**adapter\_name** (`str`, _optional_) — Adapter name to be used for referencing the loaded adapter model. If not specified, it will use `default_{i}` where i is the total number of adapters being loaded.
*   [](#diffusers.loaders.AmusedLoraLoaderMixin.load_lora_into_transformer.low_cpu_mem_usage)**low\_cpu\_mem\_usage** (`bool`, _optional_) — Speed up model loading by only loading the pretrained LoRA weights and not initializing the random weights.

This will load the LoRA layers specified in `state_dict` into `transformer`.

[](#diffusers.loaders.lora_base.LoraBaseMixin)LoraBaseMixin
-----------------------------------------------------------

### class diffusers.loaders.lora\_base.LoraBaseMixin

[](#diffusers.loaders.lora_base.LoraBaseMixin)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_base.py#L455)

( )

Utility class for handling LoRAs.

#### delete\_adapters

[](#diffusers.loaders.lora_base.LoraBaseMixin.delete_adapters)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_base.py#L750)

( adapter\_names: typing.Union\[typing.List\[str\], str\] )

Parameters

*   [](#diffusers.loaders.lora_base.LoraBaseMixin.delete_adapters.Deletes)**Deletes** the LoRA layers of `adapter_name` for the unet and text-encoder(s). — adapter\_names (`Union[List[str], str]`): The names of the adapter to delete. Can be a single string or a list of strings

#### fuse\_lora

[](#diffusers.loaders.lora_base.LoraBaseMixin.fuse_lora)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_base.py#L522)

( components: typing.List\[str\] = \[\]lora\_scale: float = 1.0safe\_fusing: bool = Falseadapter\_names: typing.Optional\[typing.List\[str\]\] = None\*\*kwargs )

Parameters

*   [](#diffusers.loaders.lora_base.LoraBaseMixin.fuse_lora.components)**components** — (`List[str]`): List of LoRA-injectable components to fuse the LoRAs into.
*   [](#diffusers.loaders.lora_base.LoraBaseMixin.fuse_lora.lora_scale)**lora\_scale** (`float`, defaults to 1.0) — Controls how much to influence the outputs with the LoRA parameters.
*   [](#diffusers.loaders.lora_base.LoraBaseMixin.fuse_lora.safe_fusing)**safe\_fusing** (`bool`, defaults to `False`) — Whether to check fused weights for NaN values before fusing and if values are NaN not fusing them.
*   [](#diffusers.loaders.lora_base.LoraBaseMixin.fuse_lora.adapter_names)**adapter\_names** (`List[str]`, _optional_) — Adapter names to be used for fusing. If nothing is passed, all active adapters will be fused.

Fuses the LoRA parameters into the original parameters of the corresponding blocks.

This is an experimental API.

[](#diffusers.loaders.lora_base.LoraBaseMixin.fuse_lora.example)

Example:

Copied

from diffusers import DiffusionPipeline
import torch

pipeline = DiffusionPipeline.from\_pretrained(
    "stabilityai/stable-diffusion-xl-base-1.0", torch\_dtype=torch.float16
).to("cuda")
pipeline.load\_lora\_weights("nerijs/pixel-art-xl", weight\_name="pixel-art-xl.safetensors", adapter\_name="pixel")
pipeline.fuse\_lora(lora\_scale=0.7)

#### get\_active\_adapters

[](#diffusers.loaders.lora_base.LoraBaseMixin.get_active_adapters)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_base.py#L772)

( )

Gets the list of the current active adapters.

[](#diffusers.loaders.lora_base.LoraBaseMixin.get_active_adapters.example)

Example:

Copied

from diffusers import DiffusionPipeline

pipeline = DiffusionPipeline.from\_pretrained(
    "stabilityai/stable-diffusion-xl-base-1.0",
).to("cuda")
pipeline.load\_lora\_weights("CiroN2022/toy-face", weight\_name="toy\_face\_sdxl.safetensors", adapter\_name="toy")
pipeline.get\_active\_adapters()

#### get\_list\_adapters

[](#diffusers.loaders.lora_base.LoraBaseMixin.get_list_adapters)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_base.py#L805)

( )

Gets the current list of all available adapters in the pipeline.

#### set\_lora\_device

[](#diffusers.loaders.lora_base.LoraBaseMixin.set_lora_device)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_base.py#L827)

( adapter\_names: typing.List\[str\]device: typing.Union\[torch.device, str, int\] )

Parameters

*   [](#diffusers.loaders.lora_base.LoraBaseMixin.set_lora_device.adapter_names)**adapter\_names** (`List[str]`) — List of adapters to send device to.
*   [](#diffusers.loaders.lora_base.LoraBaseMixin.set_lora_device.device)**device** (`Union[torch.device, str, int]`) — Device to send the adapters to. Can be either a torch device, a str or an integer.

Moves the LoRAs listed in `adapter_names` to a target device. Useful for offloading the LoRA to the CPU in case you want to load multiple adapters and free some GPU memory.

#### unfuse\_lora

[](#diffusers.loaders.lora_base.LoraBaseMixin.unfuse_lora)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_base.py#L603)

( components: typing.List\[str\] = \[\]\*\*kwargs )

Parameters

*   [](#diffusers.loaders.lora_base.LoraBaseMixin.unfuse_lora.components)**components** (`List[str]`) — List of LoRA-injectable components to unfuse LoRA from.
*   [](#diffusers.loaders.lora_base.LoraBaseMixin.unfuse_lora.unfuse_unet)**unfuse\_unet** (`bool`, defaults to `True`) — Whether to unfuse the UNet LoRA parameters.
*   [](#diffusers.loaders.lora_base.LoraBaseMixin.unfuse_lora.unfuse_text_encoder)**unfuse\_text\_encoder** (`bool`, defaults to `True`) — Whether to unfuse the text encoder LoRA parameters. If the text encoder wasn’t monkey-patched with the LoRA parameters then it won’t have any effect.

Reverses the effect of [`pipe.fuse_lora()`](https://huggingface.co/docs/diffusers/main/en/api/loaders#diffusers.loaders.LoraBaseMixin.fuse_lora).

This is an experimental API.

#### unload\_lora\_weights

[](#diffusers.loaders.lora_base.LoraBaseMixin.unload_lora_weights)[< source \>](https://github.com/huggingface/diffusers/blob/v0.32.2/src/diffusers/loaders/lora_base.py#L499)

( )

Unloads the LoRA parameters.

[](#diffusers.loaders.lora_base.LoraBaseMixin.unload_lora_weights.example)

Examples:

Copied

\>>> \# Assuming \`pipeline\` is already loaded with the LoRA parameters.
\>>> pipeline.unload\_lora\_weights()
\>>> ...

[< \> Update on GitHub](https://github.com/huggingface/diffusers/blob/main/docs/source/en/api/loaders/lora.md)

[←IP-Adapter](/docs/diffusers/v0.32.2/en/api/loaders/ip_adapter) [Single files→](/docs/diffusers/v0.32.2/en/api/loaders/single_file)