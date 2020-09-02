# Udacity-Sparkify

## Project Overview

This project is about Sparkify digital music streaming like Spotify and Pandora. They have many users that stream their favorite songs through the offered service every day using the free-tier that play advertisements between the songs or using the premium subscription model where they stream music as free but pay a monthly flat rate. <br>
Users can downgrade, upgrade, or cancel their service at any time. So is crucial to make sure the users love the service. <br>
There are some events triggered by user use, like play song, logging out, liking a song with thumbs up, hearing an add, downgrade their service, etc. These events generate data. All these data contains the key insights for keeping the users satisfied and using their service.<br>
So the goal on these project is to predict which users are at risk to churn, either downgrading from premium to free tier or canceling their service altogether.<br>
If the identification of these users were accurate enough before they leave, some marketing offers could be send to prevent the churn. <br>
To complete this project it was provided a large dataset that contains all events described above.
Here we use a tiny subset (128MB) of the full dataset available (12GB).<br>


## Problem Statement

Problem simple definition:
>Predict which users are at risk to churn, either downgrading from premium to free tier or canceling their service altogether.

The steps to solve this problem is:
 - Load data
 - Explore and Clean data
 - Create features
 - Build Models
 - Predict churn
 
 To guide myself on this journey of exploring the data, I create some questions at the beginning of the notebook regarding the data. These questions should take into account the final target (ML) and the users segmentation. For instance:
 
 - How can we defined a user churn?
I selected using the Cancellation Confirmation events to define the churn, which happen for both paid and free users.

![churn](/image/churn_def.png))

 - Is there any demographic patter?

We can say that male gender seems to be more likely to churn than womens.
![gender](/image/gender.png))

 - Is there a numerical difference between the number of songs played between churn and non-churn users?
Average number of songs played for churn users are 699.8846153846154 and for non-churn users are 1108.1734104046243

 - The number of days since the registration can be a significant factor to the churn users?
If the past days since registration are higher than 140 the chance of the user churn falls dramatically. That is a very important feature.
![pdays](/image/daysp.png))

 - Can we ensure that if the user is liking a song with thumbs up the chance of churn reduce?
The "Thumbs up", "Add Playlist" and "Add Friend" seems to have less churn users rate.
![pages](/image/pages.png))
 It may happen that not all questions get answers, but the point is to get some insights.<br>
 
 So, after these analysis and insights, it is time to model! Our problem is a classification problem, so we will use a supervised machine learning algorithm.  
 
 For that part will use three models that were quote at the class. They are:
  - Linear Regression (lr)
  - Random Forests (rf)
  - Gradient-Boosted Tree (gbt)
  - Support Vector Machines (svm)
 
## Metrics
 To evaluete and determine the winning model, we will based on validation accuracy since the churned users are a fairly small subset, we will be using F1 score as the metric to optimize. If you want to know more about which metric choose, you can check here. 
 
## Conclusion

### Reflection

This project provided an opportunity to familiarize myself with loading, analyzing, cleaning and predicting using big data. It was very challenging, but joyfull. <br>

One of the most challenging points was getting used to the syntax. As similar as it was to python, it took me a while to get used to and understand what I was doing. <br>
 
It was amazing learn how to manipulate large and realistic datasets using Spark to engineer relevant features for predicting churn and how to use Spark MLlib to build machine learning models, far beyond what could be done with non-distributed technologies.


### Improvement 

To improve the process many thing can be made, like balance the class predict. This process could be done using oversampling, but it has do be done carefully. A common mistake when oversampling is applying the oversample before the cross validation. The problem of this approach is that at some point the training and validation set contain the same sample, resulting in overfitting and misleading results. <br>

The right way is shown in the figure above. We need to do the oversampling after the cross validation, in order to avoid using the same data for training and validation. This way we avoid overfitting and get reliable results.
It is possible to know more in: https://www.marcoaltini.com/blog/dealing-with-imbalanced-data-undersampling-oversampling-and-proper-cross-validation.<br>

Another point is to treat the skewness of the features. Many models make assumptions about the features being normally distributed, so transforming our features into more normal features can boost our predictive ability.The model based on tree decisions are not too senstive for skewness but it can be improved. 
