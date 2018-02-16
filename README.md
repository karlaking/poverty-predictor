# poverty-predictor

## Overview 
Machine learning, data science, and satellite imagery used to map areas displaying indicators of poverty. The purpose of this excercise is to apply a remote sensing research case in order to gain experience in this particular python development environment. This project applies techniques established in a 2016 study from [Stanford University](http://sustain.stanford.edu/predicting-poverty/).

### Description of methods 
  The foundational study uses World Bank Data and computer vision to complete the poverty prediction research. View the original code [here](https://github.com/nealjean/predicting-poverty). My course of analysis does not include some of these techniques, and relies on a two step method of classification and comparison. Here is an overview of the steps involved:
    
  **I. Classification**
  * Daytime image - Label pixels *1-urban* or *0-non-urban*
    * Segment the image using the ```scikit-learn quickshift``` and ```felzenszwalb modules```
    * Train the  ```scikit-learn RandomForestClassifier ``` model using training data to classify segments
    * Bin the data into urban and non-urban classes 
  * Nighttime image - Label pixels *1-light* and *0-dark*
    *  Train the  ```scikit-learn RandomForestClassifier ``` model using training data to classify pixels
    * Bin the data into light and dark classes 

  **II. Comparison**
  * Subtract the Daytime image from the Nighttime image 

Outcome      | Score        | Meaning  
------------ | ------------ | ------------
1-urban - 1-light | 0 | expected
0-non-urban - 0-dark | 0 | expected
1-urban - 0-dark | 1 | poverty is predicted
0-non-urban - 1-light | -1 | false positve (ex. fire)
        

  The quality of the classification is not the primary focus of this excercise, though an accuracy assessment of both classified images is included. I am limited to producing the training datasets and wanted to prioritize building a pipeline, including accuracy assessments, for the process using this tech stack. Parameters of training the model were optimized, however the training-data is a limiting factor.

## Data Sets 
   * [Night-lights VIIRS Imagery](https://ngdc.noaa.gov/eog/viirs/download_ut_mos.html)
   * [Day-time Landsat Imagery](https://www.descarteslabs.com/)
 

## Dependencies 
  * Jupyter Notebook
  * Python 3
  * NumPy
  * gdal 2.0
  * scikit-learn
  * scikit-image

## Project Status
  As of 2/15/18 - A first iteration of both night lights and landcover classifications is complete. I've used a segmentation method for the land cover (urban) classification, and a supervised pixel-wise method for the night lights classification. Next step is performing accuracy assessments for both classifications. 

## REFERENCES 
* [Python for geospatial data processing by Carlos De La Torre](https://www.machinalis.com/blog/python-for-geospatial-data-processing/)
* [Python for Object Based Image Analysis (OBIA) by Carlos De La Torre](https://www.machinalis.com/blog/obia/) 
* [_COMBINING SATELLITE IMAGERY AND MACHINE LEARNING TO PREDICT POVERTY_, Neal Jean, Marshall Burke, Michael Xie, W. Matthew Davis, David B. Lobell, Stefano Ermon (Stanford University, August 2016)](http://sustain.stanford.edu/predicting-poverty/)
*  [Open-geo Tutorial by Chris Holden](https://github.com/ceholden/open-geo-tutorial)
