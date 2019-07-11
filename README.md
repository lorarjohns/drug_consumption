![image](splash.png)

## Do personality traits 'predict' drug use?

+ The original study, _The Five Factor Model of personality and evaluation of drug consumption risk_, Fehrman et al. [link](https://arxiv.org/abs/1506.06297), sought to prove that personality traits 'predicted' a person's propensity to become a drug user.

+ For my analysis, the an "active user" is defined as someone who:
  + Used Heroin, Methadone, Crack, or Cocaine
  + Within the last year

+ This definition underlies the target variable. Why?

  + This might be seen as the highest risk population for whom interventions policies be tailored (real-world)
  + It allowed me to create a reasonable target variable without introducing confusion, within the 2-day time span of the code sprint (pragmatic)

## Data Pre-Processing

The data were problematic in several ways that affected the choice of logistic regression. While models such as decision trees might not be as sensitive to some kinds of data eccentricities, logistic regression is, making preprocessing a vital step.

### Checking the distribution of samples

The samples had all been binned already, despite once in their past having been continuous variables. Therefore, some information and precision have already been lost from the set. Additionally, categorizing predictors can lead to a high rate of false positives.

However, binning variables can improve the interpretability of a model, which may be advantageous in this use case, as the interpretability is what I am specifically seeking to challenge. 
Â
Because the data contained several bins with relatively few observations, I created new variables to represent arguably more meaningful groupings of observations along age, education, race, and nationality lines, etc.

I also checked the percentage of samples falling into each bin from CL0 (never used) to CL6 (used within last day) to create meaningful predictors. Many observations clustered around "never" or "recent", with a bump in the middle (for, loosely,  "former user"), a distinction I hoped to capture with feature engineering.

### Data transformation

I created dummy variables and removed the first, because some of my models (that include an intercept term) would be sensitive to the extraneous term (although RandomForests, e.g., would not). 

I scaled the data, which appears to have already been normalized, using min-max scaling, such that all the remaining continuous values would lie between 0 and 1, to eliminate problems with logarithmic calculations.

## Models

![heatmap](heatmap.png)
_heatmap of features_


![drug use](drug_use.png)
_percentage of users per group_

1. Multinomial Bayes

The most basic baseline model I ran was a multinomial Bayes model. 

2. Logistic regression

+ Logistic regression was performed after scaling the data
+ Cross-validation and ROC-AUC metrics of model performance were used to assess accuracy.

3. K-nearest neighbors

![matrix](confusion.png)

_Confusion matrix_

+ The confusion matrix was used to examine the tradeoff between sensitivity and specificity.
+ Many instantiations of KNN were run with differing values of k and plotted to find the one that maximized the 'F1' score measure of accuracy.
+ KNN can be problematic because all the data must be taken into account for training; there is no validation data as in other models. K-fold (or LOO) cross-validation can be used in addition to model iteration count to judge accuracy.

![many_k](f1.png)
_Multiple K testing_


4. Support vector classifier

5. Random forest
![tree_reg](tree_reg0.png)
+ Random forests produced the most accurate model, but it was important to use cross-validation to ensure that the bias-variance tradeoff was not skewing too heavily in favor of overfitting the training data.
+ Tree models can overfit if the depth (i.e., terminal leaves) is permitted to become too deep (or numerous).
+ Gridsearch was used to tune the hyperparameters and k-folds cross-validation used to check the model's performance.

## Takeaways

+ In all tree models, ecstasy was the top discriminator (followed by benzos and legal highs).
+ Accuracy alone isn't enough to evaluate a model's value. Other statistical validation methods must be implemented to account for accuracy versus precision. Depending on the use case, sensitivity or specificity may be more important.
+ Interrogate the underlying research
+ The purpose to which you put your data matters
+ Examine bias (in the data and the people)
