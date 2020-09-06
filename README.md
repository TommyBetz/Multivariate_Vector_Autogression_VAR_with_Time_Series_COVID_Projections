# Covid-19 Cases Projections - multivariate Vector Autogression (VAR) with Time Series

## Project Goal
Develop a projection of daily new Covid-19 cases in the United States for the next 6 months.

## Given Data
The daily.csv file contains a variety of daily data by US state about COVID-19 including the number of total positive cases, new positive cases, tests, and more.

## Model Selection - multivariate Vector Autogression (VAR) with Time Series
Given the short time allowed for this project (less than 3 hours) I selected a simple multivariate Vector Autogression (VAR) model. However, since this model is not multi-step, I had to write additional coding to make it multi-step. I ran the model once to forecast the next date (2020-06-08) based on the previous observations (e.g. last 15 days). Then I would add this forecasted date (2020-06-08) back to the original observations. Then I would make the next forecast (2020-06-09) based on the previous observations (e.g. 15 days which include the last 14 actual observations and 1 forecast.

## Data Processing

### Given Data
From the daily.csv dataset I ignored the State information, and summed up the new cases (positiveIncrease) by day for all states together. From the daily.csv dataset I only used the date and the positiveIncrease columns.

### Weather Data
In addition to the daily.csv dataset I included a Weather dataset. Since I did not want to spend time calculating averages, I looked up the monthly US average temperatures from 2019. Therefore, the average temperatures may not be accurate for this year as they are solely based on the average monthly temperatures from last year. Also, since I did not have daily values, I just assigned each day in a month the same value.

### US Border Information
Furthermore, I also included an information whether the US border was closed. I believe that the US border closed in mid March. I am assuming that the US borders will open up again mid of September. Therefore, I assigned  a 1 when a border was closed and a 0 when a border was not closed.

### Airport Arrivals
I also looked at the total arrivals at US airports in 2020. In January and February the totals were very similar to last years numbers. However, in March 2020 the numbers were significantly less than the previous year. Unfortunately, I was not able to use this dataset as my model returned an error (3-th leading minor of the array is not positive definite). The input weather data was all positive and, and all datasets including the other data were all normalized. While quickly researching this error it seems to be a common bug. However, given the timelimit I decided to not further investigate, and move on.

### Infection Period
I am assuming that the Covid-19 virus takes maximum 14 days for its symptoms to show, and that any person infected with the virus will visit a hospital after 14 days of getting infected. Therefore, I shifted all my additional datasets (weather, border closings, airport arrivals) by 15 (easier number than 14) days to accurately match them with the new cases from the daily.csv dataset.

### Assumptions
- Gap of 14 days between contraction and showing symptoms of Covid-19 
- No seasonality or trend in Covid-19 cases (impossible to say as we do not have prior years of data)
- US borders closed around mid March
- US borders will open up again in in mid September. I estimated that the daily increase of new arrivals starting in mid September will be 7% (semi-arbitrary number) from the previous day.

### Analysis
Given the non-optimization (lack of time) of the model, the forecasts are not very accurate. However, it is interesting to see that the new cases did decrease, and then significantly increased again. The new increase towards the end is due to the my estimates that the US borders will open up again in mid September. 

### Future work
    • include the data from other countries
    • validate and compare different models
        ◦ use different or a mixture of models
    • run the forecast for each US state, and then sum the forecast for the total of the US
    • run a correlation test (e.g. Pearson) to check whether other features in the original daily.csv had any correlations with the daily new cases column (positiveIncrease)
    • with the correlations of all the features I would run a test (recursive feature elimination with cross-validation) to see which features most significantly have an effect on the daily new cases 
        ◦ this would help in eliminating non-important features and speed up the model
    • correct missing data
        ◦ when quickly looking at the daily.csv data I saw rows that were duplicates to their prior day
        ◦ look closer at null/invalid values
        ◦ replace null/invalid values with forecasts or another logic
    • tinker with he model settings for optimal results
    • validate and compare different models
    • add new datasets
        ◦ location (geographical position) of the US state
            ▪ east, west, south, north, mid-west, etc.
        ◦ more detailed numbers of tourists per state
        ◦ use the daily average temperature per US state
        ◦ specific guidelines and restrictions by each state which seem to differ across the US
        ◦ etc.

### Projections
date        daily new cases
2020-06-08    21,260.0
2020-06-09    18,544.0
2020-06-10    19,888.0
2020-06-11    24,674.0
2020-06-12    22,902.0
2020-06-13    23,015.0
2020-06-14    22,279.0
2020-06-15    17,909.0
2020-06-16    18,693.0
2020-06-17    20,890.0
2020-06-18    21,184.0
2020-06-19    23,168.0
2020-06-20    22,745.0
2020-06-21    19,419.0
2020-06-22    18,575.0
2020-06-23    18,113.0
2020-06-24    18,465.0
2020-06-25    21,027.0
2020-06-26    21,738.0
2020-06-27    20,532.0
2020-06-28    19,221.0
2020-06-29    17,163.0
2020-06-30    16,360.0
2020-07-01    17,779.0
2020-07-02    19,008.0
2020-07-03    19,694.0
2020-07-04    19,319.0
2020-07-05    17,257.0
2020-07-06    15,468.0
2020-07-07    15,033.0
2020-07-08    15,549.0
2020-07-09    16,873.0
2020-07-10    17,660.0
2020-07-11    16,809.0
2020-07-12    15,130.0
2020-07-13    13,435.0
2020-07-14    12,563.0
2020-07-15    13,122.0
2020-07-16    14,201.0
2020-07-17    14,630.0
2020-07-18    13,982.0
2020-07-19    12,277.0
2020-07-20    10,451.0
2020-07-21     9,618.0
2020-07-22     9,865.0
2020-07-23    10,630.0
2020-07-24    11,007.0
2020-07-25    10,218.0
2020-07-26     8,483.0
2020-07-27     6,693.0
2020-07-28     5,632.0
2020-07-29     5,623.0
2020-07-30     6,162.0
2020-07-31     6,271.0
2020-08-01     5,383.0
2020-08-02     3,619.0
2020-08-03     1,690.0
2020-08-04       451.0
2020-08-05       166.0
2020-08-06       357.0
2020-08-07       225.0
2020-08-08         0.0
2020-08-09         0.0
2020-08-10         0.0
2020-08-11         0.0
2020-08-12         0.0
2020-08-13         0.0
2020-08-14       270.0
2020-08-15       388.0
2020-08-16       240.0
2020-08-17       166.0
2020-08-18       150.0
2020-08-19       147.0
2020-08-20       239.0
2020-08-21       296.0
2020-08-22       293.0
2020-08-23       278.0
2020-08-24       141.0
2020-08-25        11.0
2020-08-26         4.0
2020-08-27        31.0
2020-08-28        55.0
2020-08-29        44.0
2020-08-30         0.0
2020-08-31         0.0
2020-09-01         0.0
2020-09-02         0.0
2020-09-03         0.0
2020-09-04         0.0
2020-09-05         0.0
2020-09-06         0.0
2020-09-07         0.0
2020-09-08         0.0
2020-09-09         0.0
2020-09-10         0.0
2020-09-11         0.0
2020-09-12         0.0
2020-09-13         0.0
2020-09-14         0.0
2020-09-15         0.0
2020-09-16         0.0
2020-09-17         0.0
2020-09-18         0.0
2020-09-19         0.0
2020-09-20         0.0
2020-09-21         0.0
2020-09-22         0.0
2020-09-23         0.0
2020-09-24         0.0
2020-09-25         0.0
2020-09-26         0.0
2020-09-27         0.0
2020-09-28         0.0
2020-09-29         0.0
2020-09-30         0.0
2020-10-01         0.0
2020-10-02         0.0
2020-10-03         0.0
2020-10-04         0.0
2020-10-05     7,905.0
2020-10-06     6,347.0
2020-10-07     6,190.0
2020-10-08     9,311.0
2020-10-09     8,190.0
2020-10-10     9,936.0
2020-10-11    15,294.0
2020-10-12    19,627.0
2020-10-13    23,212.0
2020-10-14    24,557.0
2020-10-15    23,196.0
2020-10-16    24,761.0
2020-10-17    27,620.0
2020-10-18    30,881.0
2020-10-19    35,614.0
2020-10-20    38,843.0
2020-10-21    39,662.0
2020-10-22    40,051.0
2020-10-23    40,490.0
2020-10-24    42,438.0
2020-10-25    46,707.0
2020-10-26    50,597.0
2020-10-27    53,297.0
2020-10-28    54,748.0
2020-10-29    54,797.0
2020-10-30    55,265.0
2020-10-31    57,456.0
2020-11-01    60,768.0
2020-11-02    64,542.0
2020-11-03    67,462.0
2020-11-04    68,509.0
2020-11-05    68,752.0
2020-11-06    69,368.0
2020-11-07    71,109.0
2020-11-08    74,289.0
2020-11-09    77,832.0
2020-11-10    80,388.0
2020-11-11    81,648.0
2020-11-12    81,956.0
2020-11-13    82,400.0
2020-11-14    84,113.0
2020-11-15    86,998.0
2020-11-16    90,199.0
2020-11-17    92,731.0
2020-11-18    93,945.0
2020-11-19    94,265.0
2020-11-20    94,789.0
2020-11-21    96,296.0
2020-11-22    98,912.0
2020-11-23   101,937.0
2020-11-24   104,292.0
2020-11-25   105,500.0
2020-11-26   105,908.0
2020-11-27   106,379.0
2020-11-28   107,763.0
2020-11-29   110,179.0
2020-11-30   112,946.0

