---
title: "Building the iKatun website"
description: "Walking through the bits of how I built the iKatun website."
layout: "single"
draft: false
date: 2025-09-25T15:04:05Z
tags: ["Programming"]
coverCaption: "The iKatun website is alive again!"
coverAlt: "A screenshot of the iKatun website."
featureAlt: "The iKatun website is alive again!"
thumbnailAlt: "A screenshot of the iKatun website."
---

I recently built both an archival website for the [Institute for Infinitely Small Things](https://www.infinitelysmallthings.net/), and an archive of the research database for the [Corporate Commands project](https://www.corporatecommands.com/). There was just one other website left to build to tie all of this together, the [iKatun website](https://www.ikatun.org/), a non-profit based in Boston, Massachusetts, which made many of the Institute's projects possible.

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

## Adding text into the header - to the right of the logo

I wanted to add the text, "In South Slavic, “katun” means “temporary village” and is used to designate seasonal communities near pastures and bodies of water" at the top of the homepage, as well as any other page on the site. Because I wanted it to be in the exact sane place, no matter where one was on the site, I added it into the header of the site.

First, I created a layouts/partials/header/basic.html file. In order to add the text and move it to the right, I changed this:

````html
<div class="main-menu flex items-center justify-between px-4 py-6 sm:px-6 gap-x-3">
  <!-- Left: Logo -->
  {{ template "HeaderLogo" . }}

  <!-- Right: Navigation -->
  {{ template "HeaderDesktopNavigation" . }}
  {{ template "HeaderMobileNavigation" . }}

  <!-- Mobile menu button -->
  {{ template "HeaderMobileMenu" . }}
</div>
````

to this:

````html
<div class="main-menu flex items-center justify-between px-4 py-6 sm:px-6 gap-x-3">
  <!-- Left: Logo -->
  {{ template "HeaderLogo" . }}

  <!-- Middle + right: nav + tagline + dark mode -->
  <div class="flex flex-1 items-center justify-end gap-x-4">
    <!-- Desktop nav links -->
    {{ template "HeaderDesktopNavigation" . }}

    <!-- Mobile nav links (hidden on desktop automatically via theme) -->
    {{ template "HeaderMobileNavigation" . }}

    <!--  Tagline  -->
    <span class="ml-auto text-xs italic text-gray-500">
      In South Slavic, “katun” means “temporary village” and is used to<br>
      designate seasonal communities near pastures and bodies of water
    </span>
  </div>

  <!-- Mobile menu button -->
  {{ template "HeaderMobileMenu" . }}
</div>
````

This wrapped the desktop and mobile navigation inside a new container, and pushed the text to the right. I also made sure to move the mobile menu button ({{ template "HeaderMobileMenu" . }}) below this new wrapper, so it sits outside the nav + tagline container.

## How to remove the site author name from the hero on the homepage

Blowfish has a very cool thing where it shows the site author as a overlay over the hero image on the homepage when the profile page is in the hero layout. In my case, because my hero was an image, I didn't want any text over the image at all. Here's how I got rid of it.

Create the file in layouts/partials/home/hero.html and copy the contents into it [from the theme](https://github.com/nunocoracao/blowfish/blob/main/layouts/partials/home/hero.html). 

There are two places that you'll want to comment out in the code. 

````html
<h1 class="mb-2 text-4xl font-extrabold text-neutral-200">
  {{ .Site.Params.Author.name | default .Site.Title }}
</h1>
````

and

````html
<h1 class="mb-2 text-4xl font-extrabold text-neutral-800 dark:text-neutral-200">
  {{ .Site.Params.Author.name | default .Site.Title }}
</h1>
````

## Adding text to the homepage below the hero image

At the root of the content folder, you'll want to create an _index.md file, which will override the homepage of your site and become the new homepage. 

On this page, I created a .homepage-text div, so that I could later style up the text to my liking (see below).

I added all the text in here, in HTML, including the hyperlinks that lead to various parts of the second page of the site.


## Custom CSS

There were a few things, stylistically, that I wanted to change about the Blowfish theme for this website. 

In your asset folder, you'll want to create a css folder with a custom.css file inside. 

In here, I first added some styling to the homepage text:

````css
.homepage-text {
    text-align: justify;      /* Center the text */
    color: #212427;         /* Change to any color */
    font-size: 1.2em;         /* Optional: adjust font size */
    max-width: 800px;         /* Optional: limit width */
    margin: 0 auto;           /* Center block if width is limited */
}
````

And because I don't include a dark mode button on this site, I also wanted to ensure that all links were underlined across the site so that they would be visible.

````css
/* Underline all links */
a {
  text-decoration: underline;
}
````

## Got any feedback?

Please get in touch! I'm learning as I go and appreciate any tips and tricks! 😊