# Grape-Yield-Estimation

The goal of this project is to develop a novel, automated methodology for accurately estimating 
the number of fruits within grapevine rows using LIDAR and vision-based techniques. 
Traditional methods involve sampling a small portion of the vineyard, which leads to large 
margins of error. While experts can estimate quantities within 5% of actual yield, there is a need 
for a scalable, real-time solution that can be applied across large vineyards. 

The project will explore the use of handheld LIDAR (e.g., GEOSLAM) and structure-from-motion 
techniques to analyze data. The aim is to develop a heuristic model based on the shape and 
structure of the grape bunches, which can be trained to estimate fruit yield accurately. This 
method will be tested in both juice grape and wine grape vineyards, which have different 
structural characteristics.

Project plan video:
https://youtu.be/OqcnaxRwQts
<br>
<img src="https://img.youtube.com/vi/OqcnaxRwQts/maxresdefault.jpg" width = 500>

## Installation Guide

Here are the steps to install the necessary libraries for running the notebooks included in this repository.

### Environment Creation
To create and enter the new environment, simply execute the following commands in your shell:

```bash
conda env create -f environment.yml
conda activate grape
```

#### R-package installation

After creating and activating the new conda environment, you can install the required R package. Here are the commands:

```bash
R
install.packages(c("lidR", "sf", "tidyverse", "ggplot2", "terra"), repos="https://cloud.r-project.org/")
```

#### Python-package installation

If you need to install the Python dependencies separately, you can use pip:

```bash
pip install laspy opencv-python numpy matplotlib
```

### Cloud Compare Installation

![grape_gif](https://github.com/AlexanderGrunewald/Grape-Yield-Estimation/blob/main/src/dataExploration/media/animation3.gif)

Cloud Compare is a free open-source software that enables the visualization and processing of 3D point clouds and meshes. Many different plugins come built-in with the application that allow for complex processing, annotation, and classification of point clouds. The download instructions for the program can be found in the "Download" tab of the following website: https://www.danielgm.net/cc/

https://github.com/cloudcompare/cloudcompare

#### Cloud Compare Classifier

Cloud Compare also has a classifier plugin called, CANUPO, that utilizes proprietary ".prm" files. These files contain all parameters that define a specific classifier and can be imported and exported to share classifiers across devices and point cloud files. While this classification feature was not ulitmately used (though was tested) within our project, the ability to share these classifier definition files is important for collaborative work

#### Additional Add-Ons

Custom and external plugins can also be used within Cloud Compare to extend its functions. No custom plugins were used for our project, though if anyone would like to extend the scope of the project with custom/shared plugins, these are the locations that the application will look for those files in:

/Applications/CloudCompare.app/Contents/PlugIns/ccPlugins <br>
/Users/USER/Library/Application Support/CCCorp/CloudCompare/plugins <br>
/Library/Application Support/CCCorp/CloudCompare/plugins <br>
/Applications/CloudCompare.app/Contents/Resources/plugins

*Note: These are MacOS-based directories, though CloudCompare is also available for Windows or Linux

## Running the Demos

### LidR

LidR is an open-source R package for manipulating and visualizing airborne laser scanning (ALS) data with an emphasis on research & development for forestry and ecology applications. We chose this package since it worked naturally with LAS file type data and was used in a previous grape yield estimation study. The notebook contained in src/dataExploration/lidr.ipynb goes through the step-by-step process of how we isolated candidate grape clusters using RGB filtering.

This approach, however, has not been sucessfull and was soon abandoned due to lack of results. We encourage to use this guide as a stepping stone to other more complicated approaches. 

### laspy-cv2-demo.ipynb

1. Navigate to the directory containing laspy-cv2-demo.ipynb:

```bash
cd src/dataExploration/notebook
```

2. Launch Jupyter Notebook

```bash
jupyter notebook
```

3. Open laspy-cv2-demo.ipynb in your browser and run the cells sequentially.

The notebook guides you through:
- Constructing reference color models for grapes and wood.
- Reading, processing, and filtering image data using OpenCV.
- Computing Mahalanobis distances for LiDAR points based on the RGB values.
- Visualizing the distribution of these distances via histograms.
- Classifying LiDAR points and writing a new LAS file with the updated classification.

Note: The current classification approach uses an arbitrary Mahalanobis distance threshold. Since the distance distributions are unimodal and skewed right, there isn’t a definitive threshold that accurately separates grape points from non-grape points. This method serves as a starting point, and further calibration and validation are needed to improve accuracy for automated yield estimation.
