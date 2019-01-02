---
title: "Detection of Early Neurodegeneration with DTI"
layout: single
author_profile: true
permalink: /projects/brain/brain/
header:
  image: /assets/images/project_banner.png
  caption: ""
toc: true
---

## Abstract
With the advancement of neuroimaging, nowadays we have various modalities of neuroimages. New technique in magnetic resonance imaging with diffusion tensor imaging (DTI) provides us with more detail informations regarding the white matter. Numerous studies had focused on assessment of pathology and degeneration of whitematter with DTI. 
We implemented state-of-the-art deep learning method with convolutional neural neworks to assess normal aging in healthy indivisuals. The trained neural network then has the potential to detect early neurodegeneration in patients.

## Introduction
- Neuroimaging-derived age predictions have been explored in the context of different brain diseases. 
- By training models on healthy individuals, brain-predicted age can be thought to reflect some aberrant accumulation of age related changes to the brain
- The degree of ‘added’ brain aging can be easily quantified by subtracting chronological age from brain-predicted age
- Increased brain-predicted age has been reported in adults with traumatic brain injuries

## Conventional Machine Learning Approaches of Brain MRI
There are various researches on brain MRI using convetional machine learnings. To name a few:
- Prediction of Brain Age Suggests Accelerated Brain Atrophy After Traumatic Brain Injury
   - James H. Cole, PhD, Robert Leech, PhD, and David J. Sharp, PhD, for the Alzheimer’s Disease Neuroimaging Initiative
   - Ann Neurol. 2015 Apr; 77(4): 571–581
- Predicted age for each healthy individual in the training set (n * 1,537)
   - Gray Matter (predicted–chronological age correlation r * 0.921, R2 * 0.848, MAE * 6.2 years)
   - White Matter (r * 0.922, R2 * 0.851, MAE * 6.16 years).
![conventional result](/assets/images/neuro/conventional.png)
Conventional method envolves using Statistical Parametric Mapping (SPM) structural preprocessing pipeline to generate gray and white matter maps, normalized to Montreal Neurological Institute (MNI) space. The process is rather time-consuming.

## Related Works Using Convolutional Neural Networks
- Age estimation from brain MRI images using deep learning
   - [Tzu-Wei Huang et. al.](http://www.cs.nthu.edu.tw/~htchen/aemri/aemri.pdf)
   - 2017 IEEE 14th International Symposium on Biomedical Imaging (ISBI)
- Predicting brain age with deep learning from raw imaging data results in a reliable and heritable biomarker
   - [James H Cole et. al. 2016](https://arxiv.org/abs/1612.02572)
   - Propose a 3D convolutional neural network to predict brain age
   - Study population: 2001 health individuals

## Dataset
We used the open database from Cambridge Centre for Ageing and Neuroscience (Cam-CAN) dataset, with 558 healthy subjects, age range from 16 to 88 with T1, T2 and diffusion tensor images (DTI).
Using python package, “dipy”, we reconstructed the diffusion tensor images (DTI) and diffusion kurtosis images (DKI).
- image dimension: [96, 96, 66] (H, W, D)
- DTI (Diffusion Tensor Image)
   - FA, MD, AD, RD, color FA
- DKI (Diffusion Kurtosis Image)
   - FA, MD, AD, RD, color FA
In our experiment, **FA and MD DTI images** werer chosen as the performance was better in our task.

![samples of reconstructed MRIs](/assets/images/neuro/dti_dki.png)

## Data Preprocessing
We performed denoicing and data augmentaions
- Denoising
   - Gaussian 
   - Non-local means
   - None
- Augmentation
   - random rotation: [-25, 25] degrees
   - random shift: [-5, 5] pixels

## Our 3D CNN model
- To reduce number of network parameters, we use deeper bottleneck architecture proposed by He et. al. <https://arxiv.org/abs/1512.03385 >
![bottleneck architecture](/assets/images/neuro/structure.png)
 - Instance Normalization (IN) : normalize based on individual instances instead of the batch as a whole <https://arxiv.org/abs/1607.08022>
 - A block of convolution: Conv (1X1) + IN + ReLU + Conv (3X3) + IN + ReLU + Conv (1X1) + IN + ReLU 

Comparison of our model architecture with Jame H Cole et. al.
![model comparison](/assets/images/neuro/result_table.png)

## Results
The best result was achieved with a model with 4 3D convolution blocks. Donoising with non-local means shown best overall performance in our experiment.

![](/assets/images/neuro/result.png)

Comparison of our model's performance with related researches.
![comparisons](/assets/images/neuro/comparison.png)


## Limitations
1. Limited data: The Cam-CAN dataset only contains 558 samples, with more data we can further trained a mroe acurate model
2. Relatively low resolution: compared with other sequences of brain MRI, DTI has lower resolutions, which might restrained the CNN model from obtaining more information. Yet this problem is oriented from the difference in imaging mechanism between DTI and other brain MRI sequences, with further advancement of MRI technology we may be able to obtain DTI with higher resolution in the future.

## Conclusion
- We propose a 3D convolutional neural network, which applies on diffusion tensor images, to accurately predict ages of healthy subjects (MAE=4.29)
- The trained model can be used to detect early-stage neurodegeneration
  - If brain-predicted age greater than chronological age, the ‘added’ age can be quantified as the difference between chronological age and brain-predicted age

## Prediction model
The trained prediction model is provided on GitHub repository. [**link**](https://github.com/spreadwyvern/neurodegeneration)

## Slides

<style>
.responsive-wrap iframe{ max-width: 100%;}
</style>
<div class="responsive-wrap">
<!-- this is the embed code provided by Google -->
  <iframe src="https://docs.google.com/presentation/d/e/2PACX-1vSlZaKOw-BVhiEaacO7Bdg4FbfwhTZWaP-Qs_3lbP21Goxin1CWdMmMfh7ymsPKoAlM7zEzFPmaWVmr/embed?start=false&loop=false&delayms=3000" frameborder="0" width="960" height="749" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>
<!-- Google embed ends -->
</div>

### Links
[Link to the slides about the project.](https://docs.google.com/presentation/d/1EtcB3jbhp1rrAvZ4CVIkq0QPqe0TyLV0vdIxaAhGWes/edit?usp=sharing)