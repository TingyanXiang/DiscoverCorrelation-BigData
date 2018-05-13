# DS 1004 Final Project DiscoverCorrelation-BigData

In this project, our goal is to discover potential correlations among datasets with different temporal and spatial resolutions. We first preprocess large quantity of data with spark and then we aggregate well-structured outputs based on diverse aggregation functions. For the final step, we compute pairwise mutulal information and pearson correlation to measure relationships among different attributes. 

# Dataset

Our data is collected from NYC open data with total size of over 100 GB. There are eight data sets: 

- Yellow cab taxi data from 2011 to 2017: 
http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml
- Vehicle collision data from 2011 to 2018:
https://data.cityofnewyork.us/Public-Safety/NYPD-Motor-Vehicle-Collisions/h9gi-nx95
- 311 call service records from 2011 to 2017:
https://nycopendata.socrata.com/Social-Services/311-Service-Requests-from-2010-to-Present/erm2-nwe9
- Citibike trip history data from 2010 to 2017:
https://www.citibikenyc.com/system-data
- Crime data from 2006 to 2016:
https://data.cityofnewyork.us/Public-Safety/NYPD-Complaint-Data-Historic/qgea-i56i
- Weather data from 2011 to 2017: 
https://nyu.box.com/s/6epatrjp0bi8xvd17blzmoy301ikie9z
- Property data from 2012 to 2017: 
https://nyu.box.com/s/hx7v2mpsw7rkdps6b613tvoiq9a1r448
- Census data from 2013 to 2016: 
https://factfinder.census.gov/faces/nav/jsf/pages/guided_search.xhtml

All data sets have spatial and temporal attributes respectively with different resolutions. 

# Code
The code of this project is categorized into 4 parts, CodeSpark, MapReduce, SpatialResolution and Results.

### CodeSpark

Contains main python files that include mappers.py, preprocess.py and correlation calculating files. 
- mappers.py contains all mapper functions that are used to preprocess 8 different data sets. 
- preprocess.py removes header of each dataset and run mapper functions from mapper.py to generate dataframe outputs with keys and values in the same format.
- corr_.py files take two dataframes (Spark, not Pandas), aggregate attributes with Spark SQL, inner join two datasets with the same keys and calculate correlations afterwards. We only include a few samples here, and you need to do slight modification for other pairs of dataframes.

### SpatialResolution

Contains a python file that builds the grid search and data that includes spatial information.
- gridSearch.py builds the grid search dictionary and the search function used in mappers.
- polys_*.pickle is a list of polygons of corresponding districts.
- polys_*_dict.pickle is dictionary with key=index_of_polygons and value=corresponding_district
- bound_*.pickle is the border information of NYC. 

If you want to use the search function (find_dist), you need to generate a dictionary with key=index_of_grid and value=polygons with gridSearch.py (this dictionary is too big to put on GitHub).  

### Results 

Contains a small part of outputs form corr_.py files for different datasets. Both joined datasets and final results of mutual information and Pearson correlation are included.

### MapReduce
Contains a few map and reduce functions that are written for primary MapReduce implementation at first. Later we choose to use Spark and these functions are abandoned.

### How to run
If you want to run this system on your own, you need run the preprocess.py first to get well-structured tables, and then run corr.py files to get correlation results.

# Architecture

This project follows the process shown below:

<img src="https://user-images.githubusercontent.com/31422339/39963010-e94316c2-562d-11e8-8a86-1417be6fc401.png" width="900" height="500">
