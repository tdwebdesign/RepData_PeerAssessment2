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
health <- ddply(data, .(EVTYPE, STATE) , summarise, "fatalities" = sum(FATALITIES),
                "injuries" = sum(INJURIES))
states <- unique(health$STATE)
state_health <- data.frame()
for (i in 1:length(states)){
        curr <- health[health$STATE == states[i],]
        ST <- states[i]
        most_fatal <- max(curr$fatalities)
        most_fatal_type <- curr[curr$fatalities == max(curr$fatalities),]$EVTYPE
        most_injure <- max(curr$injuries)
        most_injure_type <- curr[curr$injuries == max(curr$injuries),]$EVTYPE
        new_data <- data.frame(ST, most_fatal, most_fatal_type, most_injure,
                     most_injure_type)
        if(!(most_fatal == 0 | most_injure == 0)){
                state_health <- rbind(state_health, new_data)
        }
}
state_health
```

```
##    ST most_fatal          most_fatal_type most_injure
## 1  AS         32                  TSUNAMI         129
## 2  NJ         39           EXCESSIVE HEAT         300
## 3  TX        538                  TORNADO        8207
## 4  AZ         62              FLASH FLOOD         179
## 5  GA        180                  TORNADO        3926
## 6  IL        653                     HEAT        4145
## 7  FL        172              RIP CURRENT        3340
## 8  WA         35                AVALANCHE         303
## 9  WV         24              FLASH FLOOD         142
## 10 IN        252                  TORNADO        4224
## 11 KY        125                  TORNADO        2806
## 12 MO        388                  TORNADO        4330
## 13 CA        110           EXCESSIVE HEAT         623
## 14 ME          6                LIGHTNING          70
## 15 NH          6                TSTM WIND          85
## 16 MD         88           EXCESSIVE HEAT         461
## 17 VA         36                  TORNADO         914
## 18 DE          7           EXCESSIVE HEAT          73
## 19 NC        126                  TORNADO        2536
## 20 NY         93           EXCESSIVE HEAT         315
## 21 OR         19                HIGH WIND          50
## 22 PA        359           EXCESSIVE HEAT        1241
## 23 AK         33                AVALANCHE          34
## 24 ID         16                AVALANCHE          74
## 25 KS        236                  TORNADO        2721
## 26 LA        153                  TORNADO        2637
## 27 SC         59                  TORNADO        1314
## 28 MT          9                LIGHTNING          33
## 29 CO         48                AVALANCHE         261
## 30 CO         48                LIGHTNING         261
## 31 NV         54                     HEAT          50
## 32 UT         44                AVALANCHE         415
## 33 WY         23                AVALANCHE         119
## 34 CT          6                HIGH WIND         703
## 35 DC         20           EXCESSIVE HEAT         316
## 36 HI         21                HIGH SURF          20
## 37 IA         81                  TORNADO        2208
## 38 MA        108                  TORNADO        1758
## 39 MI        243                  TORNADO        3362
## 40 MN         99                  TORNADO        1976
## 41 ND         25                  TORNADO         326
## 42 NE         54                  TORNADO        1158
## 43 NM         16              FLASH FLOOD         155
## 44 OH        191                  TORNADO        4438
## 45 OK        296                  TORNADO        4829
## 46 RI          2                     HEAT          23
## 47 RI          2                HIGH SURF          23
## 48 SD         18                  TORNADO         452
## 49 VT          4                    FLOOD          24
## 50 WI         96                  TORNADO        1601
## 51 PR         34              FLASH FLOOD          10
## 52 AL        617                  TORNADO        7929
## 53 MS        450                  TORNADO        6244
## 54 VI          3                HIGH SURF           1
## 55 VI          3                HIGH SURF           1
## 56 AR        379                  TORNADO        5116
## 57 TN        368                  TORNADO        4748
## 58 GU         20              RIP CURRENT         333
## 59 AM          6 MARINE THUNDERSTORM WIND          22
## 60 AN          6         MARINE TSTM WIND          18
## 61 LM          2       MARINE STRONG WIND           1
## 62 LM          2 MARINE THUNDERSTORM WIND           1
## 63 PZ          5       MARINE STRONG WIND           3
##            most_injure_type
## 1                   TSUNAMI
## 2            EXCESSIVE HEAT
## 3                   TORNADO
## 4                DUST STORM
## 5                   TORNADO
## 6                   TORNADO
## 7                   TORNADO
## 8                   TORNADO
## 9                 TSTM WIND
## 10                  TORNADO
## 11                  TORNADO
## 12                  TORNADO
## 13                 WILDFIRE
## 14                LIGHTNING
## 15                LIGHTNING
## 16           EXCESSIVE HEAT
## 17                  TORNADO
## 18                  TORNADO
## 19                  TORNADO
## 20                  TORNADO
## 21                HIGH WIND
## 22                  TORNADO
## 23                ICE STORM
## 24        THUNDERSTORM WIND
## 25                  TORNADO
## 26                  TORNADO
## 27                  TORNADO
## 28         WILD/FOREST FIRE
## 29                  TORNADO
## 30                  TORNADO
## 31                    FLOOD
## 32             WINTER STORM
## 33             WINTER STORM
## 34                  TORNADO
## 35           EXCESSIVE HEAT
## 36              STRONG WIND
## 37                  TORNADO
## 38                  TORNADO
## 39                  TORNADO
## 40                  TORNADO
## 41                  TORNADO
## 42                  TORNADO
## 43                  TORNADO
## 44                  TORNADO
## 45                  TORNADO
## 46                  TORNADO
## 47                  TORNADO
## 48                  TORNADO
## 49                TSTM WIND
## 50                  TORNADO
## 51               HEAVY RAIN
## 52                  TORNADO
## 53                  TORNADO
## 54                LIGHTNING
## 55             RIP CURRENTS
## 56                  TORNADO
## 57                  TORNADO
## 58        HURRICANE/TYPHOON
## 59 MARINE THUNDERSTORM WIND
## 60       MARINE STRONG WIND
## 61       MARINE STRONG WIND
## 62 MARINE THUNDERSTORM WIND
## 63       MARINE STRONG WIND
```
