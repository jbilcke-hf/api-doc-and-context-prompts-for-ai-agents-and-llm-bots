Documentation

Private Serverless Models on GPUs

Accessing Persistent Storage

### Accessing persistent storage[](#accessing-persistent-storage)

As mentioned earlier, each fal function runs in an isolated environment that gets voided right after their invocation (unless `keep_alive` is set). But for certain use cases, it may be important to persist certain results after the run is over. In such scenarios, you can use the `/data` volume, which is mounted on each machine and is shared across all your functions running at any point in time linked to your FAL account.

    import fal
    from pathlib import Path

    DATA_DIR = Path("/data/mnist")

    @fal.function(
        "virtualenv",
        requirements=["torch>=2.0.0", "torchvision"],
        machine_type="M",
    )
    def train_fashion_model():
        import torch
        from torchvision import datasets

        already_present = DATA_DIR.exists()
        if already_present:
            print("Test data is already downloaded, skipping download!")

        test_data = datasets.FashionMNIST(
            root=DATA_DIR,
            train=False,
            download=not already_present,
        )
        ...

    if __name__ == "__main__":
        train_fashion_model()

When you invoke this function for the first time, you will notice that Torch downloads the test dataset. However, subsequent invocations - even those not covered by the invocation's `keep_alive` - will skip the download and proceed directly to your logic.

##### Implementation note

For HF-related libraries, fal ensures all downloaded models are persisted to avoid re-downloads when running ML inference workloads. No need to customize the output path for `transformers` or `diffusers`.

Last updated on October 4, 2024

[Introduction](/docs/private-serverless-models "Introduction")[Return Files and Images from Functions](/docs/private-serverless-models/return-files-and-images "Return Files and Images from Functions")
