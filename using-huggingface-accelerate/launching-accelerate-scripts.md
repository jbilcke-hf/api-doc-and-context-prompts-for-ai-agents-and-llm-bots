[](#launching-accelerate-scripts)Launching Accelerate scripts
=============================================================

In the previous tutorial, you were introduced to how to modify your current training script to use Accelerate. The final version of that code is shown below:

Copied

from accelerate import Accelerator

accelerator = Accelerator()

model, optimizer, training\_dataloader, scheduler = accelerator.prepare(
    model, optimizer, training\_dataloader, scheduler
)

for batch in training\_dataloader:
    optimizer.zero\_grad()
    inputs, targets = batch
    outputs = model(inputs)
    loss = loss\_function(outputs, targets)
    accelerator.backward(loss)
    optimizer.step()
    scheduler.step()

But how do you run this code and have it utilize the special hardware available to it?

First, you should rewrite the above code into a function, and make it callable as a script. For example:

Copied

  from accelerate import Accelerator
  
\+ def main():
      accelerator = Accelerator()

      model, optimizer, training\_dataloader, scheduler = accelerator.prepare(
          model, optimizer, training\_dataloader, scheduler
      )

      for batch in training\_dataloader:
          optimizer.zero\_grad()
          inputs, targets = batch
          outputs = model(inputs)
          loss = loss\_function(outputs, targets)
          accelerator.backward(loss)
          optimizer.step()
          scheduler.step()

\+ if \_\_name\_\_ == "\_\_main\_\_":
\+     main()

Next, you need to launch it with `accelerate launch`.

It’s recommended you run `accelerate config` before using `accelerate launch` to configure your environment to your liking. Otherwise Accelerate will use very basic defaults depending on your system setup.

[](#using-accelerate-launch)Using accelerate launch
---------------------------------------------------

Accelerate has a special CLI command to help you launch your code in your system through `accelerate launch`. This command wraps around all of the different commands needed to launch your script on various platforms, without you having to remember what each of them is.

If you are familiar with launching scripts in PyTorch yourself such as with `torchrun`, you can still do this. It is not required to use `accelerate launch`.

You can launch your script quickly by using:

Copied

accelerate launch {script\_name.py} --arg1 --arg2 ...

Just put `accelerate launch` at the start of your command, and pass in additional arguments and parameters to your script afterward like normal!

Since this runs the various torch spawn methods, all of the expected environment variables can be modified here as well. For example, here is how to use `accelerate launch` with a single GPU:

Copied

\# for cuda device:
CUDA\_VISIBLE\_DEVICES="0" accelerate launch {script\_name.py} --arg1 --arg2 ...
\# for xpu device:
ZE\_AFFINITY\_MASK="0" accelerate launch {script\_name.py} --arg1 --arg2 ...

You can also use `accelerate launch` without performing `accelerate config` first, but you may need to manually pass in the right configuration parameters. In this case, Accelerate will make some hyperparameter decisions for you, e.g., if GPUs are available, it will use all of them by default without the mixed precision. Here is how you would use all GPUs and train with mixed precision disabled:

Copied

accelerate launch --multi\_gpu {script\_name.py} {--arg1} {--arg2} ...

Or by specifying a number of GPUs to use:

Copied

accelerate launch --num\_processes=2 {script\_name.py} {--arg1} {--arg2} ...

To get more specific you should pass in the needed parameters yourself. For instance, here is how you would also launch that same script on two GPUs using mixed precision while avoiding all of the warnings:

Copied

accelerate launch --multi\_gpu --mixed\_precision=fp16 --num\_processes=2 {script\_name.py} {--arg1} {--arg2} ...

For a complete list of parameters you can pass in, run:

Copied

accelerate launch -h

Even if you are not using Accelerate in your code, you can still use the launcher for starting your scripts!

For a visualization of this difference, that earlier `accelerate launch` on multi-gpu would look something like so with `torchrun`:

Copied

MIXED\_PRECISION="fp16" torchrun --nproc\_per\_node=2 --nnodes=1 {script\_name.py} {--arg1} {--arg2} ...

You can also launch your script utilizing the launch CLI as a python module itself, enabling the ability to pass in other python-specific launching behaviors. To do so, use `accelerate.commands.launch` instead of `accelerate launch`:

Copied

python -m accelerate.commands.launch --num\_processes=2 {script\_name.py} {--arg1} {--arg2}

If you want to execute the script with any other python flags, you can pass them in as well similar to `-m`, such as the below example enabling unbuffered stdout and stderr:

Copied

python -u -m accelerate.commands.launch --num\_processes=2 {script\_name.py} {--arg1} {--arg2}

You can run your code on CPU as well! This is helpful for debugging and testing purposes on toy models and datasets.

Copied

accelerate launch --cpu {script\_name.py} {--arg1} {--arg2}

[](#why-you-should-always-use-accelerate-config)Why you should always use accelerate config
-------------------------------------------------------------------------------------------

Why is it useful to the point you should **always** run `accelerate config`?

Remember that earlier call to `accelerate launch` as well as `torchrun`? Post configuration, to run that script with the needed parts you just need to use `accelerate launch` outright, without passing anything else in:

Copied

accelerate launch {script\_name.py} {--arg1} {--arg2} ...

[](#custom-configurations)Custom Configurations
-----------------------------------------------

As briefly mentioned earlier, `accelerate launch` should be mostly used through combining set configurations made with the `accelerate config` command. These configs are saved to a `default_config.yaml` file in your cache folder for Accelerate. This cache folder is located at (with decreasing order of priority):

*   The content of your environment variable `HF_HOME` suffixed with `accelerate`.
*   If it does not exist, the content of your environment variable `XDG_CACHE_HOME` suffixed with `huggingface/accelerate`.
*   If this does not exist either, the folder `~/.cache/huggingface/accelerate`.

To have multiple configurations, the flag `--config_file` can be passed to the `accelerate launch` command paired with the location of the custom yaml.

An example yaml may look something like the following for two GPUs on a single machine using `fp16` for mixed precision:

Copied

compute\_environment: LOCAL\_MACHINE
deepspeed\_config: {}
distributed\_type: MULTI\_GPU
fsdp\_config: {}
machine\_rank: 0
main\_process\_ip: null
main\_process\_port: null
main\_training\_function: main
mixed\_precision: fp16
num\_machines: 1
num\_processes: 2
use\_cpu: false

Launching a script from the location of that custom yaml file looks like the following:

Copied

accelerate launch --config\_file {path/to/config/my\_config\_file.yaml} {script\_name.py} {--arg1} {--arg2} ...

[](#multi-node-training)Multi-node training
-------------------------------------------

Multi-node training with Accelerate is similar to [multi-node training with torchrun](https://pytorch.org/tutorials/intermediate/ddp_series_multinode.html). The simplest way to launch a multi-node training run is to do the following:

*   Copy your codebase and data to all nodes. (or place them on a shared filesystem)
*   Setup your python packages on all nodes.
*   Run `accelerate config` on the main single node first. After specifying the number of nodes, you will be asked to specify the rank of each node (this will be 0 for the main/master node), along with the IP address and port for the main process. This is required for the worker nodes to communicate with the main process. Afterwards, you can copy or send this config file across all of your nodes, changing the `machine_rank` to 1, 2,3, etc. to avoid having to run the command (or just follow their directions directly for launching with `torchrun` as well)

Once you have done this, you can start your multi-node training run by running `accelerate launch` (or `torchrun`) on all nodes.

It is required that the command be ran on all nodes for everything to start, not just running it from the main node. You can use something like SLURM or a different process executor to wrap around this requirement and call everything from a single command.

It is recommended to use the intranet IP of your main node over the public IP for better latency. This is the `192.168.x.x` or the `172.x.x.x` address you see when you run `hostname -I` on the main node.

To get a better idea about multi-node training, check out our example for [multi-node training with FSDP](https://huggingface.co/blog/ram-efficient-pytorch-fsdp).

[< \> Update on GitHub](https://github.com/huggingface/accelerate/blob/main/docs/source/basic_tutorials/launch.md)

[←TPU training](/docs/accelerate/basic_tutorials/tpu) [Launching distributed training from Jupyter Notebooks→](/docs/accelerate/basic_tutorials/notebook)