# Concrete_Compressiveness_prediction
In this repository, I have applied linear regression to predict compressiveness of concrete. I have also tested my model if it can work well on unseen data. Along with it, I have measured errors, and found problems that can impact model's performance. Here is how:
Concrete compressive dataset (Taken from kaggle)
The shape of data is:
(1030, 9)

Information about the data:
All these observations are measured in kg/m^3 except age and concrete_compressive_strength.
1. cement
2. blast_furnace_slag (non metallic by product composed of silicates etc) 
3. fly_ash
4. water
5. superplasticizer(without water, it flows easily)
6. coarse_aggregate(larger rock particle = bajri)
7. fine_aggregate(crushed stone)
8. age (in days)
9. concrete_compressive_strength (in mpa)
----------------------------------------------------------------------------------------------------------------------------------------------

Data analysis
1. Checked missing values  =  None
2. Duplicates = yes but it is ok
with slight changes in predictors' concentrations, it changes the response = concrete strength
3. Checked the number of unique values [vary but less unique values mean many values have been repeated as compared to huge 1030 rows dataset].
4. Selected numeric data in columns and described:
blast furnace slag and fly ashes have huge difference in their 20%, 50%, 70% and max than others.
5. Correlation among 2 predictors at a time (no collinearity between each 2 individual found)
6. Relation btw target and predictors individually (Remember weak individual can still help to predict response when used with others)
cement and concrete = strong rlsp
blast furnace and concrete = moderate
fly ash vs concrete = weak
water vs concrete = weak
superplasticizer vs concrete = strong
coarse aggregate vs concrete= weak
fine aggregate vs concrete= better than weak
age vs concrete = strong
7. Outliers
| Column                        | Possible outliers |
| ----------------------------- | ----------------: |
| cement                        |                 0 |
_-----------------------------------------------------
| blast_furnace_slag            |                 2 |
--------------------------------------------------------
| fly_ash                       |                 0 |
-------------------------------------------------------
| water                         |                 9 |
--------------------------------------------------------------
| superplasticizer              |                10 |
-----------------------------------------------------
| coarse_aggregate              |                 0 |
------------------------------------------------------------
| fine_aggregate                |                 5 |
-----------------------------------------------------------
| age                           |                59 |
-----------------------------------------------------------
| concrete_compressive_strength |                 4 |

Have no reason to delete or do anything with outliers 

_____________________________________________________________________________________________________________________

Notes:
[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
[2] The condition number is large, 1.06e+05. This might indicate that there are
strong multicollinearity or other numerical problems.

1. Look for multicollinearity if it is handle it..
applied VIF and it showed that there is strong multicollinearity in some 
Possible solutions are:
1. remove if for example 2 columns have same effect ...like increase of each increase response with same extent. that variable is called highly reductant variable. 
2. Combine highly related predictors. In domain knowledge is required. 
3. Use independent data (i cannot coz the dataset is already taken from kaggle)
4. Use ridge regression (not required yet)
5. Use test spilt data to test


Multicollinearity was strong in water, coarse aggregate and fine aggregate. So, checked the impact by removing each one by one.

with all predictors
training r^2: 0.6105238047649741
testing r^2: 0.6275531792314848
training rmse: 10.518787334819802
testing rmse: 9.796475901624362
training mae: 8.33010876650668
testing mae: 7.745559243921431

_-----------------------------------------------------
without water
training r^2: 0.5613481663149011
testing r^2: 0.5326515464747873
rmse of training data:  11.163109633375614
rmse of testing data: 10.973827868608877
mse of training data: 8.828601292956698
mse of testing data: 8.772522659915847
------------------------------------------------------
without coarse aggregate
training r^2: 0.589749525369337
testing r^2: 0.585791128734759
rmse of training data:  10.79567399798901
rmse of testing data: 10.331120731331403
mse of training data: 8.668041507605809
mse of testing data: 8.324030381507802
----------------------------------------------------
without fine aggregate
training r^2: 0.5868123128341713
testing r^2: 0.5673059074037722
rmse of training data:  10.834251205409274
rmse of testing data: 10.559132066109031
mse of training data: 8.642214082983882
mse of testing data: 8.488909373275927

Removing any of them can reduce model's performance. So, I have kept them.
