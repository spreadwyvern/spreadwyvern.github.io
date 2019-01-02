---
title: "Towards the Automation of Kidney Function Classification and Prediction Through Ultrasound-based Kidney Imaging Using Deep Learning"
layout: single
author_profile: true
permalink: /projects/kidney/egfr/
header:
  image: /assets/images/project_banner.png
  caption: "The model for predicting kidney function."
toc: true
---
<!-- 
## Abstract
Prediction of kidney function and chronic kidney disease (CKD) through kidney ultrasound imaging has long been considered desirable in clinical practice because of its safety, convenience, and affordability. However, this highly desirable approach is beyond the capability of human vision. We developed a deep learning approach for automatically determining the estimated glomerular filtration rate (eGFR) and CKD status. We exploited the transfer learning technique, integrating the powerful ResNet model pretrained on an ImageNet dataset in our neural network architecture, to predict kidney function based on 4,505 kidney ultrasound images labeled using eGFRs derived from serum creatinine concentrations. To further extract the information from ultrasound images, we leveraged kidney length annotations to remove the peripheral region of the kidneys and applied various data augmentation schemes to produce additional data with variations. Bootstrap aggregation was also applied to avoid overfitting and improve the model’s generalization. Moreover, the kidney function features obtained by our deep neural network were used to identify the CKD status defined by an eGFR of <60 ml/min/1.73m2. A Pearson correlation coefficient of 0.741 indicated the strong relationship between artificial intelligence (AI)- and creatinine-based GFR estimations. Overall CKD status classification accuracy of our model was 85.6% —higher than that of experienced nephrologists (60.3%–80.1%).  Our model is the first fundamental step toward realizing the potential of transforming kidney ultrasound imaging into an effective, real-time, distant screening tool. AI-GFR estimation offers the possibility of non-invasive assessment of kidney function, a key goal of AI-powered functional automation in clinical practice.  -->


Kidney ultrasound imaging is widely used in clinical applications, such as excluding reversible causes of acute kidney injury such as urinary obstruction and identification of irreversible chronic kidney disease(CKD) that precludes unnecessary workup such as kidney biopsy.
Ultrasound comes with many advantages, it's non-invasive, relatively lower in cost, and has wider availability. Thus, prediction of kidney function and chronic kidney disease (CKD) through kidney ultrasound imaging has long been considered desirable in clinical practice. However, the high subjective variability in image acquisition and interpretation makes it difficult to translate experience-based prediction into standardized practice, such as invasive serum creatinine measurement.
Generally in clinical practice, some aspects of kidney ultrasounds are used as markers for evaluation of severity of kidney injuries. Kidney length, volume, cortical thickness, and echogenicity. There are a few relative studies in evaluation of renal function with ultrasounds. Yet the results were suboptimal or based on small samples.

|markers	|correlation by prior studies	|notes
---|---|---
length|0.36|
volume|0.4-0.49|
cortical thickness|0.852|only 42 samples

Yapark et al, 2017 developed a CKD scoring system that integrate three ultrasonographic parameters: kidney length, parenchymal thickness, and echogenicity, but the correlation remain at 0.587

### Our Goal
To overcome substantial inter-observer variability in kidney ultrasound interpretation, we train a deep learning model to inform better clinical decision, including:
- Part 1. Predict the present eGFR
- Part 2. Classification of CKD status

### Study Population
Initially we enrolled 8,281 pre-ESRD patients at China Medical University, aged 20–89 years, with a total of 203,353 sonographic images since 2003. Regarding sharpness, contrast, and noise, we selected studies performed after 2014 that used GE ultrasound systems (LOGIQ E9 and LOGIQ P3, GE Healthcare, Milwaukee, WI, USA). 
eGFR was measured within 4 weeks before or after the day of the kidney sonography using the abbreviated MDRD equation
- eGFR = 186 × creatinine−1.154 × age−0.203 × 1.212 [if black] × 0.742 [if female]

### Dataset and Data Cleaning
Total images: 37,696 (acquired after 2014)

- Training set:
  - Around 1106 patients
  - Around 3500 images
- Validation set:
  - Around 180 patients
  - Around 180 images (Only selected the image with the clearest kidney from each patient)
- Testing set:
  - 160 patients
  - 160 images (Only selected the image with the clearest kidney from each patient)

### Preprocessing
There are plenty of obstacles in obataining a clean kidney ultrasound, the surrouding organs like liver, intestines and spleen, or the adjacent tissues such as fat. Moreover, most ultrasound images contained annotations that are hardcoded to the images. These could pose as noises, or "distractions" to the deep learning model.
To cope with these noises, we developed a "tailored crop" cropping process, based on two markers annotating the kidney length. <!-- We first identified the positions of the two markers (x_1,y_1) and (x_2,y_2) and calculated their distance and middle point, denoted as d and (x_c,y_c), respectively. Next, we cropped the square region centered at (x_c,y_c) with a length d. To unify the size of the input images, we resized the cropped images to 224 × 224 pixels. -->
![tailored crop](/assets/images/kidney/tailor.png)




### Model Architecture
- Convolutional neural network based on ResNet-101 for prediction of eGFR.
- Extract features using trained CNN model
- Gradient boosted tree algorithm for classification of CKD stage (above stage 2 or not), using the above extracted features.

### Performance
#### For prediction of eGFR
![](/assets/images/kidney/result.png)
#### For classification of CKD stage
<p float="left">
  <img src="/assets/images/kidney/cfm.png" width="300" />
  <img src="/assets/images/kidney/cfm_table.png" width="300" /> 
</p>

<p float="left">
  <img src="/assets/images/kidney/auroc.png" width="300" />
  <img src="/assets/images/kidney/auroc_table.png" width="300" /> 
</p>

<!-- ![](/assets/images/kidney/cfm.png)
![confusion matrix](/assets/images/kidney/cfm.png "confusion matrix") ![classification result](/assets/images/kidney/cfm_table.png "classification result")
![AUROC](/assets/images/kidney/auroc.png "confusion matrix") ![classification result](/assets/images/kidney/auroc_table.png "classification result")
 -->
### Conclusion
Our model is the first fundamental step toward realizing the potential of transforming kidney ultrasound imaging into an effective, real-time, distant screening tool. AI-GFR estimation offers the possibility of non-invasive assessment of kidney function, a key goal of AI-powered functional automation in clinical practice. 

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