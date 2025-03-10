[](#webdataset)WebDataset
=========================

[WebDataset](https://github.com/webdataset/webdataset) is a library for writing I/O pipelines for large datasets. Its sequential I/O and sharding features make it especially useful for streaming large-scale datasets to a DataLoader.

[](#the-webdataset-format)The WebDataset format
-----------------------------------------------

A WebDataset file is a TAR archive containing a series of data files. All successive data files with the same prefix are considered to be part of the same example (e.g., an image/audio file and its label or metadata):

![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/datasets-webdataset-format.png) ![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/datasets-webdataset-format-dark.png)

Labels and metadata can be in a `.json` file, in a `.txt` (for a caption, a description), or in a `.cls` (for a class index).

A large scale WebDataset is made of many files called shards, where each shard is a TAR archive. Each shard is often ~1GB but the full dataset can be multiple terabytes!

[](#streaming)Streaming
-----------------------

Streaming TAR archives is fast because it reads contiguous chunks of data. It can be orders of magnitude faster than reading separate data files one by one.

WebDataset streaming offers high-speed performance both when reading from disk and from cloud storage, which makes it an ideal format to feed to a DataLoader:

![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/datasets-webdataset-stream.png) ![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/datasets-webdataset-stream-dark.png)

For example here is how to stream the [timm/imagenet-12k-wds](https://huggingface.co/datasets/timm/imagenet-12k-wds) dataset directly from Hugging Face:

First you need to [Login with your Hugging Face account](/docs/huggingface_hub/quick-start#login), for example using:

Copied

huggingface-cli login

And then you can stream the dataset with WebDataset:

Copied

\>>> import webdataset as wds
\>>> from huggingface\_hub import get\_token
\>>> from torch.utils.data import DataLoader

\>>> hf\_token = get\_token()
\>>> url = "https://huggingface.co/datasets/timm/imagenet-12k-wds/resolve/main/imagenet12k-train-{{0000..1023}}.tar"
\>>> url = f"pipe:curl -s -L {url} -H 'Authorization:Bearer {hf\_token}'"
\>>> dataset = wds.WebDataset(url).decode()
\>>> dataloader = DataLoader(dataset, batch\_size=64, num\_workers=4)

[](#shuffle)Shuffle
-------------------

Generally, datasets in WebDataset formats are already shuffled and ready to feed to a DataLoader. But you can still reshuffle the data with WebDataset’s approximate shuffling.

In addition to shuffling the list of shards, WebDataset uses a buffer to shuffle a dataset without any cost to speed:

![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/datasets-webdataset-shuffle.png) ![](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/datasets-webdataset-shuffle-dark.png)

To shuffle a list of sharded files and randomly sample from the shuffle buffer:

Copied

\>>> buffer\_size = 1000
\>>> dataset = (
...     wds.WebDataset(url, shardshuffle=True)
...     .shuffle(buffer\_size)
...     .decode()
... )

[< \> Update on GitHub](https://github.com/huggingface/hub-docs/blob/main/docs/hub/datasets-webdataset.md)

[←Spark](/docs/hub/en/datasets-spark) [Dataset Viewer→](/docs/hub/en/datasets-viewer)