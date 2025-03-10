WebDataset File Format Specification

Introduction
============

WebDataset is a versatile and open data format designed to efficiently handle large-scale datasets in deep learning applications. Built on the widely-used POSIX tar archive format and simple file naming conventions, WebDataset provides a robust and portable way to store and distribute data samples.

The tar format ensures compatibility across platforms and allows for easy creation, manipulation, and extraction of WebDataset files using standard tools. The file naming conventions enable the grouping of related files into individual data samples, identified by unique prefixes within the archive. This addresses the "small file problem" common in deep learning, optimizing I/O and storage utilization.

WebDataset is self-describing by relying on standard file-based formats and magic numbers, ensuring long-term readability and making it suitable for archival purposes. It supports standard compression algorithms and formats for multimedia data, enabling efficient storage and retrieval of various data types.

As a file-based format, WebDataset allows for flexible data access and manipulation, either by mounting it as a file system or extracting individual files. Its design enables distributed training across multiple devices or nodes, handling datasets that exceed single-machine memory capacity. Parallel processing capabilities speed up data loading and preprocessing pipelines, enhancing overall performance.

WebDataset integrates seamlessly with popular deep learning frameworks, making it a powerful tool for training large-scale models efficiently and scalably.

Available Libraries and Tools
=============================

The following libraries are available for reading/writing/manipulating WebDataset dataset:

-   tar command line programs (with ---sort options)

-   the WebDataset library (github: webdataset/webdataset)

-   the wids library (distributes as part of WebDataset, github: webdataset/webdataset)

-   the Ray data library of the Ray project (for large scale distributed processing)

-   the tarp command line tool (github: webdataset/tarp)

-   the Julia webdataset library

-   the AIStore high performance distributed object store

-   The Hugging Face datasets library

WebDataset Specification
========================

Shard Organization
------------------

-   Each WebDataset consists of one or more shards. 

-   Each shard is a POSIX tar archive and should have a .tar extension.

-   Shards should be numbered sequentially; six digits, zero-padded starting at 0 is recommended (but not required).

-   Example: dataset-train-000000.tar, dataset-train-000001.tar, ..., dataset-train-000973.tar

-   Shards can be referred to using brace notation with ranges; libraries generally expand such ranges

-   Example: dataset-train-{000000..000973}.tar

-   More complex collections or mixtures of shards can be specified programmatically or using YAML or JSON dataset specification files.

Organization of Samples within Shards
-------------------------------------

-   Each shard is a POSIX tar archive of files.

-   Adjacent files in the tar archive are grouped together into samples.

-   Files that have the same prefix and adjacent are grouped together into a sample.

-   The prefix of a file is all directory components of the file plus the file name component up to the first "." in the file name.

-   The last extension (i.e., the portion after the last ".") in a file name determines the file type.

-   Decoding is usually based on the file type, but this depends on the library used to read the shards.

-   Samples are usually returned as dictionaries by libraries.

Example:

images17/image194.left.jpg\
images17/image194.right.jpg\
images17/image194.json\
images17/image12.left.jpg\
images17/image12.json\
images17/image12.right.jpg\
images3/image1459.left.jpg\
...

When reading this with a WebDataset library, you would get the following two dictionaries back in sequence:

{ "__key__": "images17/image194", "left.jpg": b"...", "right.jpg": b"...", "json": b"..."}\
{ "__key__": "images17/image12", "left.jpg": b"...", "right.jpg": b"...", "json": b"..."}\
...

Note that the key inside the dictionary consists of all extensions, including the extension that indicates the file type. It is up to the training code to decide how to make use of these extensions. For example, in a simple image classification dataset, samples may sometimes consist of .jpg/.cls pairs, and sometimes of .png/.cls pairs. But in a stereo image dataset, samples may consist of .left.jpg, .right.jpg, and .depth.png images.

Recommended File Types
======================

The WebDataset format is neutral on what you store inside your datasets. As far as it is concerned, it is just collections of files that are grouped together into samples. However, there are some common formats that simplify data interchange, that are recognized by libraries, and are recommended:

-   .cls, .cls2, .index, .inx, and .id are commonly used for integers

-   .json and .mp (msgpack) are used for more complex annotations of images

-   .jpg and .jpeg is recommended for images

-   .pickle is recommended for general Python data structures (but is not portable)

-   .pth and .pyd PyTorch dumps, good for torch tensors

-   .npy and .npz are NumPy array dumps

However, nothing restricts you to these file types. If you use other file types, you simply have to decode them in your reader pipeline.

Datasets with Complicated Structures
====================================

Column Stores
-------------

You can use WebDataset for column stores the same way you would use Apache Parquet. That is, you can arrange for shards to be split both by shard number and columns. For example, for learning depth-from-stereo, you might have shards "dataset-left-000000.tar, dataset-right-000000.tar, and dataset-depth-000000.tar". As in Parquet, you have to make sure that contents of your shards are consistent and you have to associate your data in the reader. Generally, though, this is not recommended, since it requires careful bookkeeping and makes I/O less efficient. The recommended way is to preprocess your data so that all the files needed for training samples are found together in a single shard.

Column Stores with Small Columns
--------------------------------

A common special case of "column stores" is where you have a large image dataset, but you have either new class labels for all the images, dynamically changing class labels, or even just a few corrections to class labels. In this case, you can store these "small columns" in a DBM or sqlite3 file and associate them with training samples dynamically. The WebDataset library, for example, provides a .associate(db) method for this.

Random Access
-------------

WebDataset was designed as a streaming storage format; that is, it was designed as a format that can be processed with purely sequential reads and no local storage. However, libraries like the "wids" library (distributed with the "webdataset" library) provide efficient random access to large, sharded datasets.