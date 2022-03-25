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

**SHAP Analysis - Top 5 Features**
* The **number of mosquitoes** caught in a trap was the most important predictor of whether West Nile virus would be present. This makes sense because, even when West Nile conditions are optimal, there is not necessarily a high likelihood that any individual mosquito will be West Nile positive. As more mosquitos are caught in a trap, it becomes more likely that at least one mosquito will be West Nile positive. 
* As the **average daily temperature with a 23-day lag** increased, it was more likely that West Nile virus would be present. Mosquitos tend to thrive in warmer environments so this was not surprising. The warmer temperatures likely led to improved mosquito breeding conditions and, therefore, higher mosquito population numbers. However, the effect will not be seen immediately. The length of the mosquito life cycle tends to be 2-4 weeks (although it can be shorter depending on weather conditions). This is a likely explanation for the importance of the 23-day lag.
* As the **mean wind speed from 7-14 days prior** increased, the presence of West Nile virus decreased. Higher wind speeds likely make it more difficult for mosquitos to fly, reducing both their ability to fly greater distances and to accurately fly to their target destination. Therefore, higher wind speeds may result in reduced mosquito breeding. The importance of the 7-14 day lag is likely due to the length of the mosquito life cycle which tends to be 2-4 weeks, but can be as short as one week in peak summer conditions.
* Traps were considered **within the spray boundaries** when they were inside the box created by the northernmost, southernmost, easternmost, westernmost spray location (up to that point in the year). The trap locations within the spray boundaries tended to have a much higher West Nile presence. This is likely due to correlation rather than causation. Spraying may have been a reactive response in areas that were already known to have either high levels of West Nile presence or high mosquito counts. It makes sense that spray boundaries, not only the spray zones, were important because individual mosquitos are not necessarily confined to a small area. Mosquitos have a maximum flight distance of 50m to 50km, depending on the species. Therefore, if there is a high mosquito count in one area, it is likely that there will be a high mosquito count in neighbouring areas (assuming relatively similar environments). This should hold true for West Nile presence as well.
* As **average wind speed with a 15-day lag** increased, the presence of West Nile virus decreased. As mentioned above, higher wind speeds likely reduce both the distance mosquitos are able to fly and the ability of a mosquito to accurately fly to a target destination. This can be expected to result in reduced mosquito breeding. A delayed impact on mosquito population numbers would be observed, since the mosquito life cycle takes 2-4 weeks. Again, this explains the importance of the 15 day lag.

**SHAP Analysis - Other Feature Importance Observations**
* A **23-day lag** seemed to be especially significant. Temperature and average wind speed lagged by 23 days both showed up in the top 6 most important features. Total precipitation lagged by 23 days also showed some importance. The typical mosquito life cycle is 2-4 weeks and varies based on environmental factors including temperature and moisture levels. It is possible that a life cycle of roughly 23 days tends to be common in the conditions created by the Chicago climate.
* Higher **relative humidity** tended to go along with higher West Nile virus presence. Importance in relative humidity was seen for both a 4-day and 10-day lag. With the 4-day lag time, it is likely that mosquito activity increased with humidity, resulting in a higher number of mosquitoes being caught in the traps. Since traps were not checked daily, mosquitos may be caught in a trap for a few days before being discovered. With the 10-day lag time, it is likely that increased humidity improved breeding conditions for mosquitos. The mosquito life cycle is shorter in peak summer heat (which is often accompanied by high humidity levels). This may explain why a 10-day lag was important with relative humidity rather than the longer lag times associated with other weather features.
* The mosquito **species** showed some importance in the model. Only two species - Culex Restuans and Culex Pipiens - were caught in significant numbers. These were also the only two species that were observed to be West Nile virus positive. **Culex Restuans**  mosquitoes were less likely to test positive for West Nile virus.
* Among **location** based features, the **Northwest Zone** identified during the EDA phase was positively correlated with the presence of West Nile. It is possible that this area provides an optimal environment for either mosquitoes or for bird species that are susceptible to West Nile virus (since mosquitoes become West Nile virus carriers by biting birds infected with the disease).
* **Seasonality** also played a role in West Nile virus prediction, as week of the year indicators appeared in the top 20 most important features. Weeks 28 and 34 had negative and positive correlations with the presence of West Nile virus respectively.
* **Precipitation** had a varied effect, but the two most important precipitation features had long lag times (mean precipitation with a lag of 28-35 days, and precipitation with a lag of 27 days). In these two cases, precipitation was negatively correlated with West Nile virus. This may be due to the fact that water sources become more scarce in dry conditions. Culex species tend to disperse more widely under these conditions, as adequate breeding grounds become more scarce. Additionally, contact between birds and mosquitoes tends to increase in dry conditions, as they both rely on the few remaining water sources. This increases the likelihood that mosquitoes will bite a bird that is infected with West Nile virus. On the other hand, mosquito numbers tend to increase in rainy conditions. This may explain why precipitation can have a varied impact on the presence of West Nile virus.

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