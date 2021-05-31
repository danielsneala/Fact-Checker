---
title: "Heart Analysis"
author: "Neal Daniels"
date: "May 28, 2021"
output:
  html_document:
    keep_md: true
    code_folding: hide
    theme: cerulean
---


```r
library(readr)
library(haven)
library(readxl)
library(downloader)
library(tidyverse)
library(foreign)


TemporaryFile <- tempfile()

ZippedData <- download("https://www.kaggle.com/rashikrahmanpritom/heart-attack-analysis-prediction-dataset/download", TemporaryFile, mode = "wb")

ExtractData <- unzip(TemporaryFile)

ExtractData
```

```
## NULL
```

```r
# Attempt_1<- read_csv(ExtractData)


# Col meanings:
# Age- age of patient
# Sex - gender of patient
# exang- exercise induced angina (1- yes, 0- no)
# ca - number of major vessels (0-3)
# cp - chest paing type (1- typical angina, 2- atypical, 3- non-anginal pain, 4-asymptomatic)
# trtbps- resting blood pressure (in mm Hg)
# chol - cholestoral in mg/dl
# fbs (fasting blood sugar > 120 mg/dl, 1 - true, 0- false)
# rest_ecg - resting electrocardiographic results (0- normal, 1- abnormality present, 2- probable or definite left ventricular hypertrophy)
# thalach- max heart rate achieved
# target - 0- less chance of heart attack, 1- more chance of heart attack. 


heart <- read_csv("archive/heart.csv") %>%
  mutate(AgeRank = case_when(
    str_detect(age, c("34", "35", "37", "38", "39", "40")) ~ "34-40",
    str_detect(age, c("41", "42", "43", "44", "45", "46", "47", "48", "49", "50")) ~ "41-50",
    str_detect(age, c("51", "52", "53", "54", "55", "56", "57", "58", "59", "60")) ~ "51-60",
    #str_detect(age, c(61-70)) ~ "61-70",
    T ~ "Outsiders"
  ))
```


```r
# Chi Squared test, look at age vs target, sex vs target, ca vs target, cp vs target.
library(pander)
```


```r
# Chi squared test, look at fbs vs age (34-40, 41-50, 51-60, 61-70), fbs vs sex, etc. 


Chi_fbsAgeRank <- table(heart$fbs, heart$AgeRank)


# Can't use. 
pander(Chi_fbsAgeRank)
```


--------------------------------------------
 &nbsp;   34-40   41-50   51-60   Outsiders 
-------- ------- ------- ------- -----------
 **0**      3      10      11        234    

 **1**      0       0       2        43     
--------------------------------------------

```r
#Chi_
```
