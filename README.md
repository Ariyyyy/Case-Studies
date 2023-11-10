# Cyclistic bike-share analysis

### Project Overview

Cyclistic is a fictional bike share company in Chicago. The bike-share program features more than 5,8000 bicycles and 600 docking stations. The bikes can be unlocked from one station and returned to any other station in the system anytime. Until now, Cyclistic's marketing strategy relied on building general awareness and appealing to broad consumer segments. One approach that helped make these things possible was the flexibility of its pricing plans: single- ride passes, full-day passes, and annual memberships. Customers who purchase single- ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members. Cyclistic's finance analysts have concluded that annual members are much more profitable than casual riders. The director of marketing believes the company's future success depends on maximizing the number of annual memberships. Therefore the marketing analyst team wants to understand how casual riders and annual members use cyclistic bikes differently. From these insights,the team will design a new marketing strategy to convert casual riders into annual memebrs.

### Data Sources

This data has been made available by Motive International Inc under this license (https://divvybikes.com/data-license-agreement)

### Tools
- R

### Data Cleaning/ Preparation
1. Installed and loaded tidyverse to help wrangle data, lubridate to help wrangle date attributes, and ggplot2 to help visualize data.
2. Removed data that was not needed for analysis.
3. Handling missing values.
4. Data cleaning and formatting.

### Exploratory Data Analysis
- How do annual members and casual riders ues Cyclistic bikes differently?
- What is the average ride length for both casual riders and members?
- What is the number of rides for both casual riders and members?

### Data Analysis

Used the summary() function to quickly summarize the ride length to get the mean, median, maximum, and minimum values.

```R
summary(all_trips_v2$ride_length)
```

Visualized the number of rides by rider type

```R
all_trips_v2 %>%
 mutate(weekday = wday(started_at, label = TRUE)) %>%
 group_by(member_casual, weekday) %>%
 summarise(number_of_rides = n()
     ,average_duration = mean(ride_length)) %>%
 arrange(member_casual, weekday) %>%
 ggplot(aes(x = weekday, y = number_of_rides, fill = memebr_casual)) +
 geom_col(position = "dodge")+
 labs(title= "Number of rides: Casual vs Member", subtitle= "q4 2019 - q1 2020")
```

Visualized the average duration

```R
all_trips_v2 %>%
 mutate(weekday = wday(started_at, label = TRUE)) %>$
 group_by(member_casual, weekday) %>%
 summarise(number_of_rides = n()
    ,average_duration = mean(ride_length)) %>$
 arrange(member_casual, weekday) %>%
 ggplot(aes(x = weekday, y = average_duration, fill = member_casual)) +
 geom_col(position = "dodge")+
labs(title= "Average duaration: Casual vs Member", subtitle= "q4 2019 - q1 2020")
```

### Results/ Findings

The analysis results are summarized as follows:

Annual members go on more rides than casual riders and casual riders take longer rides than members throughout the week for a one year period through q4 2019 to q1 2020.

### Recommendations

Based on the analysis, the recommendations are as follows:
1. A promotion, if casual riders ride a certain duration they could upgrade to become an annual member and get the first month free or at a discounted price.
2. If casual riders uprade to an annual member they could get a ride with unlimited duration for a certain amount of time. Ex. 3 days.

### Limitations
- Removed latitude, longitude, birth year and gender fields as this data was dropped beginning in 2020.
- Removed "bad" data. The dataframe included a few hundred entries when bikes were taken out of docks and checked for quality or the ride length was negative.
