---
title       : MPG Prediction Using ShinyApp
subtitle    : Developing Data Products Project
author      : Serkan Serttop
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Target Audience

Many drivers are interested in the mpg eficiency of their car. 
Drivers are mainly concerned about:

1. The environment.

2. The economic impact in a period of rising fuel costs.

Our app allows drivers to:

1. Tweak the parameters they are interested in.

2. Balance features according to their concerns.

--- .class #id 

## Dataset

The "Motor Trend Car Road Tests" dataset was taken from 1974 Motor Trend US Magazine.
The dataset contains information on 32 cars on the following 11 variables. 

1. mpg   Miles/(US) gallon
2. cyl	 Number of cylinders
3. disp	 Displacement (cu.in.)
4. hp	 Gross horsepower
5. drat	 Rear axle ratio
6. wt	 Weight (lb/1000)
7. qsec	 1/4 mile time
8. vs	 V/S
9. am	 Transmission (0 = automatic, 1 = manual)
10. gear	 Number of forward gears
11. carb	 Number of carburetors

--- .class #id 

## Predictive Model 

**Step** function of **R** found "wt + cyl + hp + am" variables to give the best fit when 'am', 'carb', 'cyl', 'gear', 'vs' variables were factorized. Further manual examination revealed that adding the interaction term wt:am improved the adjusted R-squared. That mix was chosen as the final model.


```r
model <- lm( mpg ~ wt + cyl + hp + am + wt:am, data = mtcars )
summary(model)$coefficients
```

```
##             Estimate Std. Error t value  Pr(>|t|)
## (Intercept) 33.22945    3.01690 11.0144 2.732e-11
## wt          -2.19536    0.84638 -2.5938 1.539e-02
## cyl         -0.83651    0.52826 -1.5835 1.254e-01
## hp          -0.01246    0.01322 -0.9426 3.545e-01
## am          11.26038    3.91986  2.8726 7.999e-03
## wt:am       -3.72353    1.40714 -2.6462 1.364e-02
```
One detail merits pointing out, cars with manual tranmission have better mpg up to about 3.024 thousand pounds, after which cars with automatic transmission become more efficient.

--- .class #id 

## Shiny App

Our shiny app offers users to tweak the following parameters:

1. Weight

2. Cylinders

3. Horse Power

4. Type of Transmission

When any parameter is changed, our app immediately returns the result with a sentence like below:

"A car with manual transmission, weighing 1995 pounds, that has 4 cylinders and 140 horse power is predicted to have 27.38 mpg"

