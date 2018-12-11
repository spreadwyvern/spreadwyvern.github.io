---
title: "Kidney Function Classification and Prediction Through Ultrasound-based Kidney Imaging: From Deep Learning to Mass Screening of Chronic Kidney Disease "
layout: single
author_profile: true
permalink: /projects/kidney/egfr/
header:
  image: /assets/images/kidney_model_design.png
  caption: "The model for predicting kidney function."
toc: true
---

## Abstract
Prediction of kidney function and chronic kidney disease (CKD) through kidney ultrasound imaging has long been considered desirable in clinical practice because of its safety, convenience, and affordability. However, this highly desirable approach is beyond the capability of human vision. We developed a deep learning approach for automatically determining the estimated glomerular filtration rate (eGFR) and CKD status. We exploited the transfer learning technique, integrating the powerful ResNet model pretrained on an ImageNet dataset in our neural network architecture, to predict kidney function based on 4,505 kidney ultrasound images labeled using eGFRs derived from serum creatinine concentrations. To further extract the information from ultrasound images, we leveraged kidney length annotations to remove the peripheral region of the kidneys and applied various data augmentation schemes to produce additional data with variations. Bootstrap aggregation was also applied to avoid overfitting and improve the model’s generalization. Moreover, the kidney function features obtained by our deep neural network were used to identify the CKD status defined by an eGFR of <60 ml/min/1.73m2. A Pearson correlation coefficient of 0.741 indicated the strong relationship between artificial intelligence (AI)- and creatinine-based GFR estimations. Overall CKD status classification accuracy of our model was 85.6% —higher than that of experienced nephrologists (60.3%–80.1%).  Our model is the first fundamental step toward realizing the potential of transforming kidney ultrasound imaging into an effective, real-time, distant screening tool. AI-GFR estimation offers the possibility of non-invasive assessment of kidney function, a key goal of AI-powered functional automation in clinical practice. 

## Slides

<style>
.responsive-wrap iframe{ max-width: 100%;}
</style>
<div class="responsive-wrap">
<!-- this is the embed code provided by Google -->
  <iframe src="https://docs.google.com/presentation/d/e/2PACX-1vSrqUfrvGpnvan2MnXPxtbv19NElpJcRIxPKP__vf43YKBSA2p38jdIm88htGljzmRzRHPluuzh9nlQ/embed?start=false&loop=false&delayms=3000" frameborder="0" width="960" height="749" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>
<!-- Google embed ends -->
</div>

### Links
- [Link to the slides about the project.](https://docs.google.com/presentation/d/12E7BDb0iw8yRu9tH8eVg-oo3E04Rx9qVv3PDxhAUwTA/edit?usp=sharing)
- [Github Repository](https://github.com/spreadwyvern/kidney-sonography)