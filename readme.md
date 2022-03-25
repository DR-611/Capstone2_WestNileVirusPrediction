# West Nile Virus Prediction in Chicago

***

### Business Problem and Background

**Problem Statement**
The City of Chicago and the Chicago Department of Public Health (CDPH) are seeking an improved method to predict when, and where, West Nile virus outbreaks will occur in mosquitoes. A solution will enable resources to be allocated more efficiently and effectively in the effort to reduce the transmission of West Nile virus.


**Background Information**
West Nile virus is transmitted to humans via infected mosquitoes. In severe cases, individuals can develop potentially fatal neurological illnesses. After first observing human West Nile virus cases in 2002, the City of Chicago and the CDPH initiated a program in 2004 to monitor mosquito populations and reduce the transmission of West Nile virus. Mosquito traps were established at different locations throughout Chicago and monitored for the presence of West Nile virus. This information was used to determine the location and timing of mosquito spraying efforts. Making use of mosquito trap data, Chicago weather data, and mosquito spray data the City of Chicago and the CDPH would like to improve their ability to predict the presence of West Nile virus in mosquitoes. An improved method of prediction will allow for greater effectiveness, and a more efficient allocation of resources, in the efforts to reduce transmission of West Nile virus.

References:
*https://www.kaggle.com/c/predict-west-nile-virus
***
### Data Collection

**Mosquito trap data, Chicago weather data, and mosquito spray data will be used to develop our West Nile virus prediction model.**
* The **mosquito trap data** was gathered from mosquito traps that were placed at various locations throughout Chicago. Each trap was tested for the presence of West Nile virus on a weekly basis. The trap location, mosquito count, mosquito species, and presence of West Nile virus within the trap cohort was recorded.
* The **Chicago weather data** was procured from two City of Chicago weather stations: Chicago O’Hare International Airport and Chicago Midway International Airport.
* The **mosquito spray data** was a record of the City of Chicago’s efforts to control mosquito population and West Nile virus transmission using mosquito spray. The date and location of spraying was provided. 
***
### Modeling

**Model Evaluation**
In order to perform model evaluation, the **AUC-ROC Curve (AUC)**. ROC is effective at assessing model performance for binary classification problems. The AUC assesses the model’s ability to differentiate between the positive and negative class. 

**Modeling Options**
The following **8 machine learning models** were selected, trained, and used to make predictions on the test data:
* Logistic Regression
* Support Vector Classifier
* Random Forest Classifier
* Gradient Boosting Classifier
* XGBoost Classifier
* LightGBM Classifier
* AdaBoost Classifier
* Extra Trees Classifier

Additionally, a Dummy Classifier was used to establish a **baseline model**. The Dummy Classifier makes predictions by randomly drawing a class from a uniform distribution of the unique classes.

**Model Selection**
After initial modeling using the default hyperparameters for each of the 8 models, the **Gradient Boosting Clasifier** had the best initial performance (AUC = 0.8389).  Threfore, it was selected as the starting point to build a final model.

**HyperParameter Tuning**
In an attempt to improve upon the Gradient Boosting Classifier’s initial performance, hyperparameter tuning was performed. Hyperparameter tuning **improved the model's AUC score to 0.8425.** The best parameters for the model were the following:
* learning_rate: 0.1
* max_depth: 3
* subsample: 0.75
* max_features: 'log_2'
***
### Conclusions

**Recommendations to the City of Chicago and CDPH**
A trained Gradient Boosting Classifier will be provided to the City of Chicago and CDPH, which will provide an improved ability to predict where, and when, West Nile virus will occur. Weather data and mosquito population trends can be monitored, and the Gradient Boosting Classifier can be used to model different scenarios to proactively determine if, and when, different areas are at risk for the presence of West Nile virus. **The following are recommendations** on how the City of Chicago and CDPH can make use of this capability:

1. **Mosquito Spraying** 
Mosquito spraying can be done in locations where West Nile virus is predicted to be present. The model’s predictive ability should allow for mosquito spraying efforts to be more effective. Spraying can be done proactively when conditions are ideal for West Nile virus. Therefore, mosquito population numbers can be reduced prior to the occurrence of a West Nile virus outbreak. This should be more effective in limiting the West Nile virus risk to the human population than the current reactive approach to spraying. 

2. **Public Awareness**
	Modeling can also be used to inform the public of West Nile virus risks at different times and locations throughout mosquito season. The predictive ability of the model will allow the public to be given advance notice of the risks, giving individuals time to plan accordingly. 

3. **Insights from EDA and SHAP Analysis**
In addition to making use of the model, several important insights can be taken from the EDA and Feature Importance Analysis stages of the exploration. West Nile virus season tends to begin around July 15th, and the presence of West Nile virus is at its peak in August. The risks are especially high in areas with a high concentration of Culex Pipiens mosquitoes. In peak West Nile virus season it should be noted that the Chicago downtown core appeared to be especially safe, while West Nile virus presence in the Northwest Zone (identified during EDA) was very high. In terms of weather, high temperatures, high humidity, and low wind speeds appeared to create favourable conditions for the appearance of West Nile virus 1-3 weeks later. 

**Recommendations for Future Investigation**
* Incorporating bird population data into a model may be beneficial. Mosquitoes become West Nile virus carriers by biting birds infected with the disease. Analyzing susceptible bird species, bird migration patterns, bird habitat information, and West Nile virus presence in birds may provide additional value.
* An analysis of Chicago geography/terrain may be valuable. This could provide a finer grained understanding of which locations provide favourable habitats for mosquitoes. Identifying which areas are forested, grasslands, swampy, or urban could be beneficial for understanding and modeling.
* Checking mosquito traps daily may provide a more accurate picture of mosquito population and West Nile virus trends. However, City of Chicago resource allocation will be a factor here. 
* Adoption of the model should lead to more proactive spraying. Analysis of these efforts may allow for a better understanding of the impact of spraying.
* Weather data was only provided for May through October. Analyzing annual weather data may be beneficial in determining the impact of winter and early spring weather conditions on mosquito numbers and/or West Nile virus presence later in the year. 
* The model found that mosquito population numbers were an important West Nile virus predictor. Therefore, it may be worth doing further research into factors that impact mosquito populations. It may be possible to collect data on these factors and incorporate them into a future model.
***