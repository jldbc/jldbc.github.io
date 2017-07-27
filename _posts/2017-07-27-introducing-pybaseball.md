---
title: "Introducing pybaseball: an Open Source Package for Baseball Data Analysis"
layout: post
categories: projects open-source
excerpt: Throughout my baseball-facing work at MLB Advanced Media, I came to realize that there was no reliable Python tool available for sabermetric research and advanced baseball statistics. As a response to this, I built pybaseball - a Python package for baseball data analysis.
---

Baseball and statistics go together like peanut butter and jelly; it's almost hard to imagine following one without involving the other. In recent years, the data that make this game enjoyable for so many have only gotten better. With the introduction of the [Statcast](http://m.mlb.com/statcast/leaderboard){:target="_blank"} system for measuring sci-fi-sounding statistics such as the spin speed of a thrown ball and its launch angle off a player's bat, I believe we are at the beginning of an exciting new era for baseball statistics. 

Unfortunately for Python-loving statisticians like myself, there has historically been no tool for bringing this data into one's work without a painful process of manual curation. For this reason, I'm releasing pybaseball: an open source package for 21st century baseball data analysis in Python. 

<p align = "center">
    <img src="/images/fulls/judge-derby-mlbdotcom.jpg" alt>
</p>
<p align="center">
    <em align="center">How does Aaron Judge hit baseballs into the stratosphere? Pybaseball and Statcast can help you find out (image: mlb.com)</em>
</p>

