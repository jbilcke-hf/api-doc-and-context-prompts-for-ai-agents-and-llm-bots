[](#installation)Installation
=============================

Before you start, you will need to setup your environment, install the appropriate packages, and configure Accelerate. Accelerate is tested on **Python 3.8+**.

Accelerate is available on pypi and conda, as well as on GitHub. Details to install from each are below:

[](#pip)pip
-----------

To install Accelerate from pypi, perform:

Copied

pip install accelerate

[](#conda)conda
---------------

Accelerate can also be installed with conda with:

Copied

conda install -c conda-forge accelerate

[](#source)Source
-----------------

New features are added every day that haven’t been released yet. To try them out yourself, install from the GitHub repository:

Copied

pip install git+https://github.com/huggingface/accelerate

If you’re working on contributing to the library or wish to play with the source code and see live results as you run the code, an editable version can be installed from a locally-cloned version of the repository:

Copied

git clone https://github.com/huggingface/accelerate
cd accelerate
pip install -e .

[](#configuration)Configuration
-------------------------------

After installing, you need to configure Accelerate for how the current system is setup for training. To do so run the following and answer the questions prompted to you:

Copied

accelerate config

To write a barebones configuration that doesn’t include options such as DeepSpeed configuration or running on TPUs, you can quickly run:

Copied

python -c "from accelerate.utils import write\_basic\_config; write\_basic\_config(mixed\_precision='fp16')"

Accelerate will automatically utilize the maximum number of GPUs available and set the mixed precision mode.

To check that your configuration looks fine, run:

Copied

accelerate env

An example output is shown below, which describes two GPUs on a single machine with no mixed precision being used:

Copied

\- \`Accelerate\` version: 1.2.0.dev0
- Platform: Linux-6.8.0-47-generic-x86\_64-with-glibc2.35
- \`accelerate\` bash location: /home/zach/miniconda3/envs/accelerate/bin/accelerate
- Python version: 3.10.13
- Numpy version: 1.26.4
- PyTorch version (GPU?): 2.5.1+cu124 (True)
- PyTorch XPU available: False
- PyTorch NPU available: False
- PyTorch MLU available: False
- PyTorch MUSA available: False
- System RAM: 187.91 GB
- GPU type: NVIDIA GeForce RTX 4090
- \`Accelerate\` default config:
        - compute\_environment: LOCAL\_MACHINE
        - distributed\_type: MULTI\_GPU
        - mixed\_precision: no
        - use\_cpu: False
        - debug: False
        - num\_processes: 2
        - machine\_rank: 0
        - num\_machines: 1
        - gpu\_ids: all
        - rdzv\_backend: static
        - same\_network: True
        - main\_training\_function: main
        - enable\_cpu\_affinity: False
        - downcast\_bf16: no
        - tpu\_use\_cluster: False
        - tpu\_use\_sudo: False
        - tpu\_env: \[\]

[< \> Update on GitHub](https://github.com/huggingface/accelerate/blob/main/docs/source/basic_tutorials/install.md)

[←🤗 Accelerate](/docs/accelerate/index) [Quicktour→](/docs/accelerate/quicktour)