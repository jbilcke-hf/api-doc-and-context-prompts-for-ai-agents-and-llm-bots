Documentation

Guidelines

Writing efficient Dockerfiles for faster builds

Cache-Efficient Dockerfile Guidelines with docker buildx (or buildKit)[](#cache-efficient-dockerfile-guidelines-with-docker-buildx-or-buildkit)
-----------------------------------------------------------------------------------------------------------------------------------------------

Under the hood, we use [buildkit (opens in a new tab)](https://docs.docker.com/build/buildkit) (or [docker buildx (opens in a new tab)](https://docs.docker.com/reference/cli/docker/buildx)) to build docker images. This allows us to take advantage of advanced caching mechanisms to improve build times and reduce resource consumption. In this guide, we'll provide some guidelines for creating cache-efficient Dockerfiles.

### Introduction[](#introduction)

Building a cache-efficient Dockerfile is crucial for improving the build time and reducing resource consumption. Docker Buildx and BuildKit provide advanced features that enhance caching mechanisms. This document provides guidelines for creating such Dockerfiles.

Ensure you have Docker Buildx and BuildKit enabled in your Docker environment if you want to test your containers locally. Otherwise, you don't need to worry about it. fal platform takes care of it for you when you deploy your application using container support.

Check out the [Docker buildx documentation (opens in a new tab)](https://github.com/docker/buildx) for more information.

### General Guidelines[](#general-guidelines)

Please also refer to the [Dockerfile best practices (opens in a new tab)](https://docs.docker.com/build/building/best-practices) for detailed information on Dockerfile best practices.

#### 1\. Minimize Layers[](#1-minimize-layers)

Each `RUN`, `COPY`, or `ADD` instruction creates a new layer. Minimize the number of layers by combining commands.

**Bad Example:**

    RUN apt-get update
    RUN apt-get install -y curl

**Good Example:**

    RUN apt-get update && apt-get install -y curl

#### 2\. Leverage Layer Caching[](#2-leverage-layer-caching)

Order instructions from least to most frequently changing to maximize layer caching.

**Example:**

    # Install dependencies (changes less frequently)
    COPY requirements.txt /app/
    RUN pip install -r requirements.txt

    # Copy application code (changes more frequently)
    COPY . /app

#### 3\. Use `--mount=type=cache`[](#3-use---mounttypecache)

Utilize BuildKit's `--mount=type=cache` to cache directories across builds.

**Example:**

    # syntax=docker/dockerfile:1.3-labs
    FROM python:3.9

    # Use BuildKit cache for pip
    RUN --mount=type=cache,target=/root/.cache/pip \
        pip install --upgrade pip

    COPY requirements.txt /app/
    RUN --mount=type=cache,target=/root/.cache/pip \
        pip install -r requirements.txt

    COPY . /app

#### 4\. Multi-Stage Builds[](#4-multi-stage-builds)

Use multi-stage builds to reduce the final image size by copying only the necessary artifacts from intermediate stages.

**Example:**

    # syntax=docker/dockerfile:1.3
    FROM python:3.9 AS builder
    WORKDIR /app
    COPY . .
    RUN pip install --upgrade pip \
     && pip install -r requirements.txt

    FROM python:3.9-slim
    COPY --from=builder /app /app
    WORKDIR /app
    ENTRYPOINT ["python", "app.py"]

#### 5\. Clean Up After Installations[](#5-clean-up-after-installations)

Remove unnecessary files and caches after installing packages to keep the image size small.

**Example:**

    RUN apt-get update && apt-get install -y \
        build-essential \
     && rm -rf /var/lib/apt/lists/*

#### 6\. Use `.dockerignore`[](#6-use-dockerignore)

Specify files and directories to ignore during the build process to avoid unnecessary files in the build context.

As of now, fal does not support `.dockerignore` files. Since we don't allow using `COPY` and `ADD` from the host filesystem, you can ignore this step. However, we plan to add support for this in the near future. Stay tuned!

See [below](/docs/guidelines/dockerfile#1-interacting-with-the-local-filesystem) for more information.

**Example:**

    __pycache__
    *.pyc
    *.pyo

### Example Dockerfile[](#example-dockerfile)

Here is an example of a cache-efficient Dockerfile using the principles outlined above:

    # syntax=docker/dockerfile:1.3
    FROM python:3.9 AS base
    WORKDIR /app

    # Install dependencies
    COPY requirements.txt ./
    RUN --mount=type=cache,target=/root/.cache/pip \
        pip install --upgrade pip \
     && pip install -r requirements.txt

    # Copy source files
    COPY . .

    # Build the application
    RUN python setup.py build

    # Production image
    FROM python:3.9-slim
    COPY --from=base /app /app
    WORKDIR /app
    ENTRYPOINT ["python", "app.py"]

### fal Platform Specific Gotchas[](#fal-platform-specific-gotchas)

When deploying your application on the fal platform, you don't need to worry about enabling Docker Buildx or BuildKit. We take care of it for you. However, you can follow the guidelines mentioned above to create efficient Dockerfiles that will help speed up the build process and reduce resource consumption.

#### 1\. Interacting with the local filesystem[](#1-interacting-with-the-local-filesystem)

`COPY` and `ADD` (from local filesystem) are not supported as of now to copy files into the container from the host. Instead you can use fal's `fal.toolkit` to upload files and refer them in the container using links.

If you are curious about the differences between `COPY` and `ADD`, check out the [following link (opens in a new tab)](https://www.baeldung.com/ops/docker-copy-add).

    json_url = File.from_path("my-file.json", repository="cdn").url

    dockerfile_str = f"""
    FROM python:3.11-slim
    RUN apt-get update && apt-get install -y curl
    RUN curl '{json_url}' > my-file.json
    """

or you can use `ADD` to directly download the file from the URL:

    json_url = File.from_path("requirements.txt", repository="cdn").url

    dockerfile_str = f"""
    FROM python:3.11-slim
    ADD {json_url} /app/requirements.txt
    WORKDIR /app
    RUN pip install -r requirements.txt
    """

### Conclusion[](#conclusion)

By following these guidelines, you can create Dockerfiles that build efficiently and take full advantage of Docker Buildx and BuildKit's caching capabilities. This will lead to faster build times and reduced resource usage.

For more detailed information, refer to the [Docker documentation (opens in a new tab)](https://docs.docker.com/build).

Last updated on October 4, 2024

[Migrating from Replicate](/docs/migration-guidelines/replicate "Migrating from Replicate")[Advanced reference](/docs/advanced-reference "Advanced reference")
