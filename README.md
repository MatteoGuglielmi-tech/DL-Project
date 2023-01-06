# TOC

<!--toc:start-->
- [Authors](#authors)
- [Unsupervised domain adaptation](#unsupervised-domain-adaptation)
  - [Problem statement](#problem-statement)
    - [Task in details](#task-in-details)
  - [Dataset](#dataset)
  - [Repository structure](#repository-structure)
  - [Results](#results)
        - [Real-World $\to$ product](#real-world-to-product)
        - [Product $\to$ real-world](#product-to-real-world)
<!--toc:end-->

# Authors
- Alessandro Zinni (Repository Owner) : [@github](https://github.com/Zinni98)
- Matteo Guglielmi (Collaborator) : [@github](https://github.com/MatteoGuglielmi-tech)

# Unsupervised domain adaptation 
This repository contains an implementation of an *Unsupervised domain adaptation* technique as practical part of the course "Machine Learning Module II" (Deep learning).   
For reference, [this paper](https://arxiv.org/abs/1904.04663) has been taken into consideration.

## Problem statement
In this assignment we are asked to build, train and evaluate a deep model that is able to counteract the negative impact of a domain shift when the training and test sets
have different distributions. This can be considered as a simulation of a realistic case where only the training dataset is available.  
As the majority of UDA frameworks, the quality of our technique has been addressed by looking at the gain over a simple baseline (in this case a ResNet-34 has been used as reference).  
In this work, we had at our disposal two different datasets (see Section [Dataset](#Dataset) for details) and we were expected to **test** our
technique in **two different directions** : once taking the first datasets source and the second one as test and vice versa. This allows to 
address if the model is in any case biased on a specific direction or not. 

### Task in details
The basic object recognition task consists in predicting correctly, given as input an image depicting an object, the label associated 
with this object. In this specific case, the settings are a little bit different since we are considering a domain shift, i.e. we trained our
model **supervisedly** exploiting the ground truth labels and tested **unsupervisedly** on the *target domain* without explicitly using the labels
(labels in the target domains are used just to compute the cumulative accuracy).  
Briefly, we were required to:
- address the performances of a simple model to use it as reference (**baseline**)
- implement a more **sophisticated model** to achieve a gain in performances 
- test the baseline model exploiting also the labels on the test set to have an **upper bound** reference

All three steps needs to be performed using both datasets, in turn, as training and test sets.

## Dataset
The dataset used in this assignment is the [Adaptiope](https://openaccess.thecvf.com/content/WACV2021/papers/Ringwald_Adaptiope_A_Modern_Benchmark_for_Unsupervised_Domain_Adaptation_WACV_2021_paper.pdf) 
object recognition dataset. 
This dataset includes images from $33$ different domains but in the specific case of this work only two were used.  
More in detail, for the sake of this assignment $20$ randomly chosen categories from the product and real world domains have been used. 
As split sizes, a standard $80\%/20\%$ has been used.

## Repository structure
In this repository, you can find the adopted solution in the [project.ipynb](https://github.com/Zinni98/Symnet-Unsupervised-domain-adaptation/blob/main/project.ipynb)
notebook.

## Results

#### Single run

##### Real-World $\to$ product

| Model          | Test Accuracy     |
| :---           |         ---:      |
| Baseline       |   $91.75\%$       |
| Upper Bound    |   $96.75\%$       |
| SymNet         |   $95.25\%$       |

##### Product $\to$ real-world

| Model          | Test Accuracy     |
| :---           |          ---:     |
| Baseline       |    $80.75\%$      |
| Upper Bound    |    $91.75\%$      |
| SymNet         |    $89.75\%$      |

#### 5-fold cross-validation

##### Product $\to$ real-world

| Model          | Average Test Accuracy   | $\sigma$ Accuracy     |
| :---           |    :----:               |          ---:         |
| Baseline       |  $77.05\%$              |   $2.48\%$           |
| Upper Bound    |  $91.60\%$              |   $0.60\%$           |
| SymNet         |  $87.55\%$              |   $0.58\%$           |


##### Real-World $\to$ product

| Model          | Average Test Accuracy   | $\sigma$ Accuracy     |
| :---           |    :----:               |          ---:         |
| Baseline       |  $91.95\%$              |   $0.292\%$           |
| SymNet         |  $95.25\%$              |   $0.224\%$           |


Across the multiple run, our implementation, besides showing an improvement in accuracy, confirm to be more stable as well.

#### Student T-test
To further confirm the results obtained, a T-test has been performed. The latter shows a p-value of $0.0004$ so the null hypothesis is 
rejected and a significance difference in performances is confirmed.
