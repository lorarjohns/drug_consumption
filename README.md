![image](splash.png)

## Do personality traits 'predict' drug use?

+ _The Five Factor Model of personality and evaluation of drug consumption risk_, Fehrman et al. [link](https://arxiv.org/abs/1506.06297)
+ For this analysis, an "active user":
  + Used Heroin, Methadone, Crack, or Cocaine
  + Within the last year


+ This definition underlies the target variable. Why?

  + Highest risk population (real-world)
  + Create a reasonable target variable without introducing confusion (pragmatic)

## Models

![heatmap](heatmap.png)
_heatmap of features_


![drug use](drug_use.png)
_percentage of users per group_

1. Multinomial Bayes
2. Logistic regression
3. K-nearest neighbors

![matrix](confusion.png)

_Confusion matrix_

![many_k](f1.png)
_Multiple K testing_


4. Support vector classifier

5. Random forest
![tree_reg](tree_reg0.png)
## Takeaways

+ In all models, ecstasy was the top discriminator (followed by benzos and legal highs)
+ Accuracy alone isn't enough
+ Interrogate the underlying research
+ The purpose to which you put your data matters
+ Examine bias (in the data and the people)
