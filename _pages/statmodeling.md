---
layout: archive
title: "Statistics"
permalink: /statmodeling/
author_profile: true
---

## Open Data
Life is full of statistical data, so why don't we take advantage of it? As I live my life, I try to collect as much data as possible whenever I realize there is an opportunity. Here is a list of data I have collected, which may be of use when in need of data to practice skills for statistical analysis or to teach a course for applied statistics.
<br>

[Weight-loss data](https://github.com/maieryo/research/tree/weightloss)<br>
Intermittently in my life, I have tried to lose weight to get into shape. This is a dataset from one of my weight-loss streaks in 2020-2021. There are six variables in the datset.
1. Date = The dates of data points
2. kg = Actual weight in kilograms
3. bmi = Body mass index caculated as kg/(m^2) where m refers to my height (1.72m)
4. Day = Days since the first day
5. Colombia = I went to a trip to Colombia between 2020-2021. This variable refers to whether the dates were before or after the trip
6. Month = The month of the dates.

### Sample Analysis
Here is linear regression modeling of the weight loss data. The model regresses `kg` on `Day`, `Month`, and `Colombia`. I also added an interaction of `Day` and `Month`, so the effect of accumulating days can vary among specific months.

`rm(list=ls()) # Clear R session` <br>
`library(readxl) # Read Excel files`　<br>
`library(sjPlot) # Plotting regression model`　<br>
`library(ggplot2) # Plotting in general`　<br>
<br>
`d <- read_excel("Weight2020.xlsx") # Load the dataset`　<br>
`m <- lm(kg ~ Day*Month, d) # Linear model`　<br>
`summary(m) # See the result`　<br>


| Variable  | Estimate | Std. Error |
| --------  | ---------| -----------|
| Intercept | 85.518    | 1.000     |
| Day       | -0.101    | -0.101    |
| November  | 2.723     | 1.010     |
| December  | 6.404     | 1.359     |
| February  | -0.704    | 1.146     |
| March     | -1.098    | 1.228     |
| May       | 3.998     | 6.154     |
| Day:Novem | -0.005    | 0.011     |
| Day:Decem | -0.144    | 0.024     |
| Day:Feb   | -0.000    | 0.012     |
| Day:March | 0.005     | 0.011     | 
| Day:May   | -0.026    | 0.043     |

<br>
You can also visualize the data using the following code:
`d$Month <- factor(d$Month, levels = c("November", "December", "February", "March", "April", "May"))`
`ggplot(d, aes(x = Day, y = kg, color = Month)) + 
  geom_point()  + 
  geom_smooth(method = "lm") + 
  xlab("Weights in kilograms") +
  ylab("Day (1-145)") +
  scale_y_continuous(breaks = seq(70, 90, 2.5), limits = c(70, 90)) +
  scale_x_continuous(breaks = seq(0, 145, 10), limits = c(0, 145)) +
  theme_bw()`

![kg]([https://github.com/maieryo/maieryo.github.io/assets/kg.png](https://github.com/maieryo/maieryo.github.io/blob/master/assets/kg.png))

<br>

[Sleep data](https://github.com/maieryo/research/tree/sleep)<br>
For 128 days, I collected my sleep data using Fitbit Charge 5 and just made the data publicly available. The file contains the following seven variables. I have additional data regarding which sleep level I was in (a) light sleep, (b) deep sleep, and (c) REM sleep, which to be added soon. 
1. Date = The dates of data points
2. Time = How long I slept in minutes
3. Day = Day of the week
4. Holiday = Whether it was a holiday in Japan,
5. Weekend = Whether it was on the weekend (Saturday or Sunday)
6. Score = Fitbit Charge 5 gives the score for each sleep event
7. Teaching = Whether I had teaching on that day
<br>

## J-SLARF Stats SIG
Japan Second Language Acquisition Forum has a special interest group on applied statistics, especially to be used in L2 research. 

| History | Year        | Topic                          |Textbook    |
| --------| ------------| -------------------------------|------------|
| S1      | 2019-2020   | Multilevel Modeling            | Gelman, A., & Hill, J. (2007). *Data analysis using regression and multilevel/hierarchical models*. New York: Cambridge University Press. |
| S2      | 2020-2021   | Bayesian Data Analysis   | McElreath, R. (2020). *Statistical rethinking: A Bayesian course with examples in R and Stan* (2nd ed.). Boca Raton, FL: CRC Press.          |
| S3      | 2021-2022   | Structural Equation Modeling   | Kline, R. B. (2016). *Principles and practice of structural equation modeling* (4th ed.). New York: The Guilford Press.                  |
| S4      | 2023-2024   | Applied Regression Modeling    | Gelman, A., Hill, J., & Vehtari, A. (2020). *Regression and other stories*. New York: Cambriedge University Press.                   |
