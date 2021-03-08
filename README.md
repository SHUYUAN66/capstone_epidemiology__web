
# Using Epidemiology Model To Predict Case Numbers for COVID-19

## Table of contents
* [Website](#io)
* [General info](#general-info)
* [Technologies](#technologies)
* [Setup](#setup)
* [Directions](#directions)
* [Processing](#in_processing)
* [Contact Us](#contact_info)

## Website
https://shuyuan66.github.io/capstone_epidemiology__web/

## General info
- Use covid-19 datasets provided by JHU to fit epidemiology model to U.S. After figuring out the infection parameter, we can then predict infected number for future. 

## Introduction
The early state and late stage of a pandemic is very different. At early stage, the case number grows exponentially. Government agencies and institutions want to the ability to forecast the number of cases in order to allocated medical and other resources. Furthermore, knowing how protocols such as stay at home order can affect the case number is extremely useful to make predictions. However, in order to predict number of cases in the future, the growth factor is needed and can be generated from fitting previous data to an epidemiology model. The exponential factor is based on two factors that can be learned from data: the infection rate, $\beta$ and number of days a patient stays infectious $D$.


## Technology
Project is created with:
- Image : https://hub.docker.com/repository/docker/caw062/test	

## Setup
- Before running, use `pip install -r requirements.txt` to install all the required packages
- on terminal, run `python run.py data` to retrieve the most current data from JHU & Apple Data

## Directions
`python run.py test` to start

## Processing
We are using gradient descent to find infection rate and infection duration. Then we want to check whether the parameters can predict useful information (accuracy). 

However, in reality, the case numbers of the entire country/state is not evenly distributed among counties. Besides computing the individual infection rate for all the counties, each as a separate entity from its neighbors, we will predict case numbers based on the mobility data provided by Descartes Labs[3] (how fast is people moving inside each county and across county boundaries), and the case numbers of each county's neighboring counties. We will use a $dt$ around 0.001 day instead of 1 day to better predict the dynamics. This process requires a fixed $\beta$ and $D$ predetermined for each county. 

Furthermore, $\beta$ and $D$ are also dynamic. So in the future, we will replace the fixed $\beta$ and $D$ with dynamic, changing according to the data.

The mobility data is representing the distance a typical member of a given population moves in a day. With this data set, we are able to see how stay-at-home orders by different states and the pandemic itself have effect on average mobility trends. The data set also provides additional information for our epidemiology model. 

### Achievements

We obtained the following results:At US country level (Figure 1), the model is underestimating the number of cases.  At state and countylevel (Figure 2 and Figure 3), the model is overestimating the number of cases.

<img src="https://user-images.githubusercontent.com/49173407/110281161-25b2a580-8017-11eb-8889-8ef0419fdd4f.png" width="20%"></img> <img src="https://user-images.githubusercontent.com/49173407/110281170-29462c80-8017-11eb-9681-aded85eb2dec.png" width="20%"></img> 
<img src="https://user-images.githubusercontent.com/49173407/110281176-2a775980-8017-11eb-9499-efe9f37600cd.png" width="20%"></img>  

### Use Geographical Information And Mobility Data to Predict County Infection

One of the pressing problems in epidemiology is long term prediction of the spreading of an infectious disease. Of particular interest is how mitigation measures (government policies) can affect the number of infected in the future. Numerous efforts have been tried around the world. Many cities and states in the U.S. have ordered stay-at-home policies. It is useful to see how administering these orders can affect the case numbers, how would the case numbers react if the government revoke the orders. As our test dataset, We applied our methods to California. 

Each county is never in total isolation from other counties. There is always traffic going in and out of the counties at county borders. So it is necessary to account for the relative mobility, what are the neighboring counties and what are the infection numbers of the neighboring counties to predict infection numbers for each county.

We will use spatial dynamics to predict case numbers for the next day based on the case numbers of the previous day (and of course, geographical information and mobility score)

## Result & Discussion

### Example: California, 3/2/2021

<img src="https://user-images.githubusercontent.com/49173407/110284425-c6f02a80-801c-11eb-8111-d7e41d4a01cb.png" width="45%"></img> <img src="https://user-images.githubusercontent.com/49173407/110284418-c2c40d00-801c-11eb-9ec7-4ea5a8ac02b1.png" width="45%"></img>

These two Heat maps shows how different the actual cases as well as the predicting cases differently distributing in California. From the actual cases map, Los Angelas county with darkest green has the most number of actual cases. However after predicting based on the past days, Imperial county was predicted to have the most number of cases.


<img src="https://user-images.githubusercontent.com/49173407/110284967-847b1d80-801d-11eb-951d-939263e10974.png" width="45%"></img> <img src="https://user-images.githubusercontent.com/49173407/110284965-82b15a00-801d-11eb-9a8f-b05094107367.png" width="45%"> </img>

The absolute percent difference between actual cases and predicting cases, as the heatmap and the treemap show that most of the counties were predicted under 25%. In the meantime, we can see that the counties we have really "inaccurate" predictions is Imperial county, which is in the corners of all the counties we took into consideration. The missing data for neighboring counties for the counties on edges/corners can explain away some of the inaccuracy in predictions for these counties.

<img src="https://user-images.githubusercontent.com/49173407/110285583-6c57ce00-801e-11eb-8805-1aabbde36d29.png" width="45%"></img>

In addition, the positive or negative percent difference is another issue to investigate on. 


## Contact US
- Shuyuan Wang shw276@ucsd.edu
- Caiwei Wang caw062@ucsd.edu
