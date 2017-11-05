# poverty-predictor

## Overview 
* Machine learning, data science, and satellite imagery used to map areas displaying indicators of poverty. The purpose of this excercise is to apply newly researched remote sensing techniques to analyze a new area and to gain experience in this particular python development environment. 
    * This project applies techniques established in a 2016 study from [Stanford University](http://sustain.stanford.edu/predicting-poverty/)

### Description of methods 
  * View the original code [here](https://github.com/nealjean/predicting-poverty)
  The foundational study uses World Bank Data and computer vision to complete the poverty prediction research. My course of analysis does not include some of these techniques, rather relies on a two step method of classification and comparison. Here is an overview of the steps involved:
    
  I. Classification 
      1. Daytime image - Label pixels *1-urban* or *0-non-urban*
         * Segment the image using the ```scikit-learn quickshift``` and ```felzenszwalb modules```
         * Train the  ```scikit-learn RandomForestClassifier ``` model using training data to classify segments
         * Bin the data into urban and non-urban classes 
      2. Nighttime image - Label pixels *1-light* and *0-dark*
        *  Train the  ```scikit-learn RandomForestClassifier ``` model using training data to classify pixels
         * Bin the data into light and dark classes 

  II. Comparison 
      1. Subtract the Daytime image from the Nighttime image 
        * A score of 0 is expected:
        ``` (1-urban - 1-light = 0) (0-non-urban - 1- dark = 0) ```
        * A score of 1 indicates an early where poverty is predicted:
        ``` (1-urban - 0-dark = 1) ```
        * A score of -1 may be a false positive, such as a fire: 
        ``` (0-non-urban - 1-light = -1)```

    *The quality of the classification is not the primary focus of this excercise, though an accuracy assessment of both classified images is included. I am limited to producing the training datasets and wanted to prioritize building a pipeline, including accuracy assessments, for the process using this tech stack. Parameters of training the model were optimized, however the training-data is a limiting factor.*

## Data Sets 
   * [Night-lights VIIRS Imagery](https://ngdc.noaa.gov/eog/viirs/download_ut_mos.html)
   * [Day-time Landsat Imagery](https://www.descarteslabs.com/)
 

## Dependencies 
  * Jupyter Notebook
  * Python 3
  * Numpy
  * gdal 2.0
  * scikit-learn
  * scikit-image


## REFERENCES 
* [Python for geospatial data processing by Carlos De La Torre](https://www.machinalis.com/blog/python-for-geospatial-data-processing/)
* [Python for Object Based Image Analysis (OBIA) by Carlos De La Torre](https://www.machinalis.com/blog/obia/) 
* [_COMBINING SATELLITE IMAGERY AND MACHINE LEARNING TO PREDICT POVERTY_, Neal Jean, Marshall Burke, Michael Xie, W. Matthew Davis, David B. Lobell, Stefano Ermon (Stanford University, August 2016)](http://sustain.stanford.edu/predicting-poverty/)
*  [Open-geo Tutorial by Chris Holden](https://github.com/ceholden/open-geo-tutorial)
