# Predicting House Prices for Homes in Aimes, IA

Below is the Order and Organization of this Summary:
1. Background
2. Extended Problem Statement and Explanation of Notebooks
3. EDA Data Cleaning Notebook
4. Further EDA, Cleaning, Preprocessing and Modeling for each model
5. Evaluation of Models 
6. Conclusions and Reccomendations

## Background

* Millenial generation and housing.
    * There has been a near constant discussion of the Millenial generation and husing; especially around Millenials struggles to own a home.
    * As this Denver Post article describes the average colorado home price has increased over % 450 in the last 31 years ([*Source*](https://www.denverpost.com/2021/07/04/millennials-debt-wealth-housing-health-care-colorado/)) this price increase coupled with the high student debt many Millenials have has dramatically impacted the rate of home ownership for Millenials.
    * In addition to student debt and rising house prices Millenials have also had to live through two recessions. As this article from business insider describes these additional issues coupled with a housing shortage are limiting Millenials opportunitities to own a home ([*Source*](https://www.businessinsider.com/housing-market-forecast-millennials-buying-homes-crisis-2021-4)).
* These issues can also be seen in the number of hits for 'millenials and housing':
    * Over 10 million hits overall
    * Over 200 thousand news articles
    
## Extended Problem Statement and Notebook Explanations

Millenials and housing. That’s it, that’s the problem statement for this project…

Okay maybe I should give a little more context and background than just “Millenials and housing.”

As described in the background Millenials have a low home ownership rate. Having to rent instead of paying into a mortgage can negatively impact Millenials current and future finances as they may be paying more than a mortgage and not seeing any return on those payments. Using linear regression I will attempt to identify important features that predict a homes saleprice in the Ames, IA dataset. I will conduct a Naive or baseline model, a common real estate features model, and a complex feature model. By examing which features are most in the complext model I may be able to illuminate high value features that aren't neccessary for Millenial or other first-time home buyers. Success in the context of this project will be defined as finding at least one impactful feature that is not in the naive or common features model.

To Further elaborate on the models in this project: 
1. First a naive model was completed as a sort of “Quick & Dirty” first attempt at predicting home prices. I had been struggling a bit with this project and finally set a time limit of 1 hour to complete a Naive Model. The first modeling notebook covers this "Quick and Dirty" model. 
2. Secondly, I completed a model that was based on the most commonly available features when searching for homes on two common real estate sites (Zillow and MLS Real estate). The Common Features Model notebook explains what features were common between the real estate sites and then conducts a linear regression using those common features.
3. The final notebook looks at what I've termed as the complex feature model. In this model I used a "Kitchen Sink" approach to throw as many variables as I could at predicting a homes sale price. This notebook features a simple linear regression model, a Ridge model, and a Lasso model. The "Kitchen Sink" approach was used to get as many additional features as possible to compare against those in the naive and common feature models. 

###Success Definition

These questions helped to guide my Definition of Success:
* What are features that lead to an increase in the overall price?
* Are these features that are necessary for a first-time buyer
Success in the context of this project will be defined as finding at least one impactful feature that is not in the naive or common features model. Furthermore success will also be seen as actionable conclusions from this project that can assist Millenials and other first-time home buyers. 

## EDA and Data Cleaning Notebook
The initial Data Cleaning and addressing of Null Values was conducted in the EDA Data Clean Notebook. Much of this process involved checking and double checking columns that contained null values against the explanation provided in the Ames, IA data dictionary. While working through this process I also created a [google doc](https://docs.google.com/document/d/1uThpvNZ_xxrwrA9rXgYtPUprQRT2oCxLcL_c94uW4Lk/edit?usp=sharing) that organized the nominal and ordinal data along with how they were encoded from the data dictionary. Using this information and the data dictionaries explanations I worked through filling null values. I then dropped 2 rows that were considered outliers based on text at the end of the data dictionary. Finally I resaved the data frame as a cleaner version of the train data.

Further EDA was conducted in the other notebooks, however following the initial EDA I remained hopeful that my success definition would be met.

## Further EDA, Cleaning, Preprocessing and Modeling for each model

### Naive Model
The initial Naive Model was conpleted in a shortened time frame to ensure I had a model submitted to Kaggle. Notes in this section relating to Preprocessing and checking distributions were conducted after the intial model was run. This was not good practice on my part. Future Model workflows will need to include the checking of distribnutions and summaries prior to modeling. With that said, I got somewhat lucky that four terms in the model did have to varying degrees a linear relationship with saleprice.

In the initial model I moved straight to using a pipeline to cast features that are nominal or ordinal to numbers to be used in the linear model. I then used a training and testing to split the data to then compare against. The outcomes of this linear model led to the following scores:
* r2 scores (or amount of variance in the model explained by the features)
    * Train .832
    * Test .805
    * Interpretation as a somewhat overfit, but overall good start for the project.
* RMSE scores (or number in dollars that the model was off by when predicting sale price):
    * Train: 33,122.28
    * Test : 32,729.8
    * Interpretaion: interestingly this model did slightlty better on the test data than the training data, but overall it ws off by about 33,000 dolars.

### Common Features Model
The common features model examined the search features common between Zillow and MLS Real Estate two large real estate search sites. These common features were:
1. Number of Bedrooms
2. Number of Bathrooms
3. Square Feet
4. Lot Size
5. Property Type:
    * Houses, Townhouses/Condos/Co-Op, Multi-Family, lots/land, rentals

Similar to the Naive model this model was also somewhat rushed and didn't involve very much prechecking of the data. Only a simple heat map and pairplot of correlations were used. To get the property type features a one hot encoding or dummy variable function was used to get a column for each of the property types in the dataset, one of these columns (ms_subclass_150) was eventually dropped due to iussues modeling on the testing dataframe. 

Following the brief dummying and a bit of extra cleaning the modeling was conducted with the following results
* r2 scores (or amount of variance in the model explained by the features)
    * Train .777
    * Test .734
    * Interpretation this is a fair bit worse than the naive model and alos much more overfit.
* RMSE scores (or number in dollars that the model was off by when predicting sale price):
    * Train: 37,948.81
    * Test : 39,166.69
    * Interpretaion: Much worse model on predicting sale price, but this was intended as more of a check against the search sites not as an improvement.

### Complex features Model
Conducted a Kitchen Sink approach that involved Dummying multiple variables and also casting to nominal and ordinal features. Ended up with a very large dataframe. Initial linear model was not great, so I moved to used regularized models starting with Ridge and than lasso. The Lasso model proved the best with the following scores:

* r2 scores (or amount of variance in the model explained by the features)
    * Train .923
    * Test .893
    * Interpretation this is a really big improvement over the other two models. Its is slightly underfit to the testing data, but still much better overall.
* RMSE scores (or number in dollars that the model was off by when predicting sale price):
    * Train: 22,649.01
    * Test : 24,240.98
    * Interpretaion: Again a vast improvement over the other two models finally broke into under 30K at only being off by 24,000 dollars.

Finally I analyzed the Coefficients from the Lasso Model and found that there were 68 positive coefficients, 19 of which that were head and shoulders above the rest. With the most important being features common to the other models:
1. Total Square Footage of the home
1. Varying Neighborhood Locations for the home
1. Quality of important parts of the home
* Kitchen most important
* Basement and the garage are next most important
* Having a Brick Exterior
1. Size of the lot
1. Number of rooms in the home
1. Suburban location (Cul De Sac location or A Floating Village Residential Area)

However there were two other high level features that were not in the previous models:
1. Screen Porch
2. Fireplace


## Conclusions and Reccomendations

The most important features from these models were total square footage of the home, neighborhood location and zoning type (residential and cul de sac best), quality of important parts of the home (Kitchen, Brick Exterior, and Garage), and the number of rooms (similar to overall size). Many of these features are common between the three models. 

Two important features that were not common to the first two models:
1. Screen Porch (and its area)
2. Fireplace(s)

Based off these features I would reccomend for Millenials and other first-time homebuyers to look for houses that have the common features, but don't have these two and attempt to get and equally good house that may cost less.
