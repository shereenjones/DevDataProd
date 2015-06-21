---
title       : Predict MPG
subtitle    : Use number of cylinders and weight in tons, to predict vehicle mpg
author      : Shereen Jones
job         : R Student
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [shiny, interactive]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
logo        : dss_logo.png
runtime     : shiny

---

## Welcome to Predict MPG

Predict MPG is a shiny app that allows you to predict the miles-per-gallon of any vehicle given the number of cylinders and weight of the vehicle.

It is an easy-to-use intuitive application.

The application is available at http://shereenjones.shinyapps.io/pa1_app and may be used by anyone who so desires.

---

## Basis of the Prediction Model

The prediction model is built using the mtcars data in R.  The model is developed as follows:

```r
     library(UsingR)
     predModel <- lm (mpg ~ cyl + wt, data=mtcars)
     predModel
```

```
## 
## Call:
## lm(formula = mpg ~ cyl + wt, data = mtcars)
## 
## Coefficients:
## (Intercept)          cyl           wt  
##      39.686       -1.508       -3.191
```

---

## Generating the Prediction

The actual mpg predicted is easily generated.  The simulation below shows how one could use the same method to generate the value for 5 randomly selected cylinder and weight pairs.


```r
     newcyl <- seq(min(mtcars$cyl), max(mtcars$cyl), length=5)
     newwt <- seq(min(mtcars$wt), max(mtcars$wt), length=5)
     newdata <- data.frame(cbind(cyl=newcyl, wt=newwt))
     newmpg <- data.frame(predict(predModel, newdata, interval="prediction"))
     newdata$mpg <- newmpg$fit
     newdata
```

```
##   cyl      wt      mpg
## 1   4 1.51300 28.82714
## 2   5 2.49075 24.19937
## 3   6 3.46850 19.57160
## 4   7 4.44625 14.94384
## 5   8 5.42400 10.31607
```

---

## Conclusion

The application is a simple one, but a useful one that satisfies many objectives.

1. You will get a reasonable accurate prediction of your vehicles mpg.
2. It is easy to use and readily available via the web.
3. It demonstrates the capabilities of shiny.
4. It costs nothing and it is ad free.

Go check out Predict MPG.

---

## Play with Predict MPG here

Input number of cylinders and weight in tons:

<div class="row-fluid">
  <div class="col-sm-4">
    <form class="well">
      <div class="form-group shiny-input-container">
        <label for="newcyl">No of cylinders</label>
        <input id="newcyl" type="number" class="form-control" value="6.1875"/>
      </div>
      <div class="form-group shiny-input-container">
        <label for="newmt">Weight</label>
        <input id="newmt" type="number" class="form-control" value="3.21725"/>
      </div>
    </form>
  </div>
  <div class="col-sm-8">
    <div id="p1" class="shiny-html-output p1"></div>
  </div>
</div>
