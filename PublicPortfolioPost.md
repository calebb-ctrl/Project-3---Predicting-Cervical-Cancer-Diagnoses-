# Project-3---Predicting-Cervical-Cancer-Diagnoses-
Introduction:

Cervical cancer is a type of cancer that develops in the cells of the cervix. Most cases are linked to high-risk HPV. Although it is considered highly preventable, cervical cancer is still the fourth most common type of cancer for women, stressing the need for more resources and research surrounding this issue. Additionally, due to the lack of resources in some countries, there were a total of 350,000 deaths in 2022 from cervical cancer (World Health Organization). This project uses a dataset from the UCI Machine Learning Repository to determine the most important features in predicting cervical cancer. This problem matters because this disease, while preventable, claims a large number of lives every year. Investigating potential factors in a diagnosis can help provide people with information on what habits may put them at risk. Regardless of what specific medical resources and treatments are available to people, they can gain an idea of what risk factors they have in their own lives. 

Our research question is: What factors amongst demographics, lifestyle habits, and medical history are most impactful in predicting a cervical cancer diagnosis?

Data

The data was collected at the “Hospital Universitario de Caracas” in Caracas, Venezuela, and covers demographics, habits, and medical history for the patients included. Patients had the choice whether or not to answer the questions. The dataset was found on GitHub but originated from the UCI Machine Learning Repository. 


The dataset has 858 rows with 36 columns, one of which is the target variable, Dx:Cancer. Each row represents a patient and their responses to questions for each column. The patients had the choice not to answer a question, so there are some missing values throughout the dataset. The features are Age, Number of sexual partners; First sexual intercouse; Num of pregnancies, details about smoking habits, details on different contraceptives, details on number, frequency, and type of STDs, diagnoses of different health issues (Cancer, HPV, etc.), and binary variables representing whether a person underwent different procedures to collect information. In this research, the following variables are being investigated.


Age: The age of the patient at the time of information collection.

Number of sexual partners: The number of sexual partners a patient has had.

First sexual intercourse: The age at which a patient first had sexual intercourse.

Num of pregnancies: The number of pregnancies a patient had; it is not stated whether this only includes full-term pregnancies. 

Smokes (packs/year): How many packs of cigarettes a patient smokes in one year.

Hormonal Contraceptives (years): The number of years a patient has been on hormonal contraceptives.

IUD (years): The number of years a patient has had an intrauterine device.

STDs (number): The total number of STDs a patient has had.

STDs: Time since first diagnosis: How long it has been since a patient was first diagnosed with an STD.

STDs: Time since last diagnosis: How long it has been since a patient was last diagnosed with an STD.

Dx:Cancer: Whether a person has been diagnosed with cervical cancer.

This is the target variable for the research, a binary categorical variable representing a positive or negative diagnosis.

Dx:CIN: Whether a person has been diagnosed with Cervical Intraepithelial Neoplasia.

Dx:HPV: Whether a person has been diagnosed with Human Papillomavirus.


All the features are numeric.


Preprocessing and Exploratory Data Analysis

The first step taken was to check for duplicate values across the entire original dataset. Any rows with identical answers for all the questions were treated as the same individual. It is unlikely that they would have had the same answers for everything, including multiple continuous variables. Looking at the numerical variables, we reviewed their distributions, data types, and outliers to ensure the values are plausible. All of the features had plausible minimum and maximum values, so no rows were dropped. 


The distribution of the target variable, Dx:Cancer, was also reviewed. There is a class imbalance present in this variable as there are only 18 positive classifications. This reflects real world trends but will be addressed in creating the models. 


The dataset contains null values in all columns except Age, Dx:Cancer, Dx:CIN, and Dx:HPV, a valid trend due to the fact that patients did not have to answer all questions. Missing values were filled with the median of the feature for most columns to ensure use of a valid value for these rows. However, in some cases, the median did not represent a legitimate value for all the rows. So, the rows missing values for that feature were instead dropped, as imputation would carry the risk of having illogical data. Additionally, the features STDs: Time since first diagnosis and STDs: Time since last diagnosis each contained mainly null rows, so these columns were dropped. 


Additionally, some connection exists between numeric features, as seen in (Figure 2). Various independent variables have high correlation with each other, particularly Age, which was addressed by creating a new column, Time since first sexual intercourse to remove privacy issues and correlation from including Age (Figure 2). First sexual intercourse was subtracted from Age to create this variable to maintain the information Age lends to time of first sexual intercourse; that is, the length of time someone has been sexually active. 


Modeling

To address the class imbalance in the target, when splitting the data, the same proportion of positive and negative classifications present in the original dataset was preserved. The dataset was otherwise split into 80% for training and 20% for testing. Before modelling, the features were standardized to limit the effect of unbalanced distributions. 


