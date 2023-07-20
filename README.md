# Machine Learning and Real Estate Forecasting

# Table of Contents
<a id='table_of_contents'></a><br>
[Problem Statement](#section_1)<br>
[Executive Summary](#section_2)<br>
[Models and Conclusion](#section_3)<br>
[Data Dictionary](#section_4)<br>
[Datasets and Libraries Used](#section_5)<br>

<a id='section_1'></a>
# Problem Statement
Many of us believe that homeownership is a natural thing we all should aspire to. It is a sign that our hard work has paid off. It’s our way of saying to the world that we made it. 

Unfortunately, this dream is becoming more fantasy than reality for millennials. <a href="https://www.inc.com/minda-zetlin/millennials-homeownership-student-debt-down-payment-apartment-list-study.html"> While 89% of millennials want to own a home, it will take a staggering <i>two decades</i> before 67% of them can afford one.</a>

Still, even with the odds against them, many millennials are pursuing homeownership. Sadly, even if millennials do somehow overcome those odds and purchase a home, many still aren’t finding the security they hoped they’d find through owning a home.

<a href="https://www.usatoday.com/story/money/2021/06/11/millennials-facing-financial-and-physical-regrets-after-buying-homes/7594826002/">Two-thirds of millennials have home-buying regrets</a> and are more likely than the generations before them to think <a href="https://www.bankrate.com/real-estate/homebuyer-regret-survey-may-2021/">a home isn’t a good investment or that they overpaid for their house.</a> 

That’s where we at MyFirstHome come in. 

Our goal is simple, provide millennial homebuyers with an easy-to-use tool that answers the question: how much should a home cost?

Not how much a realtor says a house should cost.

Not how much a house with a porch you really like should cost.

And not how much a house should cost because one two blocks sold $60K above asking.

Our hope is by doing this we will help them make better purchasing decisions in the future.

<a id='section_2'></a>
# Executive Summary
[(Back to table of contents)](#table_of_contents)<br>
Since this is more a labor of love for our fellow millennials, not profit, we wanted to do this with easily accessible information. We aim to have a turnkey process that can be used across North America.

And so, for our test case, we've picked Ames, Iowa.

Why Ames?

1. The data is publicly available.<br><br>
2. With a population of around 66,000, there is enough data to work for a test case, but not so much that we’d be overwhelmed.<br><br>
3. Its “ridiculously friendly people” helped to lift it to <a href="https://www.amestrib.com/story/news/2020/10/16/ames-ranked-top-15-places-live/3678012001/">a top 15 rating in Livability.com’s Top 100 Best Places to Live</a>, so it’s a place we could actually see millennials living in.

The data set we worked with had 80 features and 2051 observations.

You can read an explanation of all the original features <a href="http://jse.amstat.org/v19n3/decock/DataDocumentation.txt">here</a>.

While it was nice to have 80 features to work with, our goal, above all else, is simplicity. 

This is a labor of love for our fellow millennials, with an aim to help, not profit from them. We are not looking to charge exorbitant subscription fees or depend heavily on outside investment. 

Since that is the case, we wanted to create a model that focused on essential features with information that is easy to obtain and does not depend on a “special sauce” that might not be easily reproducible from one location to another.

We tried four general types of models:
- Linear Regression
- Lasso
- Ridge
- KNN

While the results varied from model to model, we generally saw a final R2 score of 91% to 92%.

Well, outside of our attempts with KNN, which on average had a final R2 score that was 6-7% lower than the other 3 model types we tested.

<a id='section_3'></a>
# Models
[(Back to table of contents)](#table_of_contents)<br>
|Model|Parameters|CV Score|Training Score|Test Score|
|:---|:---|:---|:---|:---|
|**Linear Regression**|Polynomial Features(include_bias=False), Standard Scaler, poly degree: 2, lr fit intercept: True|88.2%|90.5%|91.4%|
|**Lasso**|Polynomial Features(include_bias=False), Standard Scaler, LassoCV, poly degree: 2, lasso eps: 0.001,  lasso max iter: 1000, lasso n_alphas: 100, lasso normalize: False, lasso tol: 0.0001|88.9%|89.7%|92.1%|
|**Ridge**|Polynomial Features(include_bias=False), Standard Scaler, RidgeCV, poly degree: 2, poly interaction_only: False, ridge fit intercept: True|88.9%|89.7%|92.1%|
|**KNN**|Polynomial Features(include_bias=False), Standard Scaler, KNeighborsClassifier, poly degree: 2, knn metric: minkowski, knn n_neighbors: 5, knn p: 2, knn weights: uniform|82.8%|88.8%|85.0%|

Since Ridge performed slightly better than Lasso, that is the model we chose in the end.

Our final model's results:

![Ridge: Actual vs Predicted](https://i.imgur.com/Wc2ugAO.png)

While our model struggles a bit at higher price points, since millennials on average have
 <a href="https://www.cnbc.com/2021/11/09/how-much-debt-millennials-have-on-average.html">$87,448</a>, it's not something we are particularly concerned with, most simply do not have the budget for those price points.
 
What's more, while our tool can be a useful guide, once you get to those price points we would advised you to seek out more specialized help.

<a id='section_4'></a>
# Data Dictionary
[(Back to table of contents)](#table_of_contents)<br>

|Feature|Type|Engineerd|Description|
|:---|:---|:---|:---|
|**bsmt_exposure**|*ordinal*|No|Refers to walkout or garden level walls (range:0-4)|
|**bsmt_quality**|*ordinal*|No|Evaluates the general condition of the basement (range: 0-5)|
|**bsmtfin_type_1**|*ordinal*|No|Rating of basement finished area (range: 0-6)|
|**central_air**|*nominal*|No|Whether a property has central air conditioning (range: 0-1)|
|**exter_qual**|*ordinal*|No|Evaluates the quality of the material on the exterior (range: 1-5)|
|**fireplace_qu**|*ordinal*|No|Evaluates fireplace quality (range: 0-5)|
|**garage_finish**|*ordinal*|No|Evaluates the interior finish of the garage (range: 0-3)|
|**garage_qual**|*ordinal*|No|Evaluates the quality of the garage (range: 0-5)|
|**heating_qc**|*ordinal*|No|Evaluates the quality and condition of the heating (range: 1-5)|
|**kitchen_qual**|*ordinal*|No|Evaluates the quality of the kitchen (range: 1-5)|
|**mas_vnr_type**|*nominal*|No|Masonry veneer type (range: 1-5)|
|**overall_qual**|*ordinal*|No|Rates the overall material and finish of the house (range: 1-10)|
|**paved_drive**|*ordinal*|No|Whether a property has a paved driveway (range: 0-1)|
|**total_sf**|*float*|Yes|Combined square footage of 1st floor, 2nd floor, basement area, open porch area, and wood deck area|

<a id='section_5'></a>
# Datasets and Libraries Used
[(Back to table of contents)](#table_of_contents)<br>

<b>Datasets:</b> 
- <a href="https://www.kaggle.com/competitions/dsi-us-11-project-2-regression-challenge/data">Ames Housing Data</a>

<b>Libraries:</b> 
matplotlib, numpy, pandas, seaborn, and sklearn.
