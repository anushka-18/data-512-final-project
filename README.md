# Analysing Economic Impacts of COVID-19 in Monroe County, NY

Through this project, we aim to analyse the impacts COVID-19 had on the employment and housing sector of Monroe County, NY.

## Motivation

Given the widespread impact of the pandemic on the social and economic welfare of the human population, it seemed important to understand exactly how bad the conditions faced by the population of Monroe County was. 
It focusses on a very real problem – it can help the government take actions to mitigate such situations in the future. Although controlling GDP, unemployment, and housing prices in the face of a pandemic can be impossible, certain measures can still be taken to ameliorate the situation proactively.
This is a strong human centered problem as there is a direct negative impact of unemployment on the population, and we can keep human perspective in mind while arriving at the result. I also hope to answer some important ideas that are a consequence of the pandemic that has impacted a huge chunk of the world’s population in direct and indirect ways. 

## Data Sources

We use the following datasets:
* [U.S. State and Territorial Public Mask Mandates From April 10, 2020 through August 15, 2021 by County by Day](https://data.cdc.gov/Policy-Surveillance/U-S-State-and-Territorial-Public-Mask-Mandates-Fro/62d6-pm5i) - The CDC dataset of masking mandates by county.

Column name	| Description
--- | ---
State_Tribe_Territory |	State or tribe name
County_Name |	County name
FIPS_State |	Numeric state identifier
FIPS_County |	Numeric county identifier
date |	YYYY-MM-DD format
order_code |	Order type
Face_Masks_Required_in_Public |	Boolean identifier
Source_of_Action |	Authority
URL |	URL
Citation |	Citation

* [COVID-19 data from John Hopkins University](https://www.kaggle.com/datasets/antgoldbloom/covid19-data-from-john-hopkins-university?select=RAW_us_confirmed_cases.csv) - The RAW_us_confirmed_cases.csv file from the Kaggle repository of John Hopkins University COVID-19 data. This data is updated daily. 

Column name | Description
--- | ---
Province_State | Province or state
Admin2	| Country
UID |	Unique identifier
iso2 |	Unused geography code
iso3 |	Unused geography code
code3 |	Unused geography code
FIPS |	Unique 5-digit identifier
Lat |	Latitude
Long_ |	Longitude


* [Mask-Wearing Survey Data](https://github.com/nytimes/covid-19-data/tree/master/mask-use) - The New York Times mask compliance survey data where participants indicated their mask usage

Column name	| Description
--- | ---
COUNTYFP	| Numeric state and county identifier
NEVER	| Percentage of respondants responding "never" wearing masks
RARELY	| Percentage of respondants responding "rarely" wearing masks
SOMETIMES	| Percentage of respondants responding "sometimes" wearing masks
FREQUENTLY	| Percentage of respondants responding "frequently" wearing masks
ALWAYS	| Percentage of respondants responding "always" wearing masks

* [Unemployment Rate in Monroe County, NY](https://fred.stlouisfed.org/series/NYMONR5URN) - This has been obtained from the U.S. Bureau of Labor Statistics and contains the percentage of people who are unemployed, as obtained from the Current Population Survey (CPS), also known as the household survey.

Column name	| Description
--- | ---
DATE | Date (at monthly granularity) 
NYMONR5URN | Unemployment Percentage in the month

* [Housing Inventory: Median Listing Price in Monroe County, NY](https://fred.stlouisfed.org/series/MEDLISPRI36055) - This has been obtained from Realtor.com and shows the median listing price in a given market during the specified month.

Column name	| Description
--- | ---
DATE | Date (at monthly granularity) 
MEDLISPRI36055 | Median housing price in the month

* [Gross Domestic Product: All Industries in Monroe County, NY](https://fred.stlouisfed.org/series/GDPALL36055) - This has been obtained from the U.S. Bureau of Economic Analysis and contains the yearly GDP in units of thousands of US dollars.

Column name	| Description
--- | ---
DATE | Date (at yearly granularity) 
GDPALL36055 | GDP in Thousands of U.S. Dollars

### Data set Licensing
The Johns Hopkins data is available under the [creative commons license](https://creativecommons.org/licenses/by/4.0/)

The CDC data is available under the below citation: CDC, COVID-19 Community Intervention & Critical Populations Task Force, Monitoring & Evaluation Team, Mitigation Policy Analysis Unit, the CDC, Center for State, Tribal, Local, and Territorial Support, Public Health Law Program, and Max Gakh, Assistant Professor, School of Public Health, University of Nevada, Las Vegas, “U.S. State and Territorial Orders Requiring Masks in Public,” (August 15, 2021).

The Unemployment Data is open for free use after attributing the source - BLS.gov 
BLS.gov cannot vouch for the data or analyses derived from these data after the data have been retrieved from BLS.gov.

The GDP data is open for free use after attributing the source - bea.gov

The housing prices data is open for free use after attributing the source - https://www.realtor.com/research/data/

## Repository Structure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
├── README.md
├── LICENSE
├── data
│   ├── RAW_us_confirmed_cases.csv
│   ├── RAW_us_deaths.csv
│   └── mask-use-by-county.csv
├── reports
|   ├── Reflection on Collaboration.pdf
├   ├── Visualization Explanation.pdf
|   ├── Final Report.pdf
|   ├── Extension Plan.pdf
├── notebooks
|   ├──Analysis-COVID-Cases-Monroe.ipynb
|   ├──economic_impacts_analysis.ipynb
├── images
│   ├── Derivative of Rate of Infection Method 2.png
│   ├── Effect of masking policies on rate of infection.png
│   ├── Effect of masking policies on rate of infection second method.png
|   ├── GDP in Monroe County.png
|   ├── Median Housing Prices in Monroe County.png
|   ├── Unemployment Percentage in Monroe County.png
│   └── intermediate visualizations and EDA
│       ├── Daily Active Cases.png
│       ├── Daily death rate time series.png
│       ├── Daily total death count.png
│       └── Derivative of rate of infection.png
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

## Research Questions

* How was employment impacted by the pandemic in Monroe County, NY?
* How did median housing price of Monroe County on a month-to-month basis change with the rate of infection in Monroe County?

### Hypothesis

* Unemployment rates in Monroe County have a positive correlation with COVID-19 cases.
* Median housing prices are not “Granger Caused” by COVID-19 cases in Monroe County, ie, they do not increase with the increase in the case count.

## Methodology

To see if unemployment trends changed with respect to change in COVID-19 cases, I used Pearson Correlation coefficient. 
The Pearson correlation method is the most common method to use for numerical variables; it assigns a value between − 1 and 1, where 0 is no correlation, 1 is total positive correlation, and − 1 is total negative correlation. This is interpreted as follows: a correlation value of 0.7 between two variables would indicate that a significant and positive relationship exists between the two. A positive correlation signifies that if variable A goes up, then B will also go up, whereas if the value of the correlation is negative, then if A increases, B decreases. 
Thus, it is an appropriate test to test if unemployment increased with increase in COVID-19 cases.

The following steps were followed:
*	Cleaned the data and transformed the daily covid case count to monthly case count.
*	Plotted the daily case count and the unemployment percentages with respect to time from February 2020 to October 2022 to perform a visual analysis.
*	Calculated the value of Pearson coefficient between unemployment percentages and COVID-19 cases using the pearsonr() function[8] from the scipy library in Python for this analysis.

To see if the median housing prices changed with respect to change in COVID-19 cases, I plan to use Granger causality test, which is a statistical hypothesis test for determining whether one time series is useful for forecasting another. If probability value is less than any level, then the hypothesis would be rejected at that level. This test requires the time series to be stationary.

The following steps were followed:
*	Cleaned the data and transformed the daily covid case count to monthly case count.
*	Plotted the daily case count and the median housing prices with respect to time from February 2020 to October 2022 to perform a visual analysis.
*	The stationarity of the time series was tested using Augmented Dickey Fuller Test.
*	None of the time series was stationary, second order differencing is applied to both the time series to make them stationary.
*	Granger causality test is applied to test if one time series (COVID-19 case count) causes another (median housing prices). grangercausalitytests() function from the statsmodels library in Python for this analysis.


## Limitations
* The original formulation of G-causality can only give information about linear features of signals. Extensions to nonlinear cases now exist, however these extensions can be more difficult to use in practice and their statistical properties are less well understood.
The COVID-19 case count data and the housing prices are not strictly linear functions of time.
* G-causality should not be interpreted as directly reflecting physical causal chains.
* Pearson Correlation can only speak about correlation, not causation.

## Human Centered Aspect of the Project
*	It captures and aims to analyse the unfortunate conditions millions of people faced because of the pandemic.
*	There’s a direct negative impact of unemployment and rising housing prices on the population and economy.
*	The techniques used in the analysis as well as the results are easy to explain to a general audience.
*	The limitations of the analysis and the techniques are kept in mind instead of obfuscating the results or the numbers.


## Findings

### Visual Inspection

* This plot shows the rate of infection of COVID-19 in Monroe County from February 2020 to October 2021 while indicating the masking policy that was in effect at the time. The x-axis shows the time progression and is labelled with months over this period, and the y-axis shows the change in daily confirmed cases.
![image](https://user-images.githubusercontent.com/40142355/199908484-155e6625-4be8-40d4-914b-8b898791c717.png)

* We have plots showing the trends of COVID-19 cases and unemployment percentages. As the cases rose steadily over this period, we see that unemployment percentages peaked around April 2020, which is also around the time masking policy took effect but continued to decrease as the pandemic progressed.

 ![image](https://user-images.githubusercontent.com/40142355/207231921-5fd418be-6622-4f1a-9737-634e09edd197.png)

* GDP in Monroe County mostly increased over almost 20 years from 2001 to 2019, but saw a decrease from 2019 to 2020, which is also when the pandemic was just beginning. Median housing prices had an on-off trend where they rose and fell in no discernible pattern, but after an increase at the beginning of the pandemic, they seem to stabilize and fall barring one more peak around January 2021.

 ![image](https://user-images.githubusercontent.com/40142355/207231983-4e4634e9-bc37-4505-bd94-b9ad861eb182.png)

* Median housing prices had an on-off trend where they rose and fell in no discernible pattern, but after an increase at the beginning of the pandemic, they seem to stabilize and fall barring one more peak around January 2021.

 ![image](https://user-images.githubusercontent.com/40142355/207232155-1f21c937-4290-4754-9823-95dd4b5bb833.png)

### Statistical Analysis

* The results of our statistical analysis seem to confirm the unemployment plots. We get the value of the Pearson Coefficient as -0.533, which signifies a negative correlation. 
* We see that the p-value from Granger-Causality test is less than 0.05 for Chi-Square test (0.000) and LR test (0.0004) at lag=4, and we reject the null hypothesis that Median housing prices are not “Granger-Caused” by COVID-19 cases in Monroe County at 95% confident level. 

## Conclusion

*	While arriving at a direct impact of masking policies on the rate of infection is difficult, it is clear to see that the masking mandate was removed after a significant drop in cases, and the cases began to rise once again after the mandate was removed. There is a lot of variation in the rate of infection – this cannot be attributed to masking policies alone. There have to be other stronger factors at play here which include vaccinations, natural immunity after first infection, increase or decrease in testing.
*	Unemployment percentages are negatively correlated with increase in COVID-19 cases in Monroe County - which was initially unexpected given the existing research and articles, but open deeper analysis, made sense because unemployment peaked once when lockdown policies took effect and stabilized over the duration of the pandemic.
*	Increase in the median housing prices are Granger-Caused by the increase in COVID-19 cases in Monroe County. From visual inspection, we see that the prices rise and fall over the period of our analysis. Upon deeper inspection, we find that the housing prices first peaked when COVID-19 lockdown in New York was implemented around April 2020, and then peaked in January 2021 when we also see a sharp rise in the case count. 
*	Monroe County’s GDP in 2020 was lower than the previous year for only the second time in 20 years starting from January 2001. This was more of an exploratory analysis and cannot be confidently attributed to COVID-19 through this project, although reports and articles suggest that the economy was hit in Monroe County during the pandemic.