Of the models, Logistic Regression performed best in terms of accuracy and errors. The recall was 0.5, meaning that the model correctly identified 50% of the actual positive diagnoses. The model also had a log loss of 0.028, indicating that it was fairly accurate and confident in predicting probabilities. The confusion matrix (Figure 4) also shows that the model caught 161 true positives, 1 negative, 2 false positives, and 2 true negatives. Logistic Regression was followed by KNN (0.5, 0.8685) and Naive Bayes (0.0, 0.8685). This indicates that  Logistic Regression does the best job in predicting cervical cancer diagnoses when considering all features. In the context of this research, incorrect predictions imply that at least some features are not being given proper weight, so interpretation of which features are most important may be incorrect and mislead patients and medical specialists. An issue with all the models is that they suffered from the class imbalance in the target variable, which left them with little training data to learn from. The models may struggle to make positive predictions because they had fewer examples to learn from, which could impact the accuracy in deployment.


Results

Looking at the Logistic Regression model, the features that carry the most importance in predicting sale price are Num of pregnancies, Number of sexual partners, DX:HPV, and IUD (years) (Figure 9). DX:HPV and IUD (years) both hold a direct relationship with DX:Cancer, meaning that, with all other features held constant, an increase in the variable is predicted to increase the probability of a cervical cancer diagnosis. In the case of DX:HPV, a patient with a HPV diagnosis has a higher probability of cervical cancer than one without. Num of pregnancies and Number of sexual partners have an indirect relationship with Dx:Cancer, meaning that the higher a value for the feature, the lower the predicted probability of cervical cancer. 


These are areas that patients could place importance on in their future decisions, if they are trying to lower the probability of a cervical cancer diagnosis. Overall, the features with positive impacts are places that a patient could use caution; limiting their smoking, for instance. The features with negative impacts are places where an increase would theoretically decrease chances of cervical cancer; like an increase in the number of pregnancies.


In the context of our research question, these results matter as they help provide information to patients who are either trying to lower their chances of cervical cancer or determine their baseline. If people know which variables hold the most importance in predicting cervical cancer diagnosis, they can apply that to their own situation and identify qualities of their lives that have an impact. Patients know both which areas they can make changes in and a baseline for their own situation.  In many areas, people to do not have access to testing or even information about cervical cancer. By providing a way to estimates ones own condition, communities can gain more insights. 


Reflection

In regard to ethical considerations, the project holds significant potential for improving health insights in low-resource areas where cervical cancer mortality remains high. By identifying key predictors, the model can serve as a vital tool for people to evaluate their own situation, particularly if testing is not immediately available to them. However, several ethical considerations and limitations must be thought about.


With the dataset being from a specific geographic region, this may limit the ability for the model to be generalized to other communities, as it may not be as accurate for areas it has not seen information on.  Additionally, defining what variables mean for interpretations assumes that the definition used when collecting information matches our own assumptions, which are colored by our experience.


The dataset originates from a hospital and only includes individuals with a means of transportation to the hospital and may exclude those with limited transportation or who lack the means to afford treatment. Since we do not know the socioeconomic or community demographics of patients, we cannot say that this dataset represents a broad category of people or generalize the model to a large group.


Cost of errors must also be considered when using this model. High false positive rates could overwhelm healthcare systems such as hospitals, particularly in smaller more rural areas. We must also be concerned about false negatives as they hold significant harm in patients and their health. False negatives would tell patients they are not at risk for cervical cancer while in reality they are and could cause harm to patient health if they go without getting treated. With regards to interpretability versus accuracy, it does not matter if our model is accurate if patients are not able to understand the workings of the model; how it got to those conclusions, and what it means for them. It is important that patients do not blindly trust the results and instead have a firm understanding about how they are classified so that they may make meaningful decisions to improve their life.


A large part of healthcare ethics involves privacy concerns regarding patients' data, and sensitive information. A large part of healthcare ethics involves privacy concerns regarding patients' data, and sensitive information. So, we removed Age from the dataset.


Visualizations

![Figure 1: heatmap with all “age”  and “first sexual intercourse”](.github/Visualization1-may5.avif)

Figure 1: heatmap with all “age”  and “first sexual intercourse”

![Figure 2: heatmap with the new variable “time since first sexual intercourse"](Figure2may5.avif)

Figure 2: heatmap with the new variable “time since first sexual intercourse"

![Figure 3: Table indicating the recall and log loss for each model](figure3may5.avif)

Figure 3: Table indicating the recall and log loss for each model

![Figure 4: Confusion matrix for model 1: Logistic Regression](figure4may5.avif)

Figure 4: Confusion matrix for model 1: Logistic Regression

![Figure 5: Confusion matrix for model 2: KNN](figure5may5.avif)

Figure 5: Confusion matrix for model 2: KNN

![Figure 6: Confusion matrix for model 3: Naive Bayes](figure6may5.avif)

Figure 6: Confusion matrix for model 3: Naive Bayes

![Figure 7: Feature Importance for model 1, Logistic regression. The further positive a variable is from one, the more impact it has.](figure7may5.avif)

Figure 7: Feature Importance for model 1, Logistic regression. The further positive a variable is from one, the more impact it has.
