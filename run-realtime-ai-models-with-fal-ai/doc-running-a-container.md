Documentation

Examples

Running a container as a function

Container Support with fal[](#container-support-with-fal)
---------------------------------------------------------

fal now supports running functions within custom Docker containers, providing greater flexibility and control over your environment.

### Example: Using Custom Containers with fal functions[](#example-using-custom-containers-with-fal-functions)

Here's a complete example demonstrating how to use custom containers with `fal`.

    import fal

    from fal.container import ContainerImage

    dockerfile_str = """
    FROM python:3.11

    RUN apt-get update && apt-get install -y ffmpeg
    RUN pip install pyjokes ffmpeg-python
    """

    @fal.function(
        kind="container",
        image=ContainerImage.from_dockerfile_str(dockerfile_str),
    )
    def test_container():
        # A dependency that might have complex installation requirements.
        import ffmpeg
        (
            ffmpeg.input("input.mp4")
            .filter('thumbnail', n=300)
            .output("thumbnail_filter_2.png")
            .run()
        )
        # And tell me a joke!
        import pyjokes
        print(pyjokes.get_joke())

        print("done")

    if __name__ == "__main__":
        test_container()

#### Detailed Explanation[](#detailed-explanation)

1.  **Importing fal and ContainerImage**:

    import fal
    from fal.container import ContainerImage

2.  **Creating a Dockerfile String**: A multi-line string (`dockerfile_str`) is defined, specifying the base image as `python:3.11`, and installing `ffmpeg` and `pyjokes` packages.

    dockerfile_str = """
    FROM python:3.11

    RUN apt-get update && apt-get install -y ffmpeg
    RUN pip install pyjokes ffmpeg-python
    """

##### Version mismatch

Ensure that the Python version in the Dockerfile matches the Python version in your local environment that you use to run the function.

This is required to avoid any compatibility issues. We use `pickle` to serialize the function under the hood, and the Python versions must match to avoid any serialization issues.

That being said, we are constantly working on improving this experience.

Alternatively, you can use a Dockerfile path to specify the Dockerfile location:

    import pathlib
    PWD = Path(__file__).resolve().parent
    @fal.function(
        kind="container",
        image=ContainerImage.from_dockerfile(f"{PWD}/Dockerfile"),
    )
    def test_container():
        ...

3.  **Defining the Container Function**: The `@fal.function` decorator specifies that this function runs in a container. The `image` parameter is set using `ContainerImage.from_dockerfile_str(dockerfile_str)`, which builds the Docker image from the provided Dockerfile string.

        @fal.function(
            kind="container",
            image=ContainerImage.from_dockerfile_str(dockerfile_str),
        )

4.  **Function Implementation**: Inside `test_container`, the `ffmpeg` library processes a video to create a thumbnail image. Then, it uses `pyjokes` to print a random joke.

        def test_container():
            import ffmpeg
            (
                ffmpeg.input("input.mp4")
                .filter('thumbnail', n=300)
                .output("thumbnail_filter_2.png")
                .run()
            )
            import pyjokes
            print(pyjokes.get_joke())

            print("done")


#### Running the Function[](#running-the-function)

To run the function, save the code to a file (e.g., `test_container.py`) and execute it using the `fal run` command:

    fal run test_container.py

or directly from the Python interpreter:

    python test_container.py

This example demonstrates how to leverage Docker containers in fal, enabling customized execution environments for your functions. For more details and advanced usage, refer to the [fal Container Documentation](/docs/private-serverless-models/running-containerized-application).

Last updated on October 4, 2024

[Llama 2 with vLLM](/docs/examples/running-llama-2-with-vllm "Llama 2 with vLLM")[Supported machines](/docs/supported-machines "Supported machines")
