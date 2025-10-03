---
title: "Building the iKatun website"
description: "Walking through the bits of how built the iKatun website."
layout: "single"
draft: false
date: 2025-09-25T15:04:05Z
tags: ["Programming"]
coverCaption: "The iKatun website is alive again!"
coverAlt: "A screenshot of the iKatun website."
featureAlt: "The iKatun website is alive again!"
thumbnailAlt: "A screenshot of the iKatun website."
---

I recently built both an archival website for the [Institute for Infinitely Small Things](https://www.infinitelysmallthings.net/), and an archive of the research database for the [Corporate Commands project](https://www.corporatecommands.com/). There was just one other website to build to tie all of this together, the [iKatun website](https://www.ikatun.org/), a non-profit based in Boston, Massachusetts, which made many of the Institute's projects possible.

I decided to build the site in Hugo, using the Blowfish theme, which is a fork of the Congo them, with some enhancements. Because both Institute website and the corporate commands research database are built with this theme, I wanted to keep the aesthetic across all three sites.

I also wanted to keep track of any adjustments I made to the theme so that I a.) would be able to remember how I did stuff and b.) in case anyone else wanted to build a Hugo site with Blowfish and wanted to know how I did certain things.

So here goes! 😊

## Getting rid of the favicon 

I didn't want the iKatun website to have any favicon presented in the head of the browser. The easiest way I found to override the Blowfish theme from showing a favicon was to add the two following files to the static folder of my project. 

````bash
static/favicon.ico
static/favicon.svg
````

And then restart the server, making sure to ignore the past cache:

````bash
hugo server --ignoreCache
````