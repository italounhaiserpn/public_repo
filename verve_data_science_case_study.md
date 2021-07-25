# Verve Data Science Case Study #

Name: Ítalo Robério Haga Unhaiser
Date: 25/07/2021

Instructions for the case study are available [here][link1].


## Tasks:
> 1 - Imagine that you were asked to use this dataset to build a classification model, with gender as the target. Look at the information we have given you and identify 3-5 potential problems you can see with the provided dataset that might make building a classification model difficult.

> 2 - Describe briefly how you would find the features that are likely to be the most important for your model.

> 3 - Identify which model you would try first, and at least one advantage and disadvantage of this choice.

> 4 - Write up your findings in a Markdown document.

> 5 - Create a new Github repo and commit your Markdown document there.

## Solution:

Analyzing the given overview of the dataset, it’s possible to see that we have some missing data for device_name, app category, and ad category. For device_name it’s missing 59.10% of the values, 1.78% for the app category, and 1.78% for the ad category. However, it’s not possible to know the number of rows across the 3700 of the dataset that is missing more than one column of data.

The frequency distribution for app category can make it difficult to build a classification model, as we have more than 54% of the registers in the dataset as News. The frequency of the other app categories is low. And we also need to keep in mind that NaN frequency is higher than 5 app categories.

According to the description of the case study, we know that “_Each row of data represents an event, where a user is shown an ad during an app. Users can have multiple events for the same app session, as each time they are shown an ad while using the app it is logged as a new event_”. Based on that, the column interaction_with_app may be a problem for our model because it can have inaccurate data. For example, the user_id 100 is using the app_id 123 and is shown the ad A when the app is open by 1 minute, the user closes the ad and continues using the app. It would create a register in the dataset with interaction_with_app = 1. After 2 minutes the user is shown the ad B, it would also create a register in the dataset but with interaction_with_app = 3. Both events happened within the same session but generated different registers for the column interaction_with_app. It means that if aggregated by app_id, the total interaction_with_app will be inflating the total time for situations as described above, which may cause inaccurate data.

Based on the potential problems of the device_name and interaction_with_app, I wouldn’t consider these two features in the model. 

I would use the user_id, app_id, app category (even with the frequency issue mentioned above), ad category, and click.

For each user_id we can have different registers in the dataset, and the iteration across the app_id, app_category, ad_category, and click would be used by the model to identify patterns for each user and across all the user_id’s, in order to get more accuracy on predicting the behavior and the patterns to have the correct outcome (gender).

Taking into consideration the dataset and the features mentioned above and the fact that we have a binary classification, I would first try a Decision Tree model to predict the gender based on the provided data. 

The Decision Tree algorithm would have some advantages like it can be used when we have missing values in the dataset (in this case, we saw that we have missing values (NaN) for app category and ad category) and it’s an intuitive and easy to explain model for stakeholders. On the other hand, the Decision Tree model is sensitive to small changes in the dataset, it can cause large changes in the structure and also instability.



[link1]: <https://gist.github.com/t-redactyl/90837921265451bf519ce81d96b62462>
