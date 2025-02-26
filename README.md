<h1>Training a YOLOv8 model for detection of intestinal organoids in brightfield images</h1>

[![License](https://img.shields.io/pypi/l/napari-accelerated-pixel-and-object-classification.svg?color=green)](https://github.com/adiezsanchez/intestinal_organoid_brightfield_analysis/blob/main/LICENSE)
[![Development Status](https://img.shields.io/pypi/status/scikit-image.svg)](https://en.wikipedia.org/wiki/Software_release_life_cycle#Alpha)

![workflow](./images/workflow.png)

The goal of this repository is to obtain a custom YOLOv8 model to segment and classify intestinal organoids and spheroids from brightfield images acquired using a widefield microscope. The obtained model will be used in the [Instance Segmentation of Intestinal organoids and Spheroids from BrightField images using YOLOv8 (ISIS-BF)](https://github.com/adiezsanchez/intestinal_organoid_yolov8) repository.

As a starting point the ground truth annotations for each raw image (.czi) are in a .tiff file format, where each "channel" contains a binary mask defining instances of each class. Training dataset can be downloaded following the instructions below.

In our particular dataset we have 3 classes of intestinal organoids: dead (or overgrown organoids), differentiated (developed organoids) or undifferentiated (aka spheroids). The resulting model will detect, segment and classify each of those instances.

<p align="center">
  <img src="./images/classes.png" alt="classes" width="70%">
</p>

In order to train the YOLOv8 the initial binary masks defining each class instances must be converted to COCO polygon .json files and later on into YOLO-style polygon .txt files. Executing the notebooks and .py files in a sequential order (1 to 5) allows to do so.

<h2>Instructions</h2>

1. In order to run these Jupyter notebooks you will need to familiarize yourself with the use of Python virtual environments using Mamba. See instructions [here](https://biapol.github.io/blog/mara_lampert/getting_started_with_mambaforge_and_python/readme.html).

2. Then you will need to create a virtual environment (venv) either using the following command or recreate the environment from the .yml file you can find in the envs folder:

   <code>mamba create -n int_organoids python=3.9 devbio-napari cellpose pytorch torchvision plotly pyqt ultralytics -c conda-forge -c pytorch</code>

3. To recreate the venv from the environment.yml file stored in the envs folder (recommended) navigate into the envs folder using <code>cd</code> in your console and then execute:

   <code>mamba env create -f environment.yml</code>

4. The resulting environment will allow you to run the model training in the CPU, if you want to leverage your CUDA GPU you will need to check CUDA and cuDNN version compatibility with your hardware. In my case I have CUDA 12.1 and cuDNN 8.0 hence I can use the following command to create a working venv that leverages the CUDA cores in my GPU for training the YOLOv8 model:

   <code>mamba create -n int_organoids_GPU python=3.9 devbio-napari pytorch=2.1.2=py3.9_cuda12.1_cudnn8_0 torchvision plotly pyqt ultralytics python-kaleido -c conda-forge -c pytorch -c nvidia</code>

5. If you happen to have the same CUDA and cuDNN version you can recreate the from the environment_GPU.yml file stored in the envs folder.

<h2>Training Data Download</h2>

1. [Contact Me](mailto:alberto.d.sanchez@ntnu.no) to obtain a fresh working S3 bucket pre-signed link.

2. Paste the link inside <code>0_data_download.ipynb</code> notebook after <code>presigned_url</code>.

3. Run the notebook to download and extract the data.
