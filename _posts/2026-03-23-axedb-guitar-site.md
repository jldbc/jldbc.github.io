---
title: "AxeDB: Guitar Pricing Intelligence"
layout: posts
categories: projects
usemathjax: true
classes: wide
date: 2026-03-23
last_modified_at: 2026-03-23
excerpt: New project for studying the used and vintage guitar markets
---
<meta property="og:image" content="/images/fulls/axedb-listing-page.png">
<meta property="og:image:type" content="image/png">
<meta property="og:image:width" content="200">
<meta property="og:image:height" content="200">
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:site" content="@ledoux_james">
<meta name="twitter:creator" content="@ledoux_james">
<meta name="twitter:title" content="AxeDB: Guitar Pricing Intelligence">
<meta name="twitter:image" content="http://jamesrledoux.com/images/fulls/axedb-listing-page.png">

I've come out of side project retirement for something I'm calling [AxeDB](https://axedb.com/). AxeDB is a platform for vintage and used guitar pricing intelligence. Using data from millions of used guitar sales, it shows pricing trends on specific current and historic models and serves as a platform for research and analysis to quantify what's previously been a largely qualitative domain.

# Why AxeDB
I built AxeDB because it's the kind of niche website I wished existed for my own music gear hobby. As an amateur musician, gear nerd, and data scientist, I find myself browsing Reverb and YouTube guitar content for both the gear and the market aspect. Yes, I like to look at new and vintage instruments, pedals, amps, etc., listen to demos, and ask myself if I need a new piece of gear (I don't.) But I also see a vintage Blackguard Telecaster sell for the price of a midwestern starter home and like to ask myself: why's it worth that?

AxeDB is a place you can scratch that kind of itch. You can check a modern and vintage guitar sales market index like it's the S&P 500, see whether the newly released American Ultra Luxe Vintage line is trading at a discount on the secondary market yet, and read a deep dive analysis of where exactly the value comes from on that Blackguard (and how you're going to find a more affordable one for yourself one day.) It's for the musicians, the collectors, and the nerds.

# What It Does

## Model-Level Secondary Market Trends: A Tool for Buyers and Sellers

Series/Model-level views into secondary market trends. For a given model (e.g. the American Vintage II Telecaster), see how secondary market sales have trended relative to the retail price on the brand new guitar, browse live listings from Reverb and Sweetwater, and compare those listings to previous sales.

It's a great tool for scouting deals and tracking the market.

<p align = "center">
    <img src="/images/fulls/axedb-model-page.png" alt>
</p>

## Vintage and Modern-Aftermarket Market Indexes

Stock Market-style market indexes for modern and vintage guitar sales. A cross-market pulse on how the used markets are trending. 

<p align = "center">
    <img src="/images/fulls/axedb-market-index.png" alt>
</p>

## Market Research

Quantitative research on guitars, music, and instrument value. So far I've posted research on the [vintage Telecaster market](https://axedb.com/research/vintage-telecaster-market) and the [history of Fender's custom colors, refinishes, and how they affect sales price](https://axedb.com/research/fender-custom-colors-refinish-value). I plan to keep sharing research using the data foundation I've developed from tens of thousands of vintage guitar sales.

<p align = "center">
    <img src="/images/fulls/axedb-tele-market.png" alt>
</p>

## Editorial Content

Detail-heavy editorial content such as histories of the specs and provenance of famous guitars. See this example of [Cobain's Sky-Stang](https://axedb.com/famous-axes/kurt-cobain-skystang) as an example. The thought here is that, eventually, I could have a searchable catalog of every famous artist's guitars, their specs, and how you can get your own.


# Data Foundation and AI Exploration

The foundation of AxeDB is what its name implies: a database of axes (guitars). I pursued this project, in part, to practice building data and AI infrastructure from scratch and to experiment with LLMs.

I largely vibecoded the foundations of this project, relying heavily on Claude Code and Codex to develop the app and its foundational data pipelines, and using OpenAI's API for data enrichment and labeling to enhance the quality of listing and sales data collected from messy online sources. Agentic AI capabilities have gotten really impressive over the past couple months, so it was exciting to get to lean in and develop something I'm excited about with an AI-first mindset.

The result, in addition to a user-facing web app, is a fascinating data foundation that a data scientist and guitar hobbyist like myself can dig in to. AxeDB is built on top of cleaned, structured data from millions of live listings and past sales of guitars from online marketplaces, individual dealers, and auction houses. The data refreshes frequently from live sources, so the data presented on the site remains fresh and actionable to a user. It's a large and rich dataset that I hope will continue to power analyses and ML projects for a long time to come.

My hope is that the site is not only an interesting data and engineering exercise for myself, but a also powerful utility and source of entertainment to musicians and gear nerds like myself. Check it out and feel free to send me a note if you have feedback or ideas for site features or future research projects.