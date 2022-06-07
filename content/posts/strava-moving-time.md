---
title: "Strava Moving Time"
date: 2021-03-04T11:56:19-07:00
draft: true
---

How does Strava calculate moving time? As a hiker, this question dogs me. It isn't that I greatly care about moving time when I am hiking (I prefer to track time-to-summit); my curiosity gets piqued when I see that wildly different number without an explanation. 

I should back up - Strava thinks all my activities are runs because that is the mode I use to record them on my watch. As far as I can tell, there is not an advantage in telling my watch that I am going for a walk instead of a run. In fact, when I do, the data display changes. I just want a consistent experience. On top of that, a lot of my activities in the mountains blur the line between running and hiking. From moment to moment, I do whatever feels most economical.

## How Strava determines when I am stopped on a run

Each time my device (a Garmin watch, most of the time) records data is called a "record". For each record, the device creates a snapshot of the various data fields it can record: time, GPS coordinates, speed, distance, cadence, etc. Different devices create records at different intervals. Most of my devices create a record every second, but one of my watches uses "smart recording" which has a variable sampling rate averaging 5 seconds between records. For runs uploaded from another device (not recorded with their app on a phone), Strava labels each record as "moving" or "stopped" based on my GPS speed. [If I drop below 30 minutes per mile, Strava labels that record as "stopped"](https://support.strava.com/hc/en-us/articles/216917157-Strava-Training-Glossary-for-Running#moving). On a typical run in the flats, the algorithm correctly captures my stops (waiting for a traffic light, waiting for my dog to greet another dog, letting my dog into the house before I head back out). 

On hikes and trail runs (a dubious distinction, but that discussion is for another day), the GPS speed threshold is a less reliable indicator of my movement. First, I just go slower when it gets steep. Just because I go slower than 30 minutes per mile (2 miles per hour) does not mean I am not moving! Second, the GPS signal degrades, meaning the speed calculated using my supposed coordinates becomes a less reliable indicator of my real-world speed. All that to say: my Strava trail runs are **littered** with erroneously-labeled stops. While Strava's simplistic moving-period-labeling algorithm works well for flat-ground runs, I have little confidence in its accuracy as I move through the mountains.

(Show a bloody image of bear peak)

## Strava discards stopped time periods in a complex way

Strava's inaccurate understanding of my hiking behavior is not the point. I like to look at the data straight from the Strava API; that is how I made the plot above. I can see how it labels each record. When I try to recreate its moving time on one of my hikes based on its stopped labels, I actually underestimate. This really only becomes significant when I have hundreds of so-called stopped periods in an activity (there are 166 in the activity above). Something more sophisticated goes into their moving time. It isn't just throwing out all the elapsed time I spend below the speed threshold.