---
title: "Building the Corporate Commands Research Database"
description: "Walking through the bits of how I built the corporate commands research database."
layout: "single"
draft: false
date: 2025-08-15T15:04:05Z
tags: ["Programming"]
coverCaption: "The corporate commands research database is alive again!"
coverAlt: "A screenshot of the corporate commands research database."
featureAlt: "The corporate commands research database is alive again!"
thumbnailAlt: "A screenshot of the corporate commands research database."
---

I built an archival research database for the Corporate Commands project by The Institute for Infinitely Small things, an art and research group who conduct creative, participatory research that aims to temporarily transform public spaces and instigate dialogue about democracy, spatial justice and everyday life. The Institute's projects use performance, conversation and unexpected interventions to investigate social and political "tiny things". Corporate Commands was always one of my favorite institute projects, so I thought it would be fun to get our research database of corporate commands back up online. 

I decided to build the site in Hugo, using the Blowfish theme, which is a fork of the Congo them, with some enhancements. Because I also built the [Institute archive](https://www.infinitelysmallthings.net/) in Blowfish, I wanted to use the same theme for the corporate commands research database, so that the websites would link together aesthetically. 

I also wanted to keep track of any adjustments I made to the theme so that I a.) would be able to remember how I did stuff and b.) in case anyone else wanted to build a Hugo site with Blowfish and wanted to know how I did certain things.

So here goes! 😊

## How to change the header to show the author as opposed to the site name

Because this is meant to be a database for the Institute for Infinitely Small Things, I wanted the both the copyright and the name in the header of the site to show this name (the site author), but I wanted the actual title of the site to be The International Database of Corporate Commands (and I wanted to this to show up on the top tab). The Blowfish theme has all of these items listed as the site title, so I needed to adjust some of the code. 

Here's how I did it: 

Create the file in layouts/partials/header/basic.html and copy the contents into it [from the theme](https://github.com/nunocoracao/blowfish/blob/main/layouts/partials/header/basic.html). 

In the nav, where it says {{ .Site.Title | markdownify }}, you want to change this to .Site.Params.author.name. 

So this:

````go
 <nav class="flex space-x-3">
      {{ if not .Site.Params.disableTextInHeader | default true }}
        <a href="{{ "" | relLangURL }}" class="text-base font-medium text-gray-500 hover:text-gray-900">
          {{ .Site.Title | markdownify }}
        </a>
      {{ end }}
    </nav>
````

Becomes:


````go
 <nav class="flex space-x-3">
      {{ if not .Site.Params.disableTextInHeader | default true }}
        <a href="{{ "" | relLangURL }}" class="text-base font-medium text-gray-500 hover:text-gray-900">
          {{ .Site.Params.author.name | markdownify }}
        </a>
      {{ end }}
    </nav>
````

## How to remove the site author name from the hero on the homepage

Blowfish has a very cool thing where it shows the site author as a overlay over the hero image on the homepage when the profile page is in the hero layout. This could be very cool, but because I not only wanted this overlay to be the site title and not the site author, but also because I was also using an image that had the site name in the image, it didn't make sense for me to keep any text here, especially the site author name. So I decided to fully remove it. Here's how I did it. 

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

Once you comment both of these out, the site author will no longer appear over the top of the hero image on the homepage. 

## Making the hero image on the homepage clickable

I wanted to make the hero image on the homepage clickable, and have it lead to the research database itself. To do this, you must first add a parameter to your params.toml page:

````bash
homepageImageLink = "/research-database/"
````

Then, make your way into the layouts/partials/home/hero.html file inside of your own repository (this was created in the last point, so if you didn't do that then, you'll need to create the folder and file in own your repo first. Don't forget to add in the original code!)

Locate this line:

````html
<img class="h-full w-full object-cover nozoom mt-0 mr-0 mb-0 ml-0" src="{{ $homepageImage.RelPermalink }}">
````

and replace it with: 

````html
<a href="{{ .Site.Params.homepage.homepageImageLink | relURL }}" class="absolute inset-0 z-10"> <img class="h-full w-full object-cover nozoom mt-0 mr-0 mb-0 ml-0" src="{{ $homepageImage.RelPermalink }}"> </a>
````

Lastly, in order to actually make the image clickable, make sure to add "pointer-events-none" to the front of the following two divs, like so:

````html
  <div
  class="pointer-events-none absolute inset-0 bg-gradient-to-r from-primary-500 to-secondary-600 dark:from-primary-600 dark:to-secondary-800 mix-blend-multiply"></div>
````

````html
<div
class="pointer-events-none inset-0 from-primary-500 to-secondary-600 dark:from-primary-600 dark:to-secondary-800 mix-blend-multiply"></div>
````

This makes the element invisible to the mouse, so that it becomes clickable when you hover over it. Hooray! :) 

## How I got the images that fit perfectly in the hero and page headers. 

If you want to create images with text that work perfectly for the hero on the home page as well as the individual pages, you can use this script, just swap out the text for what you want.

{{< alert >}}
This script is for a Mac computer, and has a Mac safe font included.
{{< /alert >}}

````bash
from PIL import Image, ImageDraw, ImageFont

# Define text and layout
text = "THE INTERNATIONAL DATABASE\nOF CORPORATE COMMANDS"

# Font setup (adjust if needed)
try:
    font_path = "/System/Library/Fonts/Supplemental/Arial Bold.ttf"  # Mac safe font
except:
    font_path = None

# Output sizes
sizes = {
    "homepage_hero": (1600, 600),
    "individual_page": (1200, 630)
}

# Generate images
for name, (width, height) in sizes.items():
    # Set font size based on image height (roughly 25–30%)
    font_size = int(height * 0.25)
    if font_path:
        font = ImageFont.truetype(font_path, font_size)
    else:
        font = ImageFont.load_default()

    img = Image.new("RGB", (width, height), "black")
    draw = ImageDraw.Draw(img)

    # Reduce font size until text fits
    while True:
        bbox = draw.multiline_textbbox((0, 0), text, font=font, spacing=10)
        text_width = bbox[2] - bbox[0]
        text_height = bbox[3] - bbox[1]
        if text_width < width * 0.9 and text_height < height * 0.8:
            break
        font_size -= 2
        font = ImageFont.truetype(font_path, font_size)

    # Center text
    x = (width - text_width) / 2
    y = (height - text_height) / 2
    draw.multiline_text((x, y), text, font=font, fill="white", align="center", spacing=10)

    img.save(f"{name}_feature.png")

print("Images saved with properly scaled text.")
````

## Got any feedback?

Please get in touch! I'm learning as I go and appreciate any tips and tricks! 😊