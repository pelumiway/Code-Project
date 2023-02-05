# Code-Project
Project Submission

---
output:
  word_document: default
  html_document: default
---

title: "Taiwo data analysis"
author: "NAME "Project "
date: "`r Sys.Date()`"
output: pdf_document


```{r, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Marketing plays an important role in the maturing the product.
the marketing cost is more than the production of the product many companies spend more and more money to advertise the product on different medium in the the era of social media the advertisement is not so easy finding the target customer on different medium is more important than selling the product because if we advertise the product on the right medium that will be easy for us to take decision that in which medium we can advertise the product so that it will increase the sales of the product.
Sales of the product depends on different types of medium where we can do  the advertisement.Some companies spend so much money on creating ads for the different medium like video advertisement for Tv AND, product ads for newspaper and the audio ads for radion in this research we are trying to build a model in which we try to find that which medium is a signifcant relationship with the advertisement  
we first import the data in R and then split the data into training and testing dataset in a ratio of 80:20 

```{r,echo=FALSE}
advertising<- read.csv("C:/Users/GNG/Downloads/advertising.csv")
advertising
summary(advertising)
```

```{r}
linear<- lm(formula=Sales~TV+Radio+Newspaper,data=advertising)
summary(linear)
```


```{r,include=FALSE}
set.seed(1)
sample <- sample(c(TRUE, FALSE), nrow(advertising), replace=TRUE, prob=c(0.8,0.2))
train  <- advertising[sample, ]
test   <- advertising[!sample, ]
```

```{r,Echo=FALSE}
summary(train)
```


```{r,Echo=FALSE}
sd(train$Sales)
sd(train$TV)
sd(train$Radio)
sd(train$Newspaper)
```

```{r}
na.exclude(advertising)
boxplot(advertising)
hist(advertising$Sales)
hist(advertising$Newspaper)
hist(advertising$TV)
hist(advertising$Radio)
```
```{r}
library(gbm)

```
```{r}

library(ggplot2)
library(caret)
```
```{r}
library(gbm)
```

```{r}


```

```{r,Echo=TRUE}
head(train)
advertmodel<- lm(data= train,formula =Sales~TV+Radio+Newspaper+TV*Radio)
```


```{r}
summary(advertmodel)
```


```{r}
plot(advertmodel)
```





```{r}
cor(train)
```
```{r}
predict <-predict(advertmodel,data=test)

```


```{r}
summary(predict)
```


```{r,echo=TRUE}
confint(advertmodel)

```
```{r}
library(DescTools)
VIF(advertmodel) 
```


```{r}

model_gbm = gbm(Sales~TV+Radio+Newspaper,
                data = train,
                distribution = "gaussian",
                cv.folds = 10,
                shrinkage = .01,
                n.minobsinnode = 10,
                n.trees = 500)
 
print(model_gbm)

summary(model_gbm)
```
```{r}
plot(model_gbm$fit)

```


```{r}
plot(model_gbm)
```

```{r}
test_x = test[, -1] # feature and target array
test_y = test[, 1] 
```


```{r}
pred_y = predict.gbm(model_gbm, test)
pred_y
```

```{r}
set.seed(1)
model3 <- train(
  Sales ~ .,
  data = train,
  method = 'gbm',
  preProcess = c("center", "scale"),
  verbose = FALSE
)
model3
```




