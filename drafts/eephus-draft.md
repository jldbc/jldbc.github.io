---
title: "A Statcast Tribute to Baseball's Strangest Pitch: the Eephus"
layout: post
categories: statcast
excerpt: TBD 
---
I've been borderline obsessed with the eephus for some time now. Every time I see a player pull this pitch out of their arsenal I become equal parts excited and bamboozled. My reaction is typically equal parts "I could throw that," and "how on earth didn't he hit that?" 

For those who aren't familar, here's a quick description and history of the eephus pitch. In short, an eephus is a blooper pitch: it has a lazy, slow-pitch rec league style delivery, can arch well above the batter's head en route to the plate, and tends to travel anywhere from 40 to 70 mph as it leaves the pitcher's hand. It's sometimes hard to tell if it was thrown on purpose, or if the pitcher just forgot how to throw the ball for a moment. This pitch is said to have first been thrown by [Bill Phillips](https://www.baseball-reference.com/players/p/phillbi02.shtml), who made the pitch a part of his game [from 1890 to 1903](https://en.wikipedia.org/wiki/Eephus_pitch). The pitch was later brought to prominence by [Rip Sewell](https://www.baseball-reference.com/players/s/sewelri01.shtml) roughly 40 years later, and has seen sporatic use since. This pitch has gone by a variety of names over the years, including being referred to as a "junk pitch", a "dead fish", a "LaLob", and a "spaceball" for its high arch [source: A Brief History of the Eephus Pitch - NYTimes](https://bats.blogs.nytimes.com/2008/07/30/a-brief-history-of-the-eephus-pitch/).

Well below the speed of an average changeup, and lacking any element of deception of it being a normal pitch, why does anyone throw this bizarre pitch? The prevailing theory is that the comically slow speed of this pitch throws off a batter's calibration, making the pitches that follow appear blazing fast. In other instances, people speculate that the pitch is simply a mistake, having slipped out of the pitcher's hand. Regardless, little research has been done to date on this strange and rare pitch, so this post is going to serve as a deepdive and exploratory analysis of the mythical eephus. 

Before going any further in this post, here's some quick suggested viewing for context on the big league pitch that you could probably throw just as well as Clayton Kershaw:

[![Eephus Pitch Compilation](/images/fulls/eephus_youtube.png)](https://www.youtube.com/watch?v=QwP2U7lS28o)

Now that this pitch has received a suffieicent amount of hype, let's get up close and personal with the eephus pitch and see what it looks like by the numbers. To do this we'll need data on every eephus that's been thrown. For this, I used the [pybaseball](https://github.com/jldbc/pybaseball) module to retrieve the Statcast and Pitch FX data on every Major League pitch that's been thrown since the 2008 season. Among these 7,212,136 observations, only 2,090 of them represent eephus pitches. That's just 0.02 percent. A rare pitch indeed!

Since data on any particular pitch type is only relevalt in the context of other pitches, we'll first compare the eephus against the closest things it has to peers: the fastball, knuckleball, and changeup.

<p align = "center">
    <img src="/images/fulls/eephus_summary.png" alt>
</p>

The most relevalt data point here is speed: the eephus has an average speed of just 64.5mph. That's 23% slower than the average hangeup, and 30% slower than the average fastball. While the pitch's defining characteristic is its slow speed, however, it doesn't demonstrate the same low spin rate of other purposefully slow pitches. While the knuckeball and changeup show spin rates in the 1500s and 1700s, the eephus spins at a lofty 2301 rpm - a solid 100rpm faster than the average fastball. As spin rate is a realtively new metric to have access to, the experts aren't completely certain what exactly a high or low spin rate means for pitch quality. Early research, however, suggests that [a high spin rate is a good thing](http://m.mlb.com/news/article/212735620/what-statcast-spin-rate-means-for-fastballs/) for a non-breaking ball.


<p align = "center">
    <img src="/images/fulls/statcast_zones.png" alt>
</p>

The last summary stat is the percentage of each pitch type that's placed down the middle of the strike zone, along the edges, and outside the zone. Here I use the statcast zones shown above, defining "down the middle" as being in zone 5, "edge of strike zone" as zones 1, 2, 3, 4, 6, 7, 8, and 9, and "outside strikezone" as zones 11 through 14. At a high level, the farther pitches tend to be placed from the middle of the strike zone, the more likely it is that pitchers are using this pitch for strategic reasons and the less likely it is that a pitcher is confident at the pitch's ability to get past a batter without being expertly placed. Here we see about what we'd expect. Fastballs and knuckleballs are placed within the strike zone relatively more often than the slow-speed changeup and eephus, with the eephus being thrown outside the strike zone 2% more often than the changeup and 12% more often than the fastball. This makes intuitive sense, since one can imagine that a well-prepared power hitter could do some damage to a 60mph pitch thrown down the middle. Due to the eephus' high arch, it may be challenging to place accurately as well, which would also contribute to how often it lands outside the strike zone. 

While summary stats are useful, a simple average never tells the full story. To better understand baseball's slowest pitch, let's take a look at how its release speeds are distributed relative to these other pitches. 

<p align = "center">
    <img src="/images/fulls/speed_dist.png" alt>
</p>
From this figure we can see that the eephus' slowness is even more pronounced than one may have thought! In fact, if we throw out the fastest 1% of eephus pitches which are outliers that appear to have been misclassified, we see that the remaining 99% of recorded eephus pitches are slower than 97% of recorded changeups. So while there is *some* overlap between the two pitches in terms of speed, the eephus is essentially in a league of its own in terms of slowness. 

The speed gap between the eephus and the fastball is even more pronounced. One can imagine how disorienting it would be to see an eephus float by after a 95mph fastball, or how blazingly fast this same fastball would look after a 60mph eephus pitch. As a side note, the bi-modality of knuckleball speeds suggests that Statcast may be miscalssifying some of these pitches as knuckleballs when they're actually eephuses. Since there's no accurate way of saying which declared-knuckleballs are actually eephuses, however, we'll have to leave those pitches be.

This brings us to a more practical question: *does the eephus actually work?* The most salient argument for its use is the one aluded to above, that the extreme speed differential between an eephus and any other pitch makes the non-eephus options of a pitcher's repertoir seem faster and harder to track, and therefore more effective. But does this theory hold up in practice? Let's examine the effectiveness of the eephus vs. a few more common pitches, and then test whether an eephus actually makes the following pitch harder to hit. 

[[ eephus success metrics -> fastball success metrics -> eephus in atbat success metrics vs everything else success metrics -> fastball-after-eephus success vs. standard fastball effectieness. ]]

For examining the effectiveness of the eephus vs. all other pitches, I'll look at five metrics: contact percentage, hit percentage, launch angle, exit velocity, and barrel percent. These metrics collectively represent how hittable the pitch is, how high quality eephus hits tend to be, and whether people hit the eephus for power or for contact. 

<p align = "center">
    <img src="/images/fulls/hitability_stats.png" alt>
</p>
[[analyze this]]


<p align = "center">
    <img src="/images/fulls/speeds.png" alt><img src="/images/fulls/angles.png" alt>
</p>
Moving from the pitch itself to its hollistic impact on an atbat, let's take a look at the on base and slugging percentage of an eephus-containing atbat vs. an average one. 

[[ do this ]]

Last, let's test the exact theory posed earlier; is a fastball harder to hit after an eephus? 

[[ do this ]]