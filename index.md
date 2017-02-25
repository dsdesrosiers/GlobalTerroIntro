---
title       : Global Terrorism by Region and Year
subtitle    : 
author      : Danielle Desrosiers
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax, quiz, bootstrap] # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Introduction

The Global Terrorism Database is maintaned by the University of Maryland. It is an is an open-source database including information on more than 150,000 terrorist events around the world from 1970 through 2015 (with additional annual updates planned for the future). 

The data found at https://dsdesrosiers.shinyapps.io/Terrorism/ has been preprocessed into format and size manageable for this project (the original data set is 75MB). The preprocessing steps include:

1. Reading of the data
2. Grouping of the data by year (iyear field) and region (region_txt field)
3. Counting of the attacks within this grouping

The result is a much smaller data set - only 504 rows across 3 columns. Code to show some of the sample is on the next slide.

The application at shinyio allows users to more fully examine all 35 years of the dataset across all the regions.

---

## Process sample of Terror Attacks by Year and Region


```r
require(data.table)
require(dplyr)
require(plyr)
require(janitor)

attacks <- fread("../attackInAggregate.csv",sep = ";", header = TRUE)%>%
        clean_names()

attack_year_rgn <- attacks %>% 
        plyr::rename(c("region" = "Region")) %>%
        filter (iyear == 1970)
```

--- 

## Sample of aggregated data


```r
kable(attack_year_rgn)
```



|iyear |Region                      | attacks|
|:-----|:---------------------------|-------:|
|1970  |Australasia & Oceania       |       1|
|1970  |Central America & Caribbean |       7|
|1970  |East Asia                   |       2|
|1970  |Eastern Europe              |      12|
|1970  |Middle East & North Africa  |      29|
|1970  |North America               |     472|
|1970  |South America               |      65|
|1970  |South Asia                  |       1|
|1970  |Southeast Asia              |      10|
|1970  |Sub-Saharan Africa          |       3|
|1970  |Western Europe              |      49|

---

## More informaiton about the Global Terrorism Database

The Global Terrorism Database is maintaned by the University of Maryland. 

From the authors: The Global Terrorism Database (GTD) is an open-source database including information on terrorist events around the world from 1970 through 2015 (with additional annual updates planned for the future). Unlike many other event databases, the GTD includes systematic data on domestic as well as transnational and international terrorist incidents that have occurred during this time period and now includes more than 150,000 cases. For each GTD incident, information is available on the date and location of the incident, the weapons used and nature of the target, the number of casualties, and--when identifiable--the group or individual responsible.

Citation: National Consortium for the Study of Terrorism and Responses to Terrorism (START). (2016). Global Terrorism Database [Data file]. Retrieved from https://www.start.umd.edu/gtd



