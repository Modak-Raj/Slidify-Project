---
title       : Motot Trend Cars Data Insights
subtitle    : 
author      : Modak Raj
job         : Healthcare
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Overview

This presentation gives a basic over view of Shiny app, about the Motor Trend Cars data.
1. Leveraging basic functions in R we can get some really interesting findings from the data.

2. The app analysese the relationship between fuel economy and other configurational features of the car such as number of cylinders in the motor, output power etc.

3. We can appreciate the output in a few formats i.e. Boxplot and Regression analysis.

4. You can find the app here: https://modakraj.shinyapps.io/Shiny/ 

--- .class #id 

## Data

Description
The data was extracted from the 1974 Motor Trend US magazine, and comprises fuel consumption and 10 aspects of automobile design and performance for 32 automobiles (1973–74 models).

Parameters:
 
 ```r
 library(datasets)
 head(mtcars, 3)
 ```
 
 ```
 ##                mpg cyl disp  hp drat    wt  qsec vs am gear carb
 ## Mazda RX4     21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
 ## Mazda RX4 Wag 21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
 ## Datsun 710    22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
 ```

---.class #id

## Significance and Application

The different configurational features of the car may be  measured on diferent scales but in combination might give some key performance insights.

1. Fuel consumption - How does this get affected based on the transmission.

2. Horsepower - More cylinder leads to higher horsepower, is that related?

3. How does the car weight affect the time for quarter miles?


These are a few KPI for adjudging the performance of the car.

--- .class #idlibrar

## Analysis
Code File:

```r
formulaTextPoint <- reactive({
    paste("mpg ~", "as.integer(", input$variable, ")")  })

  fit <- reactive({
    lm(as.formula(formulaTextPoint()), data=mpgData)  })
  ...
```

```
## Error in eval(expr, envir, enclos): '...' used in an incorrect context
```

```r
  output$fit <- renderPrint({
    summary(fit()) })
```

```
## Error in output$fit <- renderPrint({: object 'output' not found
```

```r
  output$mpgPlot <- renderPlot({
    with(mpgData, {
      plot(as.formula(formulaTextPoint()))
      abline(fit(), col=2)
    })  })
```

```
## Error in output$mpgPlot <- renderPlot({: object 'output' not found
```


