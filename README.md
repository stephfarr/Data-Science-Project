# Data Science Project

Please see the obesity dataset and Python file for full details of data and code.

# Executive Summary

This project explores the use of Random Forest (RF) to identify cohorts at risk of obesity based on lifestyle and behavioural factors. This project uses publicly available data to serve as a proof of concept for predictive modelling in addressing the real business challenge of obesity costs within the NHS and wider public sector whilst aligning with prevention priorities for the NHS and the Bury Locality. 

RF was selected due to the nature of the data provided and for interpretability through feature importance. Key results include a recall of 84%, potential for generalisation and the ability to use model outputs for decision making. Visualisations such as a feature importance chart were employed to support interpretability. 

Recommendations include future iterations using local data, including SHAP analysis for further interpretability and targeting, and further cost-benefit analysis. This project provides a strong case study for data-driven, prevention-focused predictive modelling within the Bury Locality. 

# Project Background

It is well documented that obesity can lead to serious health conditions (NHS, 2017) and costs the NHS around £6.5 billion per year (DHSC, 2023). Lord Darzi’s (Darzi, 2024) independent review of the NHS emphasised the need for Integrated Care Boards (ICB) to shift from reactive hospital care to preventative community care. In line with this, Bury Locality has established a major conditions board (‘Bury Integrated Care Partnership Locality Plan Refreshed for 2025/2026’, no date) to identify key issues, risks and gaps. 

This project supports that ambition by exploring the use of RF in identifying populations at higher risk of obesity based on demographic and behavioural factors. Such models could enable the Locality to target preventative interventions more effectively – ultimately improving health outcomes and achieving greater financial efficiency. 

# Methodology

To test this approach, publicly available data from a study on obesity (Koklu, N., & Sulak, S.A., 2024) has been sought, via Kaggle, to develop a proof of concept. Whilst the dataset is not UK-based, it provides an opportunity to assess the feasibility of RF in identifying at-risk populations. 

RF has been chosen due to it’s ability to handle mixed data types, non-linear relationships, imbalanced data, correlated variables and has shown to have better predictive performance than other classification models (Breiman, 2001). Feature importance is also a factor in RF that is useful to decision makers in resource targeting decisions.

# Data Infrasrtucture & Tools
The dataset includes demographic and behavioural factors and the variable coding was provided by the study authors (Figure 1).

![Figure 1](images/Figure%201.png) 

*Figure 1: Attributes and Values in Obesity Dataset*

