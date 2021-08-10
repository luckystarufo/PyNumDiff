---
title: 'PyNumDiff: A Python package for Numerical Differentiation of noisy time-series data'
tags:
  - Python
  - numerical differentiation
  - denoising
  - dynamics
  - time series
  - machine learning
authors:
  - name: Floris Van Breugel^[corresponding author]
    affiliation: 1
  - name: Yuying Liu
    affiliation: 2
  - name: J. Nathan Kutz
    affiliation: 2
affiliations:
 - name: Department of Mechanical Engineering, University of Nevada at Reno
   index: 1
 - name: Department of Applied Mathematics, University of Washington
   index: 2
date: 10 July 2021
bibliography: paper.bib
---

# Statement of need

Calculating numerical derivatives is ubiquitous in many scientific computing and engineering applications such as 
image reconstruction, density estimation, signal processing and model discovery. Therefore, 
a variety of methods were developed for its treatment. But since their mathematical formulations and procedures are 
very different, researchers often resort to an ad hoc process for choosing one of many computational methods and its 
parameters, yielding unreliable results. Here, we take a principled approach and propose a multi-objective optimization 
framework which facilitates unbiased comparisons across different methods. Notably in this framework, there is only a 
small number of tuning parameters which balance the faithfulness and smoothness of the derivative estimate. 

Methods implemented in this work were originally used for data pre-processing in the sparse identification of nonlinear 
dynamics (SINDy)[@brunton2016discovering; @de2020pysindy], an algorithmic approach for dynamic model discovery. The goal is to discover the underlying governing 
equation from the measurement data and one important step is to use numerical derivatives of measured states to 
populate the feature library so that one can uncover the structure of the model with sparse regression techniques. 
Unfortunately, such measurement data are usually polluted by noise which makes the calculation of numerical derivatives 
sensitive. Obtaining reliable numerical derivatives therefore becomes critical to the success of the approach. 

Regardless of its specialty, we hope to make this toolbox widely accessible to scientists across domains and at various 
levels of mathematical expertise. Therefore, all methods were put together and open-sourced in the package `PyNumdiff`, 
aiming to facilitate easy application to diverse data sets.


# Summary

`PyNumdiff` is a Python package that implements methods for computing numerical derivatives of noisy data. 
In this package, we mainly implement four commonly used families of differentiation methods which take different 
assumptions, including both global and local methods [@ahnert2007numerical]. The first family of methods usually start by 
applying a smoothing filter to the data, followed by a finite difference calculation[@butterworth1930theory]. 
The second family relies on building a local model of the data through linear regression, and then analytically 
calculate the differentiation based on the model[@belytschko1996meshless; @schafer2011savitzky; @savitzky1964smoothing]. 
The third family we consider is the Kalman filter[@kalman1960new; @henderson2010fundamentals; @aravkin2017generalized; @crassidis2004optimal], 
with unknown noise characteristics. And the last family is an optimization approach based on total variation 
regularization (TVR) method [@rudin1992nonlinear; @chartrand2011numerical]. For more technical details, 
refer to [@van2020numerical].

For ease of use and updating flexibility, most APIs are directly provided as Python methods. Applying `PyNumDiff` usually 
takes three steps: (i) pick a differentiation method, (ii) obtain optimized parameters and (iii) apply the differentiation. 
Step (ii) can be skipped if one wants to manually assign the parameters, which is not recommended. Together with the four
families of differentiation methods, optimization routines are also encapsulated in a sub-module (smooth_finite_difference, 
linear_model, kalman_smooth, total_variation_regularization, optimize). The package provides a few standard options for 
optimization solver (CVXOPT) and parameter selection, users can also specify their own for further customization. 


The software package includes tutorials in the form of Jupyter notebooks. These tutorials demonstrate the usage of above 
features. For more detailed information, there is a more comprehensive Sphinx documentation associated with the repository.

# Acknowledgements

Fundings ??

# References