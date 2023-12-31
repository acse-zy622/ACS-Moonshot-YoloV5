# Moonshot
The purpose of this project is to build a software tool capable of 
automatically detecting impact craters in planetary surface images 
and producing a crater-size frequency distribution for dating.

## Table of Contents

- [Introduction](#introduction)
- [Installation Guide](#installation_guide)
- [Usage](#usage)
- [User instructions](#user_instructions)

## Introduction

<a href="url"><img src="https://drive.google.com/uc?export=view&id=1dJjw6g_S8s5hMsiZ67Sp9f50NrgZvoTm" align="left" height="300" width="300" ></a>

Impact craters are the most common surface feature found on rocky planetary bodies. 

The density of craters can be utilized to determine the age of the surface, 
with a denser terrain indicating an older surface. 

When the absolute ages of a surface are independently known, 
such as in the case of certain lava flows and areas of the Moon, 
crater density can be used to determine the absolute age of the surface.

Recent work has shown that widely used object detection algorithms
from computer vision, such as the YOLO (You Only Look Once) object
detection algorithm ([Redmon et al., 2016](https://doi.org/10.1109/CVPR.2016.91);
[Jocher et al., 2021](https://doi.org/10.5281/zenodo.4418161)), can be effective for crater detection on Mars
([Benedix et al., 2020](https://doi.org/10.1029/2019EA001005); [Lagain et al., 2021](https://doi.org/10.1029/2020EA001598)) and the Moon ([Fairweather
et al., 2022](https://doi.org/10.1029/2021EA002177)).


## Installation_Guide 

### Prerequisites

This project uses conda as a package manager. You should have conda configured on your local machine before installing the project. 

`conda -V`

### Installation and configuration

1. Clone the repository:

`git clone https://github.com/ese-msc-2022/acds-moonshot-schrodinger.git`

2. Go to the git repository on your local computer:

`cd acds-moonshot-schrodinger`

3. Create the conda environment:

`conda env create -f environment.yml`

4. Activate the `moonshot` environment:

`conda activate moonshot`

5. Once you have finished using the tool, you can deactivate the environment:

`conda deactivate`

## Usage

The aim of this tool is to enable users to efficiently and automatically 
locate all craters in an image, and from this, create a frequency distribution of 
crater sizes for dating the planetary surface. The tool must therefore possess the 
capability to calculate the actual size and location of craters in real-world units 
if the image's location, size, and resolution are supplied.

### Locating the craters
Using one or more images of a planet's surface as well as data such as the radius of the planet as input, 
the image of the impact crater on the planet's surface and the physical location 
of the impact crater (latitude, longitude, and size of the crater at the center) can be located and exported.

### Visualization
For visualization, the following functions are implemented:
1. The initial image without any labels or annotations
2. The initia input image with bounding boxes for craters detected by the CDM
3. The original input image with bounding boxes for both the results of the CDM 
and for the ground truth bounding boxes, if available
4. A standalone graph of the cumulative frequency distribution of the detected 
craters' sizes, if the information required for size calculation is provided.
5. If ground truth data is present, performance metrics including the count of 
True Positive, False Negative, and False Positive detections.

## User_instructions
### Overview
To use the tool with the GUI, first input the ```test_path``` and ```output_path```. Than choose the ```Planet``` : Mars or Moon. Then we can visualize the analysis part:
1. Show the original images. In the ```original image``` option, splitted images (416 pixels) of different regions of the planet are displayed.
2. Show craters detected with Crater Detection Model (CDM). Click the ```CDM Detection``` button, you can display the CDM results on the original images, with the red box circled the monitored craters area.
3. Compare the results. To verify the accuracy of the CDM model, click the ```Results Comparison``` button and locate the position of the known craters with a yellow box on the image that has shown the monitoring results.
4. Show the size-frequency distribution. Click ```S-F Plot``` to show a graph of the cumulative frequency distribution of crater sizes for the detected craters.
5. Performance statistics. Click ```Statistics Analysis``` to show the performance statistics data including the number of True Positive, False Negative and False Positive detections.

### Mars model

- **Step1**: use crater tool **generate_test_files.py** to automatically 
    - get dataset from your input path
    - generate new $.yaml$ file for validate in test dataset


- **Step2**: run **detect.py** to get predictions 
    - for directly using the interface, please set the API **--exist_ok** set **True**
    - use crater tool "plot_two_boxes.py" to get images with


- **Step3**: run **val.py** with crater CDM API (**--val-test**)
    - for directly using the interface, please set the API **--exist_ok** set **True**
    - get the statistics analysis results over the whole test dataset
    - name: val-test-statistics-results.csv
    
- **Step4**: use crater tool **get_bbox_csv.py** to get get detections csv files
    
- **Step5**: run crater tool **generate_output_results.py** to automatically get results in output path

### Moon model

- **Step1**: use crater tool **Preproc.py** to automatically 
    - split the moon dataset images
    - from more details see the notebook in **Moon-preproc.ipynb**
    
    
- **Step2**: use crater tool **generate_test_files.py** to automatically 
    - get dataset from your input path
    - generate new $.yaml$ file for validate in test dataset


- **Step3**: run **detect.py** to get predictions 
    - for directly using the interface, please set the API **--exist_ok** set **True**


- **Step4**: run **val.py** with crater CDM API (**--val-test**)
    - for directly using the interface, please set the API **--exist_ok** set **True**
    - get the statistics analysis results over the whole test dataset
    - name: val-test-statistics-results.csv
    
    
- **Step5**: run crater tool **generate_output_results.py** to automatically get results in output path
    - for more details, see the notebook named **Visualisation.ipynb**

