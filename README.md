
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
- Image : ucsdets/scipy-ml-notebook	

## Setup
- Before running, use `pip install -r requirements.txt` to install all the required packages
- on terminal, run `python run.py data` to retrieve the most current data from JHU & Apple Data

## Directions
`python run.py test` to start

## Processing
### Gradient Descent to solve for math$\beta$ and $\frac{1}{D}$ 

Given: 

\begin{align*}
  &\xi = \frac{1}{D} \\
  &f_s(I_n,N,S_n) = -\beta\left(\frac{I_n}{N}\right) S_n, \\
  &f_I(I_n,N,S_n) = - I\xi + \beta\left(\frac{I_n}{N}\right) S_n,  \\
  &f_R(I_n) = I_n\xi, \\
  &h=1
\end{align*}


Plug the above values into
$\frac{1}{N} \sum_{n=1}^N \nabla_{\theta} \left( \left({\frac{s(n+1)-s(n)}{h} - f_s(s(n), I(n), R(n);\theta)}\right)^2
+ \left({\frac{I(n+1)-I(n)}{h} - f_I(s(n), I(n), R(n;\theta)}\right)^2 + \dots \right)$

To calculate the above the term, we need to use __chain rule__ to differentiate with respect to $\beta$ and $\xi$

$\nabla_{\beta} = 2 \cdot \left(\frac{S_{n+1} - S_{n}}{h} - \left(-\beta S_n  \frac{I_n}{N}\right) \right) \cdot \left(S_n \cdot \frac{I_n}{N}\right) + 2 \cdot \left(\frac{I_{n+1} - I_{n}}{h}  - \left( -\xi_k I_n + \beta_k \frac{I_n}{N} S_n \right)\right) \cdot \left( -S_n \cdot \frac{I_n}{N}\right)$

$\nabla_{\xi} = 2 \cdot \left(\frac{I_{n+1} - I_{n}}{h}  + \left(I_n\xi_k - \beta_k \frac{I_n}{N}S_n\right) \right) \cdot \left(I_n\right) + 2 \cdot \left(\frac{R_{n+1} - R_{n}}{h} - I_n\xi_k\right) \cdot \left( -I_n\right)$



## Tuning
First initialize $\theta$ at $\beta = 0.2 $ and $\xi = 0.1$


Then, at each iteration update $\beta$ and $\xi$ according to the rules below


$\beta_{k+1} = \beta_k - h_G \partial_\beta L(\theta|s(1),\dots,s(N)),$


$
\xi_{k+1} = \xi_k - h_G \partial_\xi L(\theta|s(1),\dots,s(N)).$
 where $h_G = 0.001$
### Achievements

We applied our methods to south California.  We obtained the following results:At US country level (Figure 1), the model is underestimating the number of cases.  At state and countylevel (Figure 2 and Figure 3), the model is overestimating the number of cases.
<p align="center"><img width=12.5% src="" ></p>
<p align="center"><img width=12.5% src="" ></p>

### Problem to Solve

- [TODO] Using Apple's mobility data, we are able to fit a Bayesian model and use the model to predict future number of infected with new lockdowns/un-lockdowns. 

## Contact
- Shuyuan Wang shw276@ucsd.edu
- Caiwei Wang caw062@ucsd.edu
