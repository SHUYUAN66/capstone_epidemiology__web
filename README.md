
# Using Epidemiology Model To Predict Case Numbers for COVID-19

## Table of contents
* [General info](#general-info)
* [Technologies](#technologies)
* [Setup](#setup)
* [Directions](#directions)
* [Processing](#in_processing)

## General info
- Use covid-19 datasets provided by JHU to fit epidemiology model to U.S.. After figuring out the infection parameter, we can then predict 

## Introduction
Fitting Epidemiology Model with Covid-19 JHU U.S. Data

## Technology
Project is created with:
* Image : ucsdets/scipy-ml-notebook	

## Setup
- Before running, use `pip install -r requirements.txt` to install all the required packages
- on terminal, run `python run.py data` to retrieve the most current data from JHU & Apple Data

## Directions
`python run.py test` to start

## Processing

  ### Achievements

We applied our methods to south California.  We obtained the following results:At US country level (Figure 1), the model is underestimating the number of cases.  At state and countylevel (Figure 2 and Figure 3), the model is overestimating the number of cases

  ### Problem to Solve

- [TODO] Using Apple's mobility data, we are able to fit a Bayesian model and use the model to predict future number of infected with new lockdowns/un-lockdowns. 

## Contact
- Shuyuan Wang shw276@ucsd.edu
- Caiwei Wang caw062@ucsd.edu
