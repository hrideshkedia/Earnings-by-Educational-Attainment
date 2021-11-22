#### Earnings by Educational Attainment

### Context

Here's a graph from the Social Security Administration which shows that median annual earnings for all men above the age of 20 have decreased since 1988:
![](https://www.ssa.gov/policy/docs/factsheets/at-a-glance/earnings-men-1988-2018.svg)

I wanted to better understand how educational attainment has affected the above trend, and determined wages over the years, and to come up with a model to predict future trends for wages for each educational attainment level. 

As I began looking at the data from the Bureau of Labor Statistics website, there was a striking trend: the median weekly earnings for all groups of people who did not have a bachelors degree or higher had decreased from 1979 levels, in constant 2020 dollars. 

Here I have used historical median weekly earnings data, and labor force data, obtained from the US Bureau of Labor Statistics and the US Census Bureau, to generate forecasts for median weekly earnings by educational attainment level for the years 2021-2030. My forecasts predict that median weekly earnings for persons with a Bachelors or Higher Degree will continue to rise, while the median weekly earnings for all other persons will stagnate over the next decade, at levels comparable to or lower than that in 1979, after adjusting for inflation. 

This suggests that urgent steps are needed to make college education accessible to all.

### Data

The data is collated from the US Bureau of Labor Statistics (https://www.bls.gov/webapps/legacy/cpsatab4.htm) and (https://www.bls.gov/cps/cpswktabs.htm) and the US Census Bureau (https://www.census.gov/data/tables/time-series/demo/income-poverty/historical-income-people.html) to create the csv file uploaded here. The same dataset with more detailed documentation can be accessed here: https://www.kaggle.com/hrideshkedia/labor-force-and-earnings-by-educational-attainment

I have omitted details of gender and race, to solely look at the correlation between educational attainment and median weekly earnings over the years. All of the data is for ages 25 and higher unless otherwise stated in the column header. 

An important note is that all the earnings data are in constant base 2020 dollars. This removes the effects of inflation and makes it possible to compare the numbers over the years.

The data starts at the year 1960, but unfortunately only overall labor force data, and population percentages of persons with a high school graduation (HSG) and persons with a Bachelors or Higher Degree are available. Median weekly earnings data categorized by educational attainment is available from 1979 onwards, while labor force data i.e., labor force level, labor force participation rate and the employment level by educational attainment is available only from 1992 onwards. 

The only columns that have data from 1960 onwards are: (i) overall labor force level, (ii) civilian non-institutional population level, (iii) overall labor force participation rate, (iv) overall employment level, (v) overall percentage of high school graduates, and (vi) overall percentage of persons with a bachelors degree or higher.

### Inspiration

The main question is: what is the best way to generate forecasts for median weekly earnings for each educational attainment level?