# What It Does
Pybaseball takes the pain out of collecting and cleaning baseball data from the internet. In short, I scraped [Baseball Savant](https://baseballsavant.mlb.com/statcast_leaderboard){:target="_blank"}, [FanGraphs](http://www.fangraphs.com/leaders.aspx?pos=all&stats=pit&lg=all&qual=y&type=8&season=2017&month=0&season1=2017&ind=0){:target="_blank"}, and [Baseball Reference](https://www.baseball-reference.com/){:target="_blank"} so you don't have to. Currently, this means that you can retrieve season and game-level data on individual players and teams, historic schedule and record data, and division standings with simple, Pythonic one-liners. The stats that this library provides range from the classics (BA, RBI, HR, W, L, K, IP), to the slightly more sophisticated (OBP, SLG, WHIP, WAR), to what would have sounded like science fiction a few short years ago (exit velocity, spin speed, pitch x, y, and z coordinates). The goal of this library is to provide the data necessary to answer any baseball research question. 

# How it Works
The `statcast` function returns statcast pitch-level data. 

<pre>
  <code class="python">
>>> from pybaseball import statcast 
>>> data = statcast(start_dt='2017-06-15', end_dt='2017-06-28')
>>> data.head(2)  
   index pitch_type  game_date  release_speed  release_pos_x  release_pos_z  
0    314         CU 2017-06-27           79.7        -1.3441         5.4075
1    332         FF 2017-06-27           98.1        -1.3547         5.4196

  player_name    batter   pitcher     events     ...      release_pos_y  
0   Matt Bush  608070.0  456713.0  field_out     ...            54.8585
1   Matt Bush  429665.0  456713.0  field_out     ...            54.3470

   estimated_ba_using_speedangle  estimated_woba_using_speedangle  woba_value  
0                          0.100                            0.137         0.0
1                          0.269                            0.258         0.0

   woba_denom babip_value iso_value launch_speed_angle at_bat_number pitch_number  
0         1.0         0.0       0.0                3.0          64.0          1.0
1         1.0         0.0       0.0                3.0          63.0          3.0  
[2 rows x 79 columns]
  </code>
</pre>

Similarly, if you want player-level stats aggregated by season, you can pull 299 different features per player per season from FanGraphs using the `pitching_stats` and `batting_stats` functions. 

<pre>
  <code class="python">
>>> from pybaseball import pitching_stats
>>> data = pitching_stats(2012, 2016)
>>> data.head()
     Season             Name     Team   Age     W    L   ERA  WAR     G    GS  
336  2015.0  Clayton Kershaw  Dodgers  27.0  16.0  7.0  2.13  8.6  33.0  33.0
236  2014.0  Clayton Kershaw  Dodgers  26.0  21.0  3.0  1.77  7.6  27.0  27.0
472  2014.0     Corey Kluber  Indians  28.0  18.0  9.0  2.44  7.4  34.0  34.0
235  2015.0     Jake Arrieta     Cubs  29.0  22.0  6.0  1.77  7.3  33.0  33.0
256  2013.0  Clayton Kershaw  Dodgers  25.0  16.0  9.0  1.83  7.1  33.0  33.0

       ...      wSL/C (pi)  wXX/C (pi)  O-Swing% (pi)  Z-Swing% (pi)  
336    ...            1.76       22.85          0.364          0.665
236    ...            2.62         NaN          0.371          0.670
472    ...            3.92         NaN          0.336          0.598
235    ...            2.42         NaN          0.329          0.618
256    ...            0.74         NaN          0.339          0.635

     Swing% (pi)  O-Contact% (pi)  Z-Contact% (pi)  Contact% (pi)  Zone% (pi)  
336        0.511            0.478            0.811          0.689       0.487
236        0.525            0.536            0.831          0.730       0.515
472        0.468            0.485            0.886          0.744       0.505
235        0.468            0.595            0.856          0.762       0.483
256        0.484            0.563            0.873          0.763       0.492

     Pace (pi)
336       23.4
236       23.7
472       24.6
235       23.3
256       23.4

[5 rows x 299 columns]

  </code>
</pre>

But wait, there's more! Say you're interested in comparing the performances of historic teams. That, too, is easy with pybaseball. With this package, one can disect the 1927 "Murderers Row" Yankees season with a single line of Python. 

<pre>
  <code class="python">
>>> from pybaseball import schedule_and_record
>>> data = schedule_and_record(1927, 'NYY')
>>> data.head()
                Date   Tm Home_Away  Opp W/L     R   RA   Inn  W-L  Rank  \
1    Tuesday, Apr 12  NYY      Home  PHA   W   8.0  3.0   9.0  1-0   1.0
2  Wednesday, Apr 13  NYY      Home  PHA   W  10.0  4.0   9.0  2-0   1.0
3   Thursday, Apr 14  NYY      Home  PHA   T   9.0  9.0  10.0  2-0   1.0
4     Friday, Apr 15  NYY      Home  PHA   W   6.0  3.0   9.0  3-0   1.0
5   Saturday, Apr 16  NYY      Home  BOS   W   5.0  2.0   9.0  4-0   1.0

       GB      Win     Loss  Save  Time D/N  Attendance  Streak
1    Tied     Hoyt    Grove  None  2:05   D     72000.0       1
2  up 0.5  Ruether     Gray  None  2:15   D      8000.0       2
3    Tied     None     None  None  2:50   D      9000.0       2
4    Tied  Pennock    Ehmke  None  2:27   D     16000.0       3
5  up 1.0  Shocker  Ruffing  None  2:05   D     25000.0       4

  </code>
</pre>

These examples are just the tip of the iceberg, but hopefully this gives a taste of the power and versatility of pybaseball. 

# How to Install Pybaseball
Pybaseball is pip installable. Simply run `pip install pybaseball` and it's on your machine.

# Where to Read More
If any of this piqued your interest, full documentation and complete examples are available on the Github repo [here](http://github.com/jldbc/pybaseball){:target="_blank"}. If you like what you've seen so far, please give it a star. If you __really__ like what you've seen so far, drop me a suggestion or submit a code improvement. Last, if you end up using pybaseball for any type of project or analysis, I would love to hear about it. [Send me a note](mailto:ledoux.james.r@gmail.com) or reach out [on Twitter](http://twitter.com/jmzledoux){:target="_blank"}!

<div>
      <script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

  ga('create', 'UA-52953508-1', 'auto');
  ga('send', 'pageview');

</script>
</div>


