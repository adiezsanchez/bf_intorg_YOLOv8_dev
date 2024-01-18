<h1>Training a YOLOv8 model for detection of intestinal organoids in brightfield images</h1>

[![License](https://img.shields.io/pypi/l/napari-accelerated-pixel-and-object-classification.svg?color=green)](https://github.com/adiezsanchez/intestinal_organoid_brightfield_analysis/blob/main/LICENSE)
[![Development Status](https://img.shields.io/pypi/status/scikit-image.svg)](https://en.wikipedia.org/wiki/Software_release_life_cycle#Alpha)

![workflow](./images/workflow.png)

The goal of this repository is to obtain a custom YOLOv8 model to segment and classify intestinal organoids and spheroids from brightfield images acquired using a widefield microscope. The obtained model will be used in [intestinal_organoid_brightfield_analysis](https://github.com/adiezsanchez/intestinal_organoid_brightfield_analysis) repository.

As a starting point the ground truth annotations for each raw image (.czi) are in a .tiff file format, where each "channel" contains a binary mask defining instances of each class.

In our particular dataset we have 3 classes of intestinal organoids: dead (or overgrown organoids), differentiated (developed organoids) or undifferentiated (aka spheroids). The resulting model will detect, segment and classify each of those instances.

<p align="center">
  <img src="./images/classes.png" alt="classes" width="70%">
</p>

In order to train the YOLOv8 the initial binary masks defining each class instances must be converted to COCO polygon .json files and later on into YOLO-style polygon .txt files. Executing the notebooks and .py files in a sequential order (1 to 5) allows to do so.

<h2>Instructions</h2>

1. In order to run these Jupyter notebooks and .py scripts you will need to familiarize yourself with the use of Python virtual environments using Mamba. See instructions [here](https://biapol.github.io/blog/mara_lampert/getting_started_with_mambaforge_and_python/readme.html).

2. Then you will need to create a virtual environment using the following command:

   <code>mamba create -n YOLOv8-napari devbio-napari python=3.9 pyqt -c conda-forge</code>
