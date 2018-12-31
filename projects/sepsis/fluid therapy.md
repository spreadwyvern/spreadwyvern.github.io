---
title: "A Machine Learning Approach for Predicting Urine Output After Fluid Administration"
layout: single
author_profile: true
permalink: /projects/sepsis/fluid/
header:
  image: /assets/images/iceland.jpg
  caption: ""
toc: true
---
## Introduction
- Sepsis, is global health problem with high mortality and morbidity. 
- Currently intravenous fluid administration has been recommended as the first-line resuscitative therapy for septic shock patients. 
- However, excessive fluid administration could lead to complications like pulmonary edema, renal failure and impaired bowel function, and has been shown to be associated with increased mortality [1].

### Fluid Non-responders and Urine Output
- About 50% of patients with sepsis are actually not responsive to intravenous fluid resuscitation [2]. These “fluid non-responders” are at risk of being harmed by excessive fluid administration.
- Urine output is an important clinical parameter when assessing fluid balance, determining treatment strategy and predicting outcome. 
- We applied a machine learning method to predict whether a septic patient would have decreased UO or oliguria after fluid administration

## Data
Our data were from The Multiparameter Intelligent Monitoring in Intensive Care (MIMIC) III database (v1.4) [11]
- Sepsis was defined as a suspected infection (prescription of antibiotics and sampling of bodily fluids for microbiological culture) combined with evidence of organ dysfunction, defined by a Sequential Organ 
- Failure Assessment (SOFA) score greater or equal to 2.
- 19,275 patients were included, totally 232,929 events. 
  - 135,735 events (58.27%) were labeled as having decreased UO
  - 89,699 events (38.51%) were labeled as oliguria.

### Preprocess
- Data were included from up to 24 hours preceding the diagnosis of sepsis and until 48 hours following the onset of sepsis
- For each patient, clinical data are aggregated into windows of 4 hours as an event.
- From each event, we extracted patient features including:
  - Demographics
  - vital signs
  - laboratory results
  - amount of fluid administration
  - amount of UOs. 

### Dynamic Change of a Patient’s Condition
- The dynamic change of a patient’s condition is an important clinical feature event[3]
- We integrated features acquired during the corresponding time window (Fc)
- Also included the features of precedent event (Fp). 

### Feature Sets
![feature sets](/assets/images/sepsis/features.png)

## Outcome Measurements
- Decreased amount of UO compared to that in the previous time window. 
- Oliguria
  - defined as the amount of UO is less than 0.5 ml/kg per hour.

## Model Architecture and Interpretability
- The model of choice was based on gradient tree boosting algorithm.
  - eXtreme Gradient Boosting (XGBoost)[4].
- A tree based algorithm is superior in interpretability to other machine learning algorithms
  - Provides information of which features are more decisive
    - Assist doctors in better understanding of patients’ condition
    - Provide more accurate treatment plan. 
- Advantages of XGBoost
  - Better cope with sparsity of data. 
  - Surpasses traditional tree-based models by introducing regularization to avoid overfitting
  - Utilizing gradient boosting to ensemble multiple tree models for better performance and also mitigates biases

## Model Training and Features Selection
- We trained XGBoost model using different features sets.
  - Fc and Fp
  - Fc alone
- The importance of each features were ranked.
Top ranked features were selected into different subsets ranging from top 15, 10, to 5 features. Individual models were trained on these subsets respectively.

## Result
- Regarding the attributes for training the models, adding the features of precedent event (Fp) slightly improved the performance of models. 
- The more attributes used, the more accurate the models could be.
  - Models only using the top 5 ranked features could still reach an optimal performance with AUC of 0.84 and 0.86 respectively.

![uo result](/assets/images/sepsis/result_uo.png)

![bo_result](/assets/images/sepsis/result_bo.png)

### Feature Rankings
![ranking](/assets/images/sepsis/ranking.png)

## Conclusion
- It is suggested that UO may be used to guide fluid resuscitation.
- We proposed an machine learning method in predicting septic patients’ responses to fluid resuscitation therapy, which yielded moderately accurate results with AUC up to 0.86. 
- We exploited the concept of continuity of disease course
  - We added the features of precedent event and the variance of fluid status. 
  - Models trained on the combined dataset demonstrated 
  - Further concludes the idea that clinical conditions are better measured with dynamic indicators.
- Model using less features still could yield similar performance, demonstrating the clinical applicability of these models in clinical settings with limited data.

## Limitations
1. Retrospective clinical database
external validation with other clinical dataset would be needed to insure the clinical validity of this model.
2. The clinical impact of this model on patients’ outcome require further clinical evaluation.
3. We used 4 hours as our , which might be too narrow for some septic patients to generate clinically evident urine output increment.

## Reference
1. Sirvent J-M et al. Fluid balance in sepsis and septic shock as a determining factor of mortality. The American journal of emergency medicine. 2015
2. Bentzer P et al. Will this hemodynamically unstable patient respond to a bolus of intravenous fluids? Jama. 2016
3. Monnet X et al. Prediction of fluid responsiveness: an update. Annals of intensive care. 2016;
4. Chen T, Guestrin C, editors. Xgboost: A scalable tree boosting system. Proceedings of the 22nd acm sigkdd international conference on knowledge discovery and data mining; 2016: ACM.


## Slide

<style>
.responsive-wrap iframe{ max-width: 100%;}
</style>
<div class="responsive-wrap">
<!-- this is the embed code provided by Google -->
  <iframe src="https://docs.google.com/presentation/d/e/2PACX-1vT9_UWWfsmO5d85xt2zlj_G_0FW2IQ-MtKvTTi-_Jgf0NOxy6T3jTFbYAhmweak_AK4pEYZhGSqQ6sf/embed?start=false&loop=false&delayms=3000" frameborder="0" width="1280" height="749" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>
<!-- Google embed ends -->
</div>

### Links
- [Link to the slides about the project.](https://docs.google.com/presentation/d/1qA-_bxv17Pg7QewqsE0j3yZjosC6tx63Jm4xko1ksPE/edit?usp=sharing)