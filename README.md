# First Order Motion Model for Image Animation

This repository contains an implementation of image animation using a First Order Motion Model.

## Example animations

The videos on the left show the driving videos. The first row on the right for each dataset shows the source videos. The bottom row contains the animated sequences with motion transferred from the driving video and object taken from the source image.This is how the working in the project is done.

### VoxCeleb Dataset
![Screenshot](sup-mat/vox-teaser.gif)
### Fashion Dataset
![Screenshot](sup-mat/fashion-teaser.gif)
### MGIF Dataset
![Screenshot](sup-mat/mgif-teaser.gif)

### Installation

We support ```python3```. To install the dependencies run:

### YAML configs

There are several configuration (```config/dataset_name.yaml```) files one for each `dataset`. See ```config/taichi-256.yaml``` to get description of each parameter.


### Animation Demo
To run a demo, download checkpoint and run the following command:
python demo.py --config config/dataset_name.yaml --driving_video path/to/driving --source_image path/to/source --checkpoint path/to/checkpoint --relative --adapt_scale

The result will be stored in ```result.mp4```.

### Animation demo with Docker

Requirements: Docker 19.03+ and [nvidia-docker](https://github.com/NVIDIA/nvidia-docker)
installed and able to successfully run the `nvidia-docker` usage tests.

Build the container:
docker build -t first-order-model 

Run the demo:
docker run -it --rm --gpus all
-v $HOME/first-order-model:/app first-order-model
python3 demo.py --config config/vox-256.yaml
--driving_video driving.mp4
--source_image source.png
--checkpoint vox-cpk.tar
--result_video result.mp4
--relative --adapt_scale


### Colab Demo 

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Anshulsm12/first-order-model/blob/master/demo.ipynb)

### Face-swap
It is possible to modify the method to perform face-swap using supervised segmentation masks.
![Screenshot](sup-mat/face-swap.gif)

### Training

To train a model on specific dataset run:

CUDA_VISIBLE_DEVICES=0,1,2,3 python run.py --config config/dataset_name.yaml --device_ids 0,1,2,3


### Evaluation on video reconstruction

To evaluate the reconstruction performance run:

CUDA_VISIBLE_DEVICES=0 python run.py --config config/dataset_name.yaml --mode reconstruction --checkpoint path/to/checkpoint


### Image animation

To animate videos run:

CUDA_VISIBLE_DEVICES=0 python run.py --config config/dataset_name.yaml --mode animate --checkpoint path/to/checkpoint


### Datasets

1) **Bair**: [Download](https://yadi.sk/d/Rr-fjn-PdmmqeA)
2) **Mgif**: [Download](https://yadi.sk/d/5VdqLARizmnj3Q)
3) **Fashion**: Available at [UBC Vision](https://vision.cs.ubc.ca/datasets/fashion/)
4) **Taichi**: Follow instructions in [data/taichi-loading](data/taichi-loading/README.md)
5) **Nemo**: Follow instructions at [UVA-NEMO](https://www.uva-nemo.org/)
6) **VoxCeleb**: Follow video preprocessing instructions in repository

### Training on your own dataset
1) Resize videos to 256x256
2) Create ```data/dataset_name``` with ```train``` and ```test``` subfolders
3) Create config ```config/dataset_name.yaml```

Last Updated: 2025-04-09 16:23:30 UTC
Maintained by: Anshulsm12, anishqt, Dhruvsr

