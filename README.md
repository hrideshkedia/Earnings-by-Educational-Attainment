### *Earnings by Educational Attainment*

### Context

Here's a graph from the Social Security Administration which shows that median annual earnings for all men above the age of 20 have decreased since 1988:
![](https://www.ssa.gov/policy/docs/factsheets/at-a-glance/earnings-men-1988-2018.svg)

I wanted to better understand how educational attainment has affected the above trend, and determined wages over the years, and to come up with a model to predict future trends for wages for each educational attainment level. 

As I began looking at the data from the Bureau of Labor Statistics website, there was a striking trend: the median weekly earnings for all persons who did not have a bachelors or higher degree had decreased from 1979 levels, in constant 2020 dollars: 
![](https://github.com/hrideshkedia/Earnings-by-Educational-Attainment/blob/main/mwe_data.png)
where the educational attainment levels are denoted by:
LHS -- Less than High School diploma
HSG -- High School Graduation
CAD -- some College or Associates Degree
BHD -- Bachelors or Higher Degree

My goal is use historical median weekly earnings data, and labor force data, obtained from the US Bureau of Labor Statistics and the US Census Bureau, to generate forecasts for median weekly earnings by educational attainment level for the years 2021-2030, and forecast how the above mentioned trend is likely to change or to continue.

### Data

The data is collated from the US Bureau of Labor Statistics (https://www.bls.gov/webapps/legacy/cpsatab4.htm) and (https://www.bls.gov/cps/cpswktabs.htm) and the US Census Bureau (https://www.census.gov/data/tables/time-series/demo/income-poverty/historical-income-people.html) to create the csv file uploaded here. The same dataset with more detailed documentation can be accessed here: https://www.kaggle.com/hrideshkedia/labor-force-and-earnings-by-educational-attainment

I have omitted data on gender and race, to look solely at the correlation between educational attainment and median weekly earnings over the years. All of the data is for ages 25 and higher unless otherwise stated in the column header. 

An important note is that all the earnings data are in constant base 2020 dollars. This removes the effects of inflation and makes it possible to compare the numbers over the years.

The data starts at the year 1960, but unfortunately only overall labor force data, and population percentages of persons with a high school graduation (HSG) and persons with a Bachelors or Higher Degree are available. Median weekly earnings data categorized by educational attainment is available from 1979 onwards, while labor force data i.e., labor force level, labor force participation rate and the employment level by educational attainment is available only from 1992 onwards. 

The only columns that have data from 1960 onwards are: (i) overall labor force level, (ii) civilian non-institutional population level, (iii) overall labor force participation rate, (iv) overall employment level, (v) overall percentage of high school graduates, and (vi) overall percentage of persons with a bachelors degree or higher.

### Question:

The main question is: what is the best way to generate forecasts for median weekly earnings for each educational attainment level?

### Approach:

We have at our disposal historical median weekly earnings data for each educational attainment level, and the labor force data for each educational attainment level, along with overall labor force data and the population percentage of persons with High School Graduation (HSG) and the population percentage of persons with a Bachelors or Higher Degree (BHD). 

We will use two approaches to forecast the median weekly earnings data for each educational attainment level: (i) a model that uses only the historical median weekly earnings data for each educational attainment level (ii) a model that uses the historical and forecasted labor force data along with the median weekly earnings data for each educational attainment level. 

The idea behind the 1st approach is simple: to identify the linear and seasonal trends in the historical data, and use that to generate a forecast for the future. 

The idea behind the 2nd approach is that in addition to historical trends, earnings must be determined by market factors and the supply of labor, which are to captured to some extent by the available labor force  data: the labor force level, the employment level and the labor force participation rate. The 2nd approach forecasts the trends in the market forces and labor supply and attempts to capture the dependence of earnings on these factors in addition to the historical trends. The drawback of the 2nd approach is that the labor force data for each educational attainment level is available only from 1992 onwards, while the historical median weekly earnings for each educational level is available for 1979 onwards. We use the historical median weekly earnings data only from 1992 onwards in this approach, losing out on a decade of data. 

We will present forecasts using both approaches.

### Method:

Since we want to forecast values of the median earnings and the labor force variables a decade into the future and not just one year into the future, we  will use Structural Time Series (STS) models from the Tensor Flow Probability package instead of other machine learning methods which require much more data to fit, and often involve errors that accumulate rapidly over time for future predictions. We will use [this fantastic example notebook from TensorFlow Probability](https://colab.research.google.com/github/tensorflow/probability/blob/main/tensorflow_probability/examples/jupyter_notebooks/Structural_Time_Series_Modeling_Case_Studies_Atmospheric_CO2_and_Electricity_Demand.ipynb#scrollTo=ULm_Z8Oe0Lhd) as our guide.

(i) In the first approach, we will build an STS model with a semi-local linear trend (to keep the variance bounded), and a seasonal component to forecast the values for the years 2021-2030, where we use a periodogram (a Fourier Transform really) to determine the durations and number of seasons. 

(ii) In the second approach, we will incorporate in addition to the above, a linear regression with the labor force data and its forecasted values as regressors. 
For this, we need to forecast the labor force data for each educational attainment level. To do this we use both the past historical data for that educational level and labor force variable and regressors calculated from the overall data for that labor force variable by multiplying with the population percentages for high school (HSG) and bachelors (BHD) degrees. 


### Results:

(i) Forecasts using only the historical median weekly earnings data for that educational attainment level:
![](https://github.com/hrideshkedia/Earnings-by-Educational-Attainment/blob/main/mwe_historical_forecast.png)
where the mean of forecast distribution for each educational attainment level is shown in  dashed lines, and the shaded region around it denotes two standard deviations above and below the mean. 

(ii) Forecasts using the historical median weekly earnings data and labor force data and forecasts for that educational attainment level:
![](https://github.com/hrideshkedia/Earnings-by-Educational-Attainment/blob/main/mwe_lf_historical_data_forecast.png)

While the variance of our forecasts differ between the two methods, both methods predict that median weekly earnings for persons with a Bachelors or Higher Degree will continue to rise, while the median weekly earnings for all other persons will stagnate over the next decade, at levels comparable to or lower than that in 1979, after adjusting for inflation. 

This suggests that urgent steps are needed to make college education accessible to all.
