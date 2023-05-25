# Soft-Sampling Cascade Instance segmentation

<img width="1299" src="CMRCNN_architecture.png">

## Associated paper
Wang C.*, Huang S., Lee Y., Shen Y., Meng S., Gaol J.(2022) Deep Learning for Bone Marrow Cell Detection and Classification on Whole-Slide Images, Medical Image Analysis, vol 75, 102270, 1-15 (SCI IF=13.828, 2/113 COMP. SCI., INTER. APP.). 
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

In the workstation demo, the WSI file is stored locally, and hence the data extraction time takes less than the cloud demo.


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
Execution file, configuration file, and models are download from the [zip]([https://drive.google.com/file/d/1_2pU3tUDzkk_vraTsqM8aVfMjO0VjhJl/view?usp=sharing](https://drive.google.com/file/d/1Fc_QiMBoT5AYqoNXZKgNRWilRBP39_5l/view?usp=share_link)) file.  (For reviewers, please use the manuscript number M...........R1 as the password to decompress the file.)

#### File structure
```
BoneMarrow/
│
├── BoneMarrow - execution file
├── setting.json - configuration file
│
├── TestImgTemp/ - temp data extraction folder
|
├── Data/ - inference data location
│   ├── 1M05.mrxs
│   ├── 1M05/
│   │   ├── Index.dat
│   │   ├── Slidedat.ini
│   │   ├── Data0000.dat
│   │   ├── Data0001.dat
│   │   ├── Data0002.dat
│   │   ├── Data0003.dat
│   │   ├── Data0004.dat
│   │   │       ⋮
│   │   └── Data0030.dat
│   │
|   ├── 1M14.mrxs
|   └── 1M14/
│       ├── Index.dat
│       ├── Slidedat.ini
│       ├── Data0000.dat
│       ├── Data0001.dat
│       ├── Data0002.dat
│       ├── Data0003.dat
│       ├── Data0004.dat
│       │       ⋮
│       └── Data0035.dat
│
├── Model/ - contains detection models
|   ├── BMntu10mix_9_i90w
|   └── NTU_ROI_i10w
|
└── Result/ - inference result is saved here

```

#### Inference
Open the setting.json file to set up the input WSI filename and the GPUs to use.    
The file format is as follows:  
```
{
    "DATA": "1M14.mrxs",    //the input WSI filename.
    "GPU": [0, 1]           //the ID(s) of GPU(s) to use for testing.
}
```

Then in a terminal run:  
```
./BoneMarrow
```


## License
This extension to the Caffe library is released under a creative commons license, which allows for personal and research use only. For a commercial license please contact Prof Ching-Wei Wang. You can view a license summary here:  
http://creativecommons.org/licenses/by-nc/4.0/


## Contact
Prof. Ching-Wei Wang  
  
cweiwang@mail.ntust.edu.tw; cwwang1979@gmail.com  
  
National Taiwan University of Science and Technology
