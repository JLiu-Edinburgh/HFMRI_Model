# CoilfreeMRI_ACCV2022
This is the code for paper "*Coil-Agnostic Attention-Based Network for Parallel MRI Reconstruction*" accepted at **ACCV2022**.

# Environment 
1. create Anaconda environment via conda create -n myenv

2. install torch, e.g. with cuda=10.2: conda install pytorch==1.7.1 torchvision==0.8.2 torchaudio==0.7.2 cudatoolkit=10.2 -c pytorch

3. install other dependencies, e.g. pip package:

* h5py
* matplotlib
* pathlib

# Dataset
Multi-coil knee MRI samples from the *FastMRI Dataset* [1] are used in our experiments. Data are saved in h5 files with keywords `csm` and `multi_coil`, representing the sensitivity maps and multi-coil images. The structure of one instance is shown as follows:

* file['section0']['csm'][()] of shape (15, 2, 256, 256),
* file['section0']['multi_coil'][()] of shape (15, 2, 256, 256),

where 15 is the number of coils, 2 channels are used to handle complex-valued data, and (256, 256) refers to the spatial size. The dataset and dataloader can be conveniently customized by tracking the specified data size in codes.

# Train the model 
run the code to train the model:

python multicoil_knee_baseline.py --mask ./mask/brain_mask_0_125.pt --dataroot path/to/training/dataset --testroot path/to/test/samples --dataset_name multi_coil_DACB --n_epochs 35 --epoch 0

Checkpoints will be saved in `./saved_models/multi_coil_DACB` and samples in `./images/multi_coil_DACB`.

# List of Papers

1. Zbontar, J.\*, Knoll, F.\*, Sriram, A.\*, Murrell, T., Huang, Z., Muckley, M. J., ... & Lui, Y. W. (2018). [fastMRI: An Open Dataset and Benchmarks for Accelerated MRI](https://arxiv.org/abs/1811.08839). *arXiv preprint arXiv:1811.08839*.