The data comes in an Excel spreadsheet format (Figure 2) downloaded from [Kaggle.](https://www.kaggle.com/datasets/suleymansulak/obesity-dataset/data)

![Figure 2](images/Figure%202.png)

*Figure 2: Original data*

The project was developed locally in Jupyter Notebooks but, should this lead to the development of projects using NHS data, the organisation’s cloud-based infrastructure, Snowflake, could be used to ensure the most recent data is used and is suitably secured.

Python libraries (Figure 3) used included pandas for data manipulation, scikit-learn for modelling, numpy for maths and matplotlib and seaborn for data visualisation. These libraries are well established and well-used for these purposes.

![Figure 3](images/Figure%203.png)

*Figure 3: Importing relevant libraries into Jupyter Notebooks*

# Data Engineering

The data was pulled into a pandas dataframe for exploration and manipulation. Checks (Figure 4) were carried out for duplicate and null values. 

![Figure 4](images/Figure%204.png)

*Figure 4: Data exploration*

"For users (decision makers, analysts, experts, project stakeholder, etc), the interpretability of ML models is often as important as their predictive performance” (Haddouchi and Berrado, 2024). It is for this reason that, though it was not necessary to create bins for the Age and Height variables because RF splits the data at the optimal threshold when creating each tree, interpretability was prioritised because this project is a use-case for using predictive models in health care commissioning decision making and interventions are likely to be targeted at population groups, rather than people of individual ages and heights. (Figure 5). After binning, the original Age and Height fields were dropped from the dataframe.

![Figure 5](images/Figure%205.png)

*Figure 5: Creating bins for Age and Height variables*

According to Pinheiro et al, RF is not sensitive to scale so scaling of the data was not required (Pinheiro et al., 2025). If an alternative model, such as logistic regression, was used then the data would be normalised because that model is sensitive to scale.

Outcome data was found to be unbalanced (Figure 6), therefore the decision was made to apply class weighting to ensure the model didn’t simply favour the majority classes.

![Figure 6](images/Figure%206.png)

*Figure 6: Number of records per class*

Data was split the data into X and Y variables and encoded (Figure 7) because, although integers are used to represent values, they are not binary.  

![Figure 7](images/Figure%207.png)

*Figure 7: Splitting data into X and Y variables and encoding X variables*

Finally, the data was split into train and test sets with an 80%/20% split (Figure 8).

![Figure 8](images/Figure%208.png)

*Figure 8: Splitting data into train and test sets*

# Data Analytics

The data was checked for the best hyperparameters to use and applied to the model (Figure 9). 

According to (Rimal, Y., Sharma, N., Paudel, S. et al., 2025) “Cross-validation is a robust statistical approach to evaluating machine learning models by systematically splitting data into training and testing subsets. This method ensures models generalize effectively to unseen data, minimizing the risks of overfitting and underfitting.” and so cross-validation was included in the analysis.

![Figure 9](images/Figure%209.png)

*Figure 9: Hyperparameter tuning and model production*

Gradient Boosting (GB) is an alternative model to RF (Natekin and Knoll, 2013). To ensure the best model was used for the project, a GB model was also produced for comparison (Figure 10).

![Figure 10](images/Figure%2010.png)

*Figure 10: Creating Gradient Boosting model and confusion matrices*

Confusion matrices were produced for both models and feature importance calculated (Figure 11). 

![Figure 11](images/Figure%2011.png)

*Figure 11: Calculating feature importance*

# Results

Recall is the most important metric to this project as the cost to the NHS of missing a patient to offer health advice is more than providing advice to those who might not need it. 

![Figure 12](images/Figure%2012.png)

*Figure 12: Model evaluation metrics*

Recall for RF was 84% (Figure 12) which means the model is performing well. The high CV accuracy scores indicate that the model would generalise well and RF outperformed GB on all evaluation metrics. 

![Figure 13](images/Figure%2013.png)

*Figure 13: Confusion matrices for RF and GB*

Confusion matrices (Figure 13) indicated that RF predicted the class closer to the true class than GB. For example, GB incorrectly predicted 3 obese individuals as normal whilst RF predicted only one. 
Feature importance analysis (Figure 14) revealed that the most important features were:

•	Physical exercise – no physical activity

•	Frequency of vegetable consumption - always

•	Number of main meals daily – 3+

![Figure 14](images/Figure%2014.png)

*Figure 14: Feature importance analysis*

# Data Visualisation and Dashboards

To aid in communicating findings from the model, visualisations for feature importance and confusion matrices were created. Decision makers come from a variety of backgrounds but many would not know how to interpret a confusion matrix therefore they were created with the original class labels included (Figure 15).

![Figure 15](images/Figure%2015.png)

*Figure 15: Code to produce visualisations*

Feature importance visualisation is particularly useful to decision makers as these help to prioritise interventions based on lifestyle factors. Future iterations could include interactive dashboards for decision makers to explore the data in more detail, particularly if future iterations include demographic information so end-users can explore the most important features for different cohorts. 

# Impact and Conclusions

The model demonstrates strong predictive capability in identifying individuals at risk of obesity. Its generalisability to new data suggests a similar model could have application in a real-world setting and directly inform intervention planning. 

Nudge theory suggests behaviour change intervention is most effective at a change in life stage (Behavioural Insights Team, 2024). Health visitors could use these results to advise parents of new school starters about the benefits of active travel in reducing obesity risk. A cost-benefit analysis of planned interventions would strengthen decision making.

Whilst this project provides a strong use-case for predictive modelling in targeting preventative NHS interventions, the data is not local and therefore will contain bias towards the population it was collected from. 

Future iterations of the model could use a binary outcome instead of multi-class (e.g., overweight/obese vs not) to improve predictive power and interpretability. SHAP analysis could explains feature contributions to individual predictions (Kim and Kim, 2022). Deprivation or poverty indicators would support segmentation of people within interactive dashboards to assess health inequalities and support the Locality’s strategic focus in this area. 

# References

Behavioural Insights Team (2024) ‘EAST: Four Simple Ways to Apply Behavioural Insights’, BIT, 16 December. Available at: https://www.bi.team/publications/east-four-simple-ways-to-apply-behavioural-insights/ (Accessed: 7 July 2025).

Breiman, L. (2001) ‘Random Forests’, Machine Learning, 45(1), pp. 5–32. Available at: https://doi.org/10.1023/A:1010933404324.

‘Bury Integrated Care Partnership Locality Plan Refreshed for 2025/2026’ (no date). Available at: https://councildecisions.bury.gov.uk/documents/s43774/finalv13%20locality%20plan%20refresh%202526%20draft%2014.03.25%20vWB.pdf (Accessed: 30 June 2025).

Darzi, A. (2024) ‘Independent Investigation of the National Health Service in England’. UK Government. Available at: https://assets.publishing.service.gov.uk/media/66f42ae630536cb92748271f/Lord-Darzi-Independent-Investigation-of-the-National-Health-Service-in-England-Updated-25-September.pdf (Accessed: 30 June 2025).

DHSC (2023) ‘Government plans to tackle obesity in England – Department of Health and Social Care Media Centre’, 7 June. Available at: https://healthmedia.blog.gov.uk/2023/06/07/government-plans-to-tackle-obesity-in-england/ (Accessed: 30 June 2025).

Haddouchi, M. and Berrado, A. (2024) ‘A survey and taxonomy of methods interpreting random forest models’. arXiv. Available at: https://doi.org/10.48550/arXiv.2407.12759.

Kim, Yesuel and Kim, Youngchul (2022) ‘Explainable heat-related mortality with random forest and SHapley Additive exPlanations (SHAP) models’, Sustainable Cities and Society, 79, p. 103677. Available at: https://doi.org/10.1016/j.scs.2022.103677.

Koklu, N., & Sulak, S.A. (2024) Obesity Dataset. Available at: https://www.kaggle.com/datasets/suleymansulak/obesity-dataset (Accessed: 30 June 2025).

Natekin, A. and Knoll, A. (2013) ‘Gradient boosting machines, a tutorial’, Frontiers in Neurorobotics, 7, p. 21. Available at: https://doi.org/10.3389/fnbot.2013.00021.

NHS (2017) Obesity, nhs.uk. Available at: https://www.nhs.uk/conditions/obesity/ (Accessed: 30 June 2025).

Pinheiro, J.M.H. et al. (2025) ‘The Impact of Feature Scaling In Machine Learning: Effects on Regression and Classification Tasks’. arXiv. Available at: https://doi.org/10.48550/arXiv.2506.08274.

Rimal, Y., Sharma, N., Paudel, S. et al. (2025) Comparative analysis of heart disease prediction using logistic regression, SVM, KNN, and random forest with cross-validation for improved accuracy. Available at: https://www.nature.com/articles/s41598-025-93675-1 (Accessed: 1 July 2025).
