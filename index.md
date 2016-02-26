---
title       : The accuracy of train() classification predictions.
subtitle    : 
author      : Igor Telezhinsky
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Outline
- Aims
- Moldels and Tuning Parameters
- Basic code

--- .class #id 

## Aims

* help understand the choice of train() parameters
* find optimal method for the given data
* find optimal parameter choice for the method
* reactive visual representation of the results given the choice of
  method and its parameters

--- .class #id 

## Models and Tuning Parameters

* the choice of models:
    - knn: k-nearest neighbours  
    - nnet: neural network  
    - rf: random forest  

* tuning parameters:
    - resampling method of trainControl() function:
        - bootstrapping
        - cross-validation
    - either the number of folds or number of resampling iterations

--- .class #id

## Basic code run by server.R


```r
data(iris);L <- nrow(iris); S <- sample(1:L,size = ceiling(0.7*L))
TrainData <- iris[S,-5]; TrainClass <- iris[S,5]
TestData  <- iris[-S,-5]; TestClass <- iris[-S,5];table(TestClass)
```

```
## TestClass
##     setosa versicolor  virginica 
##         18         12         15
```


```r
Fit<-train(TrainData, TrainClass, preProcess = c("center", "scale"), method = "knn",
     trControl = trainControl(method = "boot",number = 5));
c<-confusionMatrix(predict(Fit,TestData),TestClass); diag(c$table);c$overall['Accuracy']
```

```
##     setosa versicolor  virginica 
##         18         12         14
```

```
##  Accuracy 
## 0.9777778
```


