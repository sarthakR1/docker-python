# docker-python
Kaggle Notebooks allow users to run a Python Notebook in the cloud against our competitions and datasets without having to download data or set up their environment.

This repository includes our Dockerfiles for building the CPU-only and GPU image that runs Python Notebooks on Kaggle.

Our Python Docker images are stored on Google Container Registry at:

CPU-only: gcr.io/kaggle-images/python
GPU: gcr.io/kaggle-gpu-images/python
Note: The base image for the GPU image is our CPU-only image. The gpu.Dockerfile adds a few extra layers to install GPU related libraries and packages (cuda, libcudnn, pycuda etc.) and reinstall packages with specific GPU builds (torch, tensorflow and a few mores).

Getting started
To get started with this image, read our guide to using it yourself, or browse Kaggle Notebooks for ideas.

Requesting new packages
First, evaluate whether installing the package yourself in your own notebooks suits your needs. See guide.

If you the first step above doesn't work for your use case, open an issue or a pull request.

Opening a pull request
Update the Dockerfile
For changes specific to the GPU image, update the gpu.Dockerfile.
Otherwise, update the Dockerfile.
Follow the instructions below to build a new image.
Add tests for your new package. See this example.
Follow the instructions below to test the new image.
Open a PR on this repo and you are all set!
Building a new image
./build
Flags:

--gpu to build an image for GPU.
--use-cache for faster iterative builds.
Testing a new image
A suite of tests can be found under the /tests folder. You can run the test using this command:

./test
Flags:

--gpu to test the GPU image.
Running the image
For the CPU-only image:

# Run the image built locally:
docker run --rm -it kaggle/python-build /bin/bash
# Run the pre-built image from gcr.io
docker run --rm -it gcr.io/kaggle-images/python /bin/bash
For the GPU image:

# Run the image built locally:
docker run --runtime nvidia --rm -it kaggle/python-gpu-build /bin/bash
# Run the image pre-built image from gcr.io
docker run --runtime nvidia --rm -it gcr.io/kaggle-gpu-images/python /bin/bash
To ensure your container can access the GPU, follow the instructions posted here.

Tensorflow custom pre-built wheel
A Tensorflow custom pre-built wheel is used mainly for:

Faster build time: Building tensorflow from sources takes ~1h. Keeping this process outside the main build allows faster iterations when working on our Dockerfiles.
Building Tensorflow from sources:

Increase performance: When building from sources, we can leverage CPU specific optimizations
Is required: Tensorflow with GPU support must be built from sources
The Dockerfile and the instructions can be found in the tensorflow-whl folder/.
