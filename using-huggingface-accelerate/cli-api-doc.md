[](#the-command-line)The Command Line
=====================================

Below is a list of all the available commands 🤗 Accelerate with their parameters

[](#accelerate-config)accelerate config
---------------------------------------

**Command**:

`accelerate config` or `accelerate-config`

Launches a series of prompts to create and save a `default_config.yml` configuration file for your training system. Should always be ran first on your machine.

**Usage**:

Copied

accelerate config \[arguments\]

**Optional Arguments**:

*   `--config_file CONFIG_FILE` (`str`) — The path to use to store the config file. Will default to a file named default\_config.yaml in the cache location, which is the content of the environment `HF_HOME` suffixed with ‘accelerate’, or if you don’t have such an environment variable, your cache directory (`~/.cache` or the content of `XDG_CACHE_HOME`) suffixed with `huggingface`.
*   `-h`, `--help` (`bool`) — Show a help message and exit

[](#accelerate-config-default)accelerate config default
-------------------------------------------------------

**Command**:

`accelerate config default` or `accelerate-config default`

Create a default config file for Accelerate with only a few flags set.

**Usage**:

Copied

accelerate config default \[arguments\]

**Optional Arguments**:

*   `--config_file CONFIG_FILE` (`str`) — The path to use to store the config file. Will default to a file named default\_config.yaml in the cache location, which is the content of the environment `HF_HOME` suffixed with ‘accelerate’, or if you don’t have such an environment variable, your cache directory (`~/.cache` or the content of `XDG_CACHE_HOME`) suffixed with `huggingface`.
    
*   `-h`, `--help` (`bool`) — Show a help message and exit
    
*   `--mixed_precision {no,fp16,bf16}` (`str`) — Whether or not to use mixed precision training. Choose between FP16 and BF16 (bfloat16) training. BF16 training is only supported on Nvidia Ampere GPUs and PyTorch 1.10 or later.
    

[](#accelerate-config-update)accelerate config update
-----------------------------------------------------

**Command**:

`accelerate config update` or `accelerate-config update`

Update an existing config file with the latest defaults while maintaining the old configuration.

**Usage**:

Copied

accelerate config update \[arguments\]

**Optional Arguments**:

*   `--config_file CONFIG_FILE` (`str`) — The path to the config file to update. Will default to a file named default\_config.yaml in the cache location, which is the content of the environment `HF_HOME` suffixed with ‘accelerate’, or if you don’t have such an environment variable, your cache directory (`~/.cache` or the content of `XDG_CACHE_HOME`) suffixed with `huggingface`.
    
*   `-h`, `--help` (`bool`) — Show a help message and exit
    

[](#accelerate-env)accelerate env
---------------------------------

**Command**:

`accelerate env` or `accelerate-env` or `python -m accelerate.commands.env`

Lists the contents of the passed 🤗 Accelerate configuration file. Should always be used when opening an issue on the [GitHub repository](https://github.com/huggingface/accelerate).

**Usage**:

Copied

accelerate env \[arguments\]

**Optional Arguments**:

*   `--config_file CONFIG_FILE` (`str`) — The path to use to store the config file. Will default to a file named default\_config.yaml in the cache location, which is the content of the environment `HF_HOME` suffixed with ‘accelerate’, or if you don’t have such an environment variable, your cache directory (`~/.cache` or the content of `XDG_CACHE_HOME`) suffixed with `huggingface`.
*   `-h`, `--help` (`bool`) — Show a help message and exit

[](#accelerate-launch)accelerate launch
---------------------------------------

**Command**:

`accelerate launch` or `accelerate-launch` or `python -m accelerate.commands.launch`

Launches a specified script on a distributed system with the right parameters.

**Usage**:

Copied

accelerate launch \[arguments\] {training\_script} --{training\_script-argument-1} --{training\_script-argument-2} ...

**Positional Arguments**:

*   `{training_script}` — The full path to the script to be launched in parallel
*   `--{training_script-argument-1}` — Arguments of the training script

**Optional Arguments**:

*   `-h`, `--help` (`bool`) — Show a help message and exit
*   `--config_file CONFIG_FILE` (`str`)— The config file to use for the default values in the launching script.
*   `-m`, `--module` (`bool`) — Change each process to interpret the launch script as a Python module, executing with the same behavior as ‘python -m’.
*   `--no_python` (`bool`) — Skip prepending the training script with ‘python’ - just execute it directly. Useful when the script is not a Python script.
*   `--debug` (`bool`) — Whether to print out the torch.distributed stack trace when something fails.
*   `-q`, `--quiet` (`bool`) — Silence subprocess errors from the launch stack trace to only show the relevant tracebacks. (Only applicable to DeepSpeed and single-process configurations).

The rest of these arguments are configured through `accelerate config` and are read in from the specified `--config_file` (or default configuration) for their values. They can also be passed in manually.

**Hardware Selection Arguments**:

*   `--cpu` (`bool`) — Whether or not to force the training on the CPU.
*   `--multi_gpu` (`bool`) — Whether or not this should launch a distributed GPU training.
*   `--tpu` (`bool`) — Whether or not this should launch a TPU training.
*   `--ipex` (`bool`) — Whether or not this should launch an Intel Pytorch Extension (IPEX) training.

**Resource Selection Arguments**:

The following arguments are useful for fine-tuning how available hardware should be used

*   `--mixed_precision {no,fp16,bf16,fp8}` (`str`) — Whether or not to use mixed precision training. Choose between FP16 and BF16 (bfloat16) training. BF16 training is only supported on Nvidia Ampere GPUs and PyTorch 1.10 or later.
*   `--num_processes NUM_PROCESSES` (`int`) — The total number of processes to be launched in parallel.
*   `--num_machines NUM_MACHINES` (`int`) — The total number of machines used in this training.
*   `--num_cpu_threads_per_process NUM_CPU_THREADS_PER_PROCESS` (`int`) — The number of CPU threads per process. Can be tuned for optimal performance.
*   `--enable_cpu_affinity` (`bool`) — Whether or not CPU affinity and balancing should be enabled. Currently only supported on NVIDIA hardware.

**Training Paradigm Arguments**:

The following arguments are useful for selecting which training paradigm to use.

*   `--use_deepspeed` (`bool`) — Whether or not to use DeepSpeed for training.
*   `--use_fsdp` (`bool`) — Whether or not to use FullyShardedDataParallel for training.
*   `--use_megatron_lm` (`bool`) — Whether or not to use Megatron-LM for training.
*   `--use_xpu` (`bool`) — Whether to use IPEX plugin to speed up training on XPU specifically.

**Distributed GPU Arguments**:

The following arguments are only useful when `multi_gpu` is passed or multi-gpu training is configured through `accelerate config`:

*   `--gpu_ids` (`str`) — What GPUs (by id) should be used for training on this machine as a comma-seperated list
*   `--same_network` (`bool`) — Whether all machines used for multinode training exist on the same local network.
*   `--machine_rank` (`int`) — The rank of the machine on which this script is launched.
*   `--main_process_ip` (`str`) — The IP address of the machine of rank 0.
*   `--main_process_port` (`int`) — The port to use to communicate with the machine of rank 0.
*   `-t`, `--tee` (`str`) — Tee std streams into a log file and also to console.
*   `--log_dir` (`str`) — Base directory to use for log files when using torchrun/torch.distributed.run as launcher. Use with —tee to redirect std streams info log files.
*   `--role` (`str`) — User-defined role for the workers.
*   `--rdzv_backend` (`str`) — The rendezvous method to use, such as ‘static’ (the default) or ‘c10d’
*   `--rdzv_conf` (`str`) — Additional rendezvous configuration (<key1>=<value1>,<key2>=<value2>,…).
*   `--max_restarts` (`int`) — Maximum number of worker group restarts before failing.
*   `--monitor_interval` (`int`) — Interval, in seconds, to monitor the state of workers.

**TPU Arguments**:

The following arguments are only useful when `tpu` is passed or TPU training is configured through `accelerate config`:

*   `--tpu_cluster` (`bool`) — Whether to use a GCP TPU pod for training.
*   `--tpu_use_sudo` (`bool`) — Whether to use `sudo` when running the TPU training script in each pod.
*   `--vm` (`str`) — List of single Compute VM instance names. If not provided we assume usage of instance groups. For TPU pods.
*   `--env` (`str`) — List of environment variables to set on the Compute VM instances. For TPU pods.
*   `--main_training_function` (`str`) — The name of the main function to be executed in your script (only for TPU training).
*   `--downcast_bf16` (`bool`) — Whether when using bf16 precision on TPUs if both float and double tensors are cast to bfloat16 or if double tensors remain as float32.

**DeepSpeed Arguments**:

The following arguments are only useful when `use_deepspeed` is passed or `deepspeed` is configured through `accelerate config`:

*   `--deepspeed_config_file` (`str`) — DeepSpeed config file.
*   `--zero_stage` (`int`) — DeepSpeed’s ZeRO optimization stage.
*   `--offload_optimizer_device` (`str`) — Decides where (none|cpu|nvme) to offload optimizer states.
*   `--offload_param_device` (`str`) — Decides where (none|cpu|nvme) to offload parameters.
*   `--offload_optimizer_nvme_path` (`str`) — Decides Nvme Path to offload optimizer states.
*   `--gradient_accumulation_steps` (`int`) — No of gradient\_accumulation\_steps used in your training script.
*   `--gradient_clipping` (`float`) — Gradient clipping value used in your training script.
*   `--zero3_init_flag` (`str`) — Decides Whether (true|false) to enable `deepspeed.zero.Init` for constructing massive models. Only applicable with DeepSpeed ZeRO Stage-3.
*   `--zero3_save_16bit_model` (`str`) — Decides Whether (true|false) to save 16-bit model weights when using ZeRO Stage-3. Only applicable with DeepSpeed ZeRO Stage-3.
*   `--deepspeed_hostfile` (`str`) — DeepSpeed hostfile for configuring multi-node compute resources.
*   `--deepspeed_exclusion_filter` (`str`) — DeepSpeed exclusion filter string when using mutli-node setup.
*   `--deepspeed_inclusion_filter` (`str`) — DeepSpeed inclusion filter string when using mutli-node setup.
*   `--deepspeed_multinode_launcher` (`str`) — DeepSpeed multi-node launcher to use.
*   `--deepspeed_moe_layer_cls_names` (`str`) — comma-separated list of transformer MoE layer class names (case-sensitive) to wrap, e.g, `MixtralSparseMoeBlock` `Qwen2MoeSparseMoeBlock`, `JetMoEAttention,JetMoEBlock`

**Fully Sharded Data Parallelism Arguments**:

The following arguments are only useful when `use_fsdp` is passed or Fully Sharded Data Parallelism is configured through `accelerate config`:

*   `--fsdp_offload_params` (`str`) — Decides Whether (true|false) to offload parameters and gradients to CPU.
*   `--fsdp_min_num_params` (`int`) — FSDP’s minimum number of parameters for Default Auto Wrapping.
*   `--fsdp_sharding_strategy` (`int`) — FSDP’s Sharding Strategy.
*   `--fsdp_auto_wrap_policy` (`str`) — FSDP’s auto wrap policy.
*   `--fsdp_transformer_layer_cls_to_wrap` (`str`) — Transformer layer class name (case-sensitive) to wrap, e.g, `BertLayer`, `GPTJBlock`, `T5Block` …
*   `--fsdp_backward_prefetch_policy` (`str`) — FSDP’s backward prefetch policy.
*   `--fsdp_state_dict_type` (`str`) — FSDP’s state dict type.
*   `--fsdp_forward_prefetch` (`str`) — FSDP forward prefetch.
*   `--fsdp_use_orig_params` (`str`) — If True, allows non-uniform `requires_grad` mixed in a FSDP unit.
*   `--fsdp_cpu_ram_efficient_loading` (`str`) — If true, only the first process loads the pretrained model checkoint while all other processes have empty weights. When using this, `--fsdp_sync_module_states` needs to True.
*   `--fsdp_sync_module_states` (`str`) — If true, each individually wrapped FSDP unit will broadcast module parameters from rank 0.
*   `--fsdp_activation_checkpointing` (`bool`) — Decides Whether intermediate activations are freed during the forward pass, and a checkpoint is left as a placeholder

**Megatron-LM Arguments**:

The following arguments are only useful when `use_megatron_lm` is passed or Megatron-LM is configured through `accelerate config`:

*   `--megatron_lm_tp_degree` (“) — Megatron-LM’s Tensor Parallelism (TP) degree.
*   `--megatron_lm_pp_degree` (“) — Megatron-LM’s Pipeline Parallelism (PP) degree.
*   `--megatron_lm_num_micro_batches` (“) — Megatron-LM’s number of micro batches when PP degree > 1.
*   `--megatron_lm_sequence_parallelism` (“) — Decides Whether (true|false) to enable Sequence Parallelism when TP degree > 1.
*   `--megatron_lm_recompute_activations` (“) — Decides Whether (true|false) to enable Selective Activation Recomputation.
*   `--megatron_lm_use_distributed_optimizer` (“) — Decides Whether (true|false) to use distributed optimizer which shards optimizer state and gradients across Data Parallel (DP) ranks.
*   `--megatron_lm_gradient_clipping` (“) — Megatron-LM’s gradient clipping value based on global L2 Norm (0 to disable).

**FP8 Arguments**:

*   `--fp8_backend` (`str`) — Choose a backend to train with FP8 (`te` or `msamp`)
*   `--fp8_use_autocast_during_eval` (`bool`) — Whether to use FP8 autocast during eval mode (useful only when `--fp8_backend=te` is passed). Generally better metrics are found when this is not passed.
*   `--fp8_margin` (`int`) — The margin to use for the gradient scaling (useful only when `--fp8_backend=te` is passed).
*   `--fp8_interval` (`int`) — The interval to use for how often the scaling factor is recomputed (useful only when `--fp8_backend=te` is passed).
*   `--fp8_format` (`str`) — The format to use for the FP8 recipe (useful only when `--fp8_backend=te` is passed).
*   `--fp8_amax_history_len` (`int`) — The length of the history to use for the scaling factor computation (useful only when `--fp8_backend=te` is passed).
*   `--fp8_amax_compute_algo` (`str`) — The algorithm to use for the scaling factor computation. (useful only when `--fp8_backend=te` is passed).
*   `--fp8_override_linear_precision` (`Tuple[bool, bool, bool]`) — Whether or not to execute `fprop`, `dgrad`, and `wgrad` GEMMS in higher precision.
*   `--fp8_opt_level` (`str`) — What level of 8-bit collective communication should be used with MS-AMP (useful only when `--fp8_backend=msamp` is passed)

**AWS SageMaker Arguments**:

The following arguments are only useful when training in SageMaker

*   `--aws_access_key_id AWS_ACCESS_KEY_ID` (`str`) — The AWS\_ACCESS\_KEY\_ID used to launch the Amazon SageMaker training job
*   `--aws_secret_access_key AWS_SECRET_ACCESS_KEY` (`str`) — The AWS\_SECRET\_ACCESS\_KEY used to launch the Amazon SageMaker training job

[](#accelerate-estimate-memory)accelerate estimate-memory
---------------------------------------------------------

**Command**:

`accelerate estimate-memory` or `accelerate-estimate-memory` or `python -m accelerate.commands.estimate`

Estimates the total vRAM a particular model hosted on the Hub needs to be loaded in with an estimate for training. Requires that `huggingface_hub` be installed.

When performing inference, typically add ≤20% to the result as overall allocation [as referenced here](https://blog.eleuther.ai/transformer-math/). We will have more extensive estimations in the future that will automatically be included in the calculation.

**Usage**:

Copied

accelerate estimate-memory {MODEL\_NAME} --library\_name {LIBRARY\_NAME} --dtypes {dtype\_1} {dtype\_2} ...

**Required Arguments**:

*   `MODEL_NAME` (`str`)— The model name on the Hugging Face Hub

**Optional Arguments**:

*   `--library_name {timm,transformers}` (`str`) — The library the model has an integration with, such as `transformers`, needed only if this information is not stored on the Hub
*   `--dtypes {float32,float16,int8,int4}` (`[{float32,float16,int8,int4} ...]`) — The dtypes to use for the model, must be one (or many) of `float32`, `float16`, `int8`, and `int4`
*   `--trust_remote_code` (`bool`) — Whether or not to allow for custom models defined on the Hub in their own modeling files. This option should only be passed for repositories you trust and in which you have read the code, as it will execute code present on the Hub on your local machine.

[](#accelerate-tpu-config)accelerate tpu-config
-----------------------------------------------

`accelerate tpu-config`

**Usage**:

Copied

accelerate tpu-config \[arguments\]

**Optional Arguments**:

*   `-h`, `--help` (`bool`) — Show a help message and exit

**Config Arguments**:

Arguments that can be configured through `accelerate config`.

*   `--config_file` (`str`) — Path to the config file to use for accelerate.
*   `--tpu_name` (`str`) — The name of the TPU to use. If not specified, will use the TPU specified in the config file.
*   `--tpu_zone` (`str`) — The zone of the TPU to use. If not specified, will use the zone specified in the config file.

**TPU Arguments**:

Arguments for options ran inside the TPU.

*   `--command_file` (`str`) — The path to the file containing the commands to run on the pod on startup.
*   `--command` (`str`) — A command to run on the pod. Can be passed multiple times.
*   `--install_accelerate` (`bool`) — Whether to install accelerate on the pod. Defaults to False.
*   `--accelerate_version` (`str`) — The version of accelerate to install on the pod. If not specified, will use the latest pypi version. Specify ‘dev’ to install from GitHub.
*   `--debug` (`bool`) — If set, will print the command that would be run instead of running it.

[](#accelerate-test)accelerate test
-----------------------------------

`accelerate test` or `accelerate-test`

Runs `accelerate/test_utils/test_script.py` to verify that 🤗 Accelerate has been properly configured on your system and runs.

**Usage**:

Copied

accelerate test \[arguments\]

**Optional Arguments**:

*   `--config_file CONFIG_FILE` (`str`) — The path to use to store the config file. Will default to a file named default\_config.yaml in the cache location, which is the content of the environment `HF_HOME` suffixed with ‘accelerate’, or if you don’t have such an environment variable, your cache directory (`~/.cache` or the content of `XDG_CACHE_HOME`) suffixed with `huggingface`.
*   `-h`, `--help` (`bool`) — Show a help message and exit

[< \> Update on GitHub](https://github.com/huggingface/accelerate/blob/main/docs/source/package_reference/cli.md)

Quicktour