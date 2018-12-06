---
title: "Kidney Function Classification and Prediction Through Ultrasound-based Kidney Imaging: From Deep Learning to Mass Screening of Chronic Kidney Disease "
layout: single
author_profile: true
permalink: /projects/kidney/egfr/
header:
  image: /assets/images/kidney_model_design.png
  caption: "The galaxy above our medical mission's campus."
toc: true
---

## Abstract
Prediction of kidney function and chronic kidney disease (CKD) through kidney ultrasound imaging has long been considered desirable in clinical practice because of its safety, convenience, and affordability. However, this highly desirable approach is beyond the capability of human vision. We developed a deep learning approach for automatically determining the estimated glomerular filtration rate (eGFR) and CKD status. We exploited the transfer learning technique, integrating the powerful ResNet model pretrained on an ImageNet dataset in our neural network architecture, to predict kidney function based on 4,505 kidney ultrasound images labeled using eGFRs derived from serum creatinine concentrations. To further extract the information from ultrasound images, we leveraged kidney length annotations to remove the peripheral region of the kidneys and applied various data augmentation schemes to produce additional data with variations. Bootstrap aggregation was also applied to avoid overfitting and improve the model’s generalization. Moreover, the kidney function features obtained by our deep neural network were used to identify the CKD status defined by an eGFR of <60 ml/min/1.73m2. A Pearson correlation coefficient of 0.741 indicated the strong relationship between artificial intelligence (AI)- and creatinine-based GFR estimations. Overall CKD status classification accuracy of our model was 85.6% —higher than that of experienced nephrologists (60.3%–80.1%).  Our model is the first fundamental step toward realizing the potential of transforming kidney ultrasound imaging into an effective, real-time, distant screening tool. AI-GFR estimation offers the possibility of non-invasive assessment of kidney function, a key goal of AI-powered functional automation in clinical practice. 

## Slides
[Link to the slides about the project.](https://docs.google.com/presentation/d/12E7BDb0iw8yRu9tH8eVg-oo3E04Rx9qVv3PDxhAUwTA/edit?usp=sharing)