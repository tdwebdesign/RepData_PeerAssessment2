# U.S. Storm Data Analysis

Here is the synopsis of the data.  Must be <= 10 complete sentences.

## Data Processing

Download file from https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2FStormData.csv.bz2.  


```r
URL <- "https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2FStormData.csv.bz2"
if(!file.exists("StormData.csv.bz2")){
download.file(URL, "StormData.csv.bz2")
}
data <- read.csv("StormData.csv.bz2")
```

## Results


```r
library(plyr)
health <- ddply(data, ~EVTYPE , summarise, "fatalities" = sum(FATALITIES),
                "injuries" = sum(INJURIES))
health[health$fatalities == max(health$fatalities),]$EVTYPE # most fatalities
```

```
## [1] TORNADO
## 985 Levels:    HIGH SURF ADVISORY  COASTAL FLOOD ... WND
```

```r
health[health$injuries == max(health$injuries),]$EVTYPE # most injuries
```

```
## [1] TORNADO
## 985 Levels:    HIGH SURF ADVISORY  COASTAL FLOOD ... WND
```
