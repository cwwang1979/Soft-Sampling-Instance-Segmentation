# Soft-Sampling Cascade Instance segmentation

<img width="1299" src="CMRCNN_architecture.png">

## Associated paper
Wang et al. (In press) Automated quantification of HER2 amplification levels using deep learning, IEEE Journal of Biomedical and Health Informatics (JCR 2023: IF= 6.7, Q1 3/44 MEDICAL INFORMATICS) 
If you use any materials here, please cite our publication.  

## Cloud Demo
AI inference process and results are shown in the dmeo [video](https://drive.google.com/file/d/1BnJMrl5gJLrLxgFycA2eJXmcHHZ_dKyG/view?usp=sharing).

#### Device specifications
- **CPU:** Intel Xeon Gold 6148
- **RAM:** 512 GB
- **GPU:** NVIDIA TITAN RTX 24 GB * 4

#### Time consumption
- **Data extraction time:** 328 seconds
- **AI Inference time:** 336 seconds

In the cloud demo, the system gets a WSI file from the remote NAS, and hence the data extraction time takes more than the workstation demo.


## Workstation Demo
AI inference process and results as follows with demo data 1M14.mrxs.
##### ![result](result_screenshot.png)

#### Device specifications
- **CPU:** Intel Core i9-7900X
- **RAM:** 128 GB
- **GPU:** NVIDIA GeForce GTX 1080 Ti 11 GB * 2

#### Time consumption
- **Data extraction time:** 6 seconds
- **AI Inference time:** 94 seconds

In the workstation demo, the WSI file is stored locally, and hence the data extraction time takes less than the cloud demo. -->

## Available hardware
- **CPU:** Intel® Core™ i7-8700K 
- **RAM:** 32 GB
- **GPU:** NVIDIA GeForce GTX 1080 Ti 11 GB 


## Environment Setup
We  provide a sample setting up script as following:

#### Requirerements
- ubuntu 18.04
- RAM >= 16 GB
- GPU Memory >= 6 GB
- GPU driver version >= 410.48

#### Step-by-step Installation
```
conda create -n SCinstanceseg python=3.7 -y
source activate SCinstanceseg
pip install torch==1.7.1+cu101 torchvision==0.8.2+cu101 -f https://download.pytorch.org/whl/torch_stable.html
pip install -U openmim
mim install mmcv-full==1.4.8
pip install timm
pip install terminaltables
pip install pycocotools
pip install einops

# FCOS and coco api and visualization dependencies
pip install ninja yacs cython matplotlib tqdm
pip install opencv-python==4.4.0.40
# Boundary dependency
pip install scikit-image
 
export INSTALL_DIR=$PWD
 
# install pycocotools. Please make sure you have installed cython.
cd $INSTALL_DIR
git clone https://github.com/cocodataset/cocoapi.git
cd cocoapi/PythonAPI
python setup.py build_ext install

cd SS-cascade_instance_segmentation  # set up instance segmentation
pip install -v -e . 

```

#### Download
All Training Data of FISH and DISH sets with 5 Sample Testing Images, the Execution file, configuration file, and models can be download from the [zip](https://drive.google.com/file/d/1Fc_QiMBoT5AYqoNXZKgNRWilRBP39_5l/view?usp=share_link) file.  (For reviewers, please use the manuscript number C....... as the password to decompress the file.)

#### File structure
```
SS-cascade_instance_segmentation/

├── data/-DATA_NAME-/ - training and testing data location
│   ├── annotations/
│   │   ├── instances_train.json
│   │   ├── instances_val.json
│   ├── train/
│   │   ├── 125121A_S20200928_0001.jpg
│   │   ├── 125121A_S20200928_0002.jpg
│   │   ├── 125121A_S20200928_0003.jpg
│   │   │       ⋮
│   │   └── 2004994A_S20201013_0002.jpg
│   ├── val/
│   │   ├── 2004994A_S20201013_0003.jpg
│   │   ├── 2004994A_S20201013_0004.jpg
│   │   ├── 2004994A_S20201013_0005.jpg
│   │   │       ⋮
│   │   └── 2004994A_S20201013_0018.jpg
│   ├── test/
│   │   ├── 2006683A_S20201014_0021.jpg
│   │   ├── 2008522H_S20201013_0014.jpg
│   │   ├── 2016340A_S20201012_0026.jpg
│   │   │       ⋮
│   │   └── 2016340A_S20201012_0031.jpg
│   │
├── work_dirs/cascade_maskrcnn_x50_softsampling/-DATA_NAME-/ - contains instance segmentation models
│   │   ├── cascade_maskrcnn_x50_softsampling.py -config file
│   │   └── latest.pth - model
│   │
└── output/-DATA_NAME-/ - inference result is saved here

```

#### Trainining

In a terminal run:
```
cd SS-cascade_instance_segmentation  
python tools/train.py
```

#### Testing
<!-- Change "DATA_NAME" with a different data set in :83
Change config file in :18
Change model in :19 -->

In a terminal run:
```
cd SS-cascade_instance_segmentation  
python demo/image_demo.py
```


<!-- ## License
This extension to the Caffe library is released under a creative commons license, which allows for personal and research use only. For a commercial license please contact Prof Ching-Wei Wang. You can view a license summary here:  
http://creativecommons.org/licenses/by-nc/4.0/ -->


## Contact
Prof. Ching-Wei Wang  
  
cweiwang@mail.ntust.edu.tw; cwwang1979@gmail.com  
  
National Taiwan University of Science and Technology
