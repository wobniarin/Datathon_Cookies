<img src="https://bit.ly/2VnXWr2" alt="Ironhack Logo" width="100"/>

# Cookies Datathon - Can we predict the best quality cookie? 
*[Fabia Hohne, Laurent Guerguy and Íngrid Munné Collado]*

*[Data Analytics June 2019]*

![Cookies](../Datathon_Cookies/cookies.jpg)

## Content
- [Project Description](#project-description)
- [Hypotheses / Questions](#hypotheses-/-questions)
- [Dataset](#dataset)
- [Cleaning](#cleaning)
- [Analysis](#analysis)
- [Model Training and Evaluation](#model-training-and-evaluation)
- [Conclusion](#conclusion)
- [Future Work](#future-work)
- [Workflow](#workflow)
- [Organization](#organization)
- [Links](#links)

<a name="project-description"></a>

## Project Description
We are data scientist at Cookie Flea and we want to have the best cookies in the world! For this reason we are implementing a model on ML to predict the recipe that will give us the best quality cookies! 

<a name="hypotheses-/-questions"></a>

## Hypotheses / Questions
At the very begninng we think that the best quality cookies will be those that contain chocolate, that are crunchy and the aesthetics of the cookie itself. 

Considering the Codebook, our first hypotheses to a best cookie are : 
* sugar to flour ratio 
* bake temp 
* mixings 
* butter type 
* crunch factor 

The main questions we want to answer are: 

* Which are the main ingredients that gives you the best quality cookie? 
* Are higher calories a synomym of a best quality cookie? 

<a name="dataset"></a>

## Dataset
The data we are looking in order to win the cookie contest is a dataset with 16 columns that are our features or cookie elements/ingredients, and 5198 rows, that are different cookies  that have been studied. This dataset has been bought to a company that analyses several products. 

The codebook for the data can be found in the repo under [data](../Data/Codebook.pdf). 


<a name="cleaning"></a>

## Cleaning
Following steps were followed when cleaning the data:
#### 1. Analysing shape, data types, column names. 
In this step we define our target, `quality`, and we identify what data is categorical. 

#### 2. Looking at the basic statistics using the `describe` function. 
This will allow us to get an initial idear of the data distribution, informaiton on outliers, and the range of data.

#### 3. Checking for NaNs using `isnull().sum()` and `isnull().sum()/len(df)` to check the proportion of missing values.
At this point we came to following conclusions andactions: 
  
  - As we can have cookies with no added extras, we will not drop that type, instead we will replace the nan with a "No mixins" label. 
  
   - For the sugar index nans and the temperature nans, as the proportion of data is so low, we will jsut drop them. Added to this, cookies with no bake time are not useful as bake time is a very important factor to the cookie. 

#### 4. Checking correlations and distributions
We did this using a simple `sns.pairplot()` and a `sns.heatmap`.
Looking at these graphs, we quickly see that there are a few outliers that need to be considered and that we have some highly skewed distributions. We also see that there are some columns where the data is not useful for our anlysis:
   - Density (density 5 is not realisitc, all other values do not have enough variation for the variable to be useful for a comparison)
   - Diameter (mostly the diameters are very similar)
   - Aesthetic appeal (we do not know the range of the scores, therefore using this data can lead to future missinterpretations. Added to this, most of the data is within the score = 3 group, with only a few observations at 4).
   
We also see below, that we have no significant correlations which will allow us to remove any non-significant variables for a ML model. 

#### 5. Outlier removal
to remove the outliers we selected values whose z score was over 3 and removed them.
To do this, we first separated numerical and categorical values, then we removed the observations, and we merged the categorical data back in. 

This resulted in an overall improvement in our data. However, we were not quite happy with some specific variables, such as bake temp and calories as they did not fulfill our expectations. However, we have to keep in mind that we generalize our analysis and we do not want it to be bias. Therefore we will use the same process to remove outliers for all of our data, and not change any specific column according to our expectations.


<a name="analysis"></a>

## Analysis
* Overview the general steps you will go through to analyze your data in order to test your hypothesis.
* Document each step of your data exploration and analysis.
* Include charts to demonstrate the effect of your work. 
* If you use ML in your final project, describe your feature selection process.

#### 1. Replacing categorical values. 
    1.1 Butter type - melted or diced
    As this variable had only two choices, we replaced this by [0,1]
    1.2. Mixins - list
    For mixins, we had a list of different ingredients in a str. format. For this, we created new columns for each ingredient and filled the observation with a 0 or 1 depending on weather the recipe had the ingredient or not. 
    
#### 2. Our models
Our initial thoguhts on choosing a model was to classify our results into categories (1 to 11).

After running this option and not getting the desired results, we carried out a OLS method to lower the dimensionality of our data (decision trees don't work well with many vairbales). Through this, we realised that our R2 value was relatively goos (0.99), and therefore we shluld consider a Linear Regression. 

This path was the one we took to complete the predicitons on the final test data. 

#### 3. Feature selection process
To select our features we used OLS. 


<a name="model-training-and-evaluation"></a>

## Model Training and Evaluation
*Include this section only if you chose to include ML in your project.*
* Describe how you trained your model, the results you obtained, and how you evaluated those results.

For both methods we first defined our model, then split our data, fit and looked at the metrics (accuracy and R2).


#### 1. Decision tree
Hyperparameters we looked at:
- max depth
- min number of splits


#### 2. Linear Regression 
OLS for feature selection and roundign of values. 

<a name="conclusion"></a>



<a name="future-work"></a>

## Future Work
Future work on the machine learning model is needed. We could not find the accuracy rate we wished for, so we hope that with further knowledge on the topic we might rise this metric. 

<a name="workflow"></a>

## Workflow
1. Trello Organization 
2. Project initialization: .gitignore, database downloading, repository creation, collaborators added to the repo and README.md file.
3. Hypotheses writing. 
4. Data Cleaning
5. Basic Statistics 
6. Model and metric selection 
7. Model development and Model Evaluation
8. Project Review: Explanations and Conclusions 
9. Slides 
10. Presentation

<a name="organization"></a>

## Organization
We are working as team of data scientists at Cookie Flea. To achieve our goals we have structured the workflow as mentioned aboved. We are using Trello, Github, Jupyter Notebooks and Google Slides to achieve our objectives. The repo is structured as follows: 
- Data: Folder with the raw data csv and the cleaned dataset 
- Jupyter_Notebooks: Folder with two Jupyter Notebooks: one for data cleaning and the other one for the model development 

<a name="links"></a>

## Links
Find below the links to the repository, Slides and Trello in case more information is required. 
[Repository](https://github.com/wobniarin/Datathon_Cookies)  
[Slides](https://docs.google.com/presentation/d/1-NY-4s4Ak7lt6x99wn2Aeqy_UIpj6x4ImgvdTSnVz78/edit?usp=sharing)  
[Trello](https://trello.com/invite/b/9vzBesYV/5a6d54cc3902bbda4820edf89cdaff26/hackathlon)  
