## A-Project overview and Research Question

Preparing meals at home is an important part of household food behavior because it may be related to how families allocate their food spending. Households differ in how often they prepare dinner at home, how often they purchase food for home consumption, and how often they obtain food away from home. Examining these patterns can help identify whether more frequent home meal preparation is associated with differences in household food expenditures.
This project uses the U.S. Department of Agriculture (USDA) FoodAPS data to examine the relationship between home dinner preparation and recorded household food spending. Because FoodAPS is observational survey data, the analysis focuses on association rather than claiming that preparing dinner at home causes food spending to increase or decrease. A basic linear regression model will be used on the full cleaned analysis dataset; no train/test split will be performed because the goal is to describe and quantify the linear relationship rather than build a predictive model for new households.

*Research Question: How is the frequency of preparing dinner at home associated with household food spending among U.S. households?*

The main explanatory variable is dinners_prepared_at_home (renamed from the original FoodAPS variable nmealshome), which records the number of times food was prepared for dinner at home during the past 7 days. The main outcome is total_food_spending, a project-created variable formed by combining food_at_home_spending (FAH) and food_away_from_home_spending (FAFH) for each household.

# B- Dataset Description (FoodAPS)
The National Household Food Acquisition and Purchase Survey (FoodAPS) is a USDA survey designed to provide detailed information about the foods U.S. households acquire, where those foods are obtained, how much is paid, and selected household characteristics. The public-use data are organized into multiple linked CSV files rather than one single table. The original household identifier hhnum is renamed household_id in this project so the merged analysis dataset is easier to understand.

For this project, only three FoodAPS CSV files are required. Using these three files keeps the analysis focused on the research question and avoids adding variables that are not needed for the basic linear regression.

# B.1 *faps_household_puf.csv - Main household dataset*
This file is the foundation of the analysis because it contains one household-level record and the key home-meal variable. For readability, nmealshome is renamed dinners_prepared_at_home, hhsize is renamed household_size, inchhavg_r is renamed monthly_household_income, ndinnersouthh is renamed dinners_eaten_out, and hhnum is renamed household_id.
# B.2. *faps_fahevent_puf.csv - Food-at-home (FAH) events*
This file contains food-at-home acquisition events, such as foods obtained for home consumption. A household can have several event records, so totalpaid is summed by household. The resulting amount is renamed food_at_home_spending. The original hhnum identifier is renamed household_id for merging.
# B3. *faps_fafhevent_puf.csv - Food-away-from-home (FAFH) events*
This file contains food-away-from-home acquisition events. A household may appear in multiple rows, so totalpaid is summed by household. The resulting amount is renamed food_away_from_home_spending, and hhnum is renamed household_id for merging.

# Why these three CSV files were chosen
Together, these three files provide exactly what is needed for the research question: the household file supplies dinners_prepared_at_home, while the FAH and FAFH event files supply food_at_home_spending and food_away_from_home_spending. After aggregation, the three datasets are merged using household_id. The project then creates total_food_spending = food_at_home_spending + food_away_from_home_spending and uses that numeric variable as the dependent variable in the basic linear regression.
The other FoodAPS CSV files contain useful information about individual household members, meals, food items, nutrients, access, and survey weights, but they are not necessary for this basic regression question. Excluding them makes the workflow easier to explain and keeps the analysis aligned with the project objective.

# C- Variables selected

The analysis selected only the variables needed to answer the research question. For clarity, the FoodAPS variables were renamed as follows: hhnum → household_id, nmealshome → dinners_prepared_at_home, hhsize → household_size, inchhavg_r → monthly_household_income, and ndinnersouthh → dinners_eaten_out. The spending totals were also renamed food_at_home_spending and food_away_from_home_spending. 

# D- Data cleaning

The selected variables were checked for missing values and FoodAPS special negative response codes. Invalid survey codes were converted to missing values so they would not be treated as real numeric observations. Result to report: Insert the number of missing or invalid values found for the main variables and state how many observations remained available for the final analysis.
# E- Data aggregation and merging

Food-at-home (FAH) and food-away-from-home (FAFH) event-level payments were summed by household. The results were renamed food_at_home_spending and food_away_from_home_spending and merged with the household dataset using household_id. 

# F- Feature engineering: total food spending

A new variable, total_food_spending, was created by adding food_at_home_spending and food_away_from_home_spending for each household. This variable serves as the dependent variable in the linear regression.

# G- Exploratory data analysis

Descriptive statistics and visualizations were used to examine the distribution of dinners prepared at home and household food spending before fitting the regression model.

# H- Correlation analysis

The Pearson correlation between dinners_prepared_at_home and total_food_spending was calculated to measure the direction and strength of their linear relationship.

# I- Linear regression
A simple linear and multiple regression was fitted using dinners_prepared_at_home as the independent variable (X) and total_food_spending as the dependent variable (Y). The full cleaned analysis dataset was used; no train/test split was performed. 

# J- Regression graph
A scatterplot of dinners prepared at home versus total food spending was created, and the fitted linear regression line was added to show the estimated relationship.





