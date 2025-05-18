---
title: "Making this Hugo Site"
description: "Walking through the bits of how I made this site."
layout: "single"
draft: false
date: 2025-04-18T15:04:05Z
tags: ["Programming"]
coverCaption: "Photo by Alex Knight on Upsplash"
coverAlt: "An image of a computer on a table with a coffee next to it."
featureAlt: "Photo by Alex Knight on Upsplash"
thumbnailAlt: "An image of a computer on a table with a coffee next to it."
---



Hello there! I built this site in Hugo and this post is to keep track of what I did, so a.) I can remember what I did and b.) so someone else can follow along in case they like my site and want to recreate it.

## Why Hugo? 

I built my first website an a now discontinued product called iWeb, which came built in on a Mac computer. It was perfect for what it was at the time, drag and drop boxes, built in themes, etc. I was dismayed when it was discontinued and moved to Wordpress.org.

WordPress was interesting to learn, and I somewhat enjoyed it. After they moved to "blocks", a bit less so. 😊 I found that I was always searching for themes that I didn't really love, and it felt large and bloated, and was really a bit too much for what I was needed. Life got busy and the thought of moving off of Wordpress felt overwhelming and there was always something more important to do.

As I became a daily programmer, and as part of my work in open data, open source, and the Missing Maps ecosystem, I discovered static site generators. My first go was with Jekyll, where I built a [prototype](https://www.missingmaps.org/missing-maps-website/) of a new website for Missing Maps, using the [Dogwood theme](https://github.com/osmus/dogwood).

When it came time to move off Wordpress and also to bring my website into the present day, I had been hearing a lot about Hugo, and it's revolutionary build times and modern feel. I thought it would be fun to learn and experiment with. And it has been! While there has been some initial struggles here and there with learning Hugo's quirks, I find it fun to work on my website while using Hugo, and I am very excited I found it!

## Getting Started

If you are new to Hugo, I would highly recommend this [Giraffe Academy YouTube course](https://youtube.com/playlist?list=PLLAZ4kZ9dFpOnyRlyS-liKL5ReHDcj4G3&feature=shared) and follow along. It was very helpful in getting used to the specific Hugo terminology and how the overrides and directory structures work. 

## Rules of the Game

If you are just getting started in Hugo, and you are using a predefined theme, it's important to note that there are general rules that Hugo follows, and there are also rules that the theme you chose follows. These may or may not be the same! This can be incredibly confusing at the start and each set of docs seems to contradict each other and can keep you up all night.

{{< alert >}}
**Important!** Do not panic! Sleep on it for a night. Go to a yoga class. Have a friend look it over with you. It DOES get easier!! 
{{< /alert >}}

## The Congo Hugo Theme

I chose the [Congo theme](https://github.com/jpanther/congo) because it had the simplicity I wanted, seemed to be updated regularly, and had [good documentation](https://jpanther.github.io/congo/docs/). It's made by a person named [James Panther](https://jamespanther.com/), who is also a lighting designer, digital privacy advocate, and food lover. 

## Installation

I was still relatively new to Hugo when I started making this website. I decided to [install the Congo theme](https://jpanther.github.io/congo/docs/installation/) as a [Hugo module](https://gohugo.io/hugo-modules/use-modules/), since that was what was recommended. The Hugo module seems to make it the easiest to keep the theme up to date in the future, but it does makes things a bit abstract in the present, since you can't actually "see" the theme in your directory. Which means if you want to override anything, you need to be a bit patient in figuring it out. 

When installing a theme using Hugo modules, you should NEVER mess with the theme files. This will make it difficult to update later. You should using a system of overwriting to get what you want in your own layout directory. I found [this page](https://jpanther.github.io/congo/docs/advanced-customisation/) helpful. 

When installing as a Hugo module, you essentially copy the files over from your computer's cache into a config folder, and your theme folder will remain empty. You also end up with some Go files in your directory. 

Because, when you install as a Hugo module, you can't actually "see" the theme in your project, I suggest looking at the [layout files on the Congo Github](https://github.com/jpanther/congo/tree/dev/layouts) to understand how they are programmed. This will especially come in handy if you want to override something in the theme to make the site more your own.


## Creating Files Across the Site

Structure is everything in Hugo. In order to make the nav bar items, I created a folder for each nave item (except the about page - that's at the root.) Each folder should then have an _index.md in them to create that topic's landing page. You can add some text on this page to give a summary of what that landing page will contain. Then, each item on the landing page has it's own folder with it's own index.md inside (note the lack of the _ !) which makes it a single format instead of a list format. This is what makes the page feel like a page and less of an "index" of other pages. Hurrah! 

Any images you want to go with your pages will be inside of that folder with the index.md. If you want it to be a cover image, you can put the word "feature" somewhere in the title of that image and Congo will pull it in directly. If you have a lot of images, you might consider putting them in another folder called images and you can keep things organized and link from there. Make sure your paths are correct! If you have any global images, you can also put them in the static folder (like a logo that goes across your site, etc.), however, you then lose the responsiveness factor that comes with Hugo bundles. 

The setup of Hugo does make it feel like you have 15 index.md ages and 15 _index.md pages, all nested in various folders, which to me felt dizzying at the start, but one does start to get used to it.. 

Your home page is always the main _index.md file in your directory. I added the "Learn More" at the bottom of my home page by adding the a button and function to that file. 

## Getting 0001 Off the List Pages

In the Congo theme, by default the single pages are grouped by year on the index pages. If you don't set a year, this will automatically be set to the year of 0001, which means that this will end up as the first entry on any of your single pages listed on the index page. To get rid of this, you can set groupByYear = false in the params.toml file in the [list] section.

## Small Thumbnails Featured on the List Pages

If you want each of your _index pages to have a list of icons next to the directories listed on that page, you need to put an image file in the root of each directory, and it needs to have "feature" written somewhere in the image name.

## The Cascade

If you want the same features to be true on each of your pages in any given section (i.e. you want each article to show up under "Projects" or you don't want to show the author on each page), you can create a cascade on the _index.md file for that section. This makes it so you don't need to repeat yourself then putting each of these in the front matter of each page. 

Here is the cascade for the _index.md file for my Projects section.

```yaml
title: "Projects"
cascade:
  categories: ["Projects"]
  showAuthor: false
  showPagination: false
```
{{< alert >}}
**Important!** If you want to use the cascade, the _index pages for the sections will also inherit the category. 
{{< /alert >}}

This means that the list pages will also show up on your categories page, which might look odd. If you want to avoid this, you'll need to add an empty array to the category in the front matter of these list pages.

Like so:

```yaml
categories: []
cascade:
  categories: ["Projects"]  
```
This makes the actual _index file NOT inherit the category, but all the child pages will. 

Do note that it's best to use the cascade for any parts of the theme you want to overwrite - for example, if there is one section that you want to have certain features on. If you're looking to set something the same across the entire site, it's more efficient to set these in the params.toml config file.

## To Get Rid of the Dates on Only Some _index Pages

 You need to override the theme by adding a layouts/partials/article-meta.html file and make sure you add the list page page on which you want to get rid of the dates. In my case, it was the "spaces" list page that I didn't want to include the dates on.

 So this:

 ```go
 {{ if .Params.showDate | default (.Site.Params.article.showDate | default true) }}
  {{ $meta.Add "partials" (slice (partial "meta/date.html" .Date)) }}
{{ end }}
```

 Changes to this: 

  ```go
  {{ if not (or (hasPrefix .File.Dir "spaces/") (eq .File.BaseFileName "_index.md")) }}
  {{ if .Params.showDate | default (.Site.Params.article.showDate | default true) }}
    {{ $meta.Add "partials" (slice (partial "meta/date.html" .Date)) }}
  {{ end }}
{{ end }}
```
## Switching Out the Light Mode Icon from the Sun to the Light Bulb

A friend commented that the sun icon to change from dark to light mode looked like a gear icon instead of a sun. I didn't disagree. She suggested I swap it out for a lightbulb icon instead.

Here is how I did it: 

I saw that there was a [lightbulb icon](https://github.com/jpanther/congo/blob/343ba2a4ae2b7cfec5a0873320e075c894bff304/assets/icons/lightbulb.svg) in the assets directory of Congo in Github. I downloaded that and added it to my own assets/icons directory.

I then did a search of the Congo Github repo for any mentions of "sun."

That included the following pages:

- The [hybrid header](https://github.com/jpanther/congo/blob/343ba2a4ae2b7cfec5a0873320e075c894bff304/layouts/partials/header/hybrid.html#L78) (what I chose for my instance)
- The [basic header](https://github.com/jpanther/congo/blob/dev/layouts/partials/header/basic.html)
- The [footer.html](https://github.com/jpanther/congo/blob/dev/layouts/partials/footer.html)

In these files, I swapped out any mention of "sun" with "lightbulb." The basic file had one and the hybrid and footer files had two. 

## Putting the Appearance Switcher in the Header

If you want your appearance switcher in the header, as opposed to the footer, you'll need to do the following:

1.) Set the showAppearanceSwitcher in the params.toml to false
2.) Add this to your menus.en.toml

```yaml
- identifier: "appearance"
    weight: 99
    params:
      action: "appearance"
```

## Deployment to Github Pages with a Custom URL

First, in the config file, make sure you set the baseURL to your custom domain, making sure to include the / at the end.

```bash
baseURL = "https://www.nicolesiggins.com/"
```

You'll also want to add a CNAME file to your static folder.

```bash
echo "www.nicolesiggins.com" > static/CNAME
```

When you want to develop locally and change your site, you can run the following:

```bash
hugo server --baseURL http://localhost:1313/
```

Or, you can create a script that you can run at the root directory. I made a file called serve.sh at the root of my project. Inside I put the following:

```bash
#!/bin/bash
hugo server --baseURL http://localhost:1313/ --disableFastRender
```

Then, when I want to develop locally, I run the following to view it on the local host:

```bash
./serve.sh
```

You'll also want to create a .gitignore file at the root of your project. If you're not sure how to get started, [this website](https://www.toptal.com/developers/gitignore) can help. You can add your operating system, any frameworks you are using, as well as your IDE.

To deploy on Github, you'll need to create a deploy.yml file in side of .github/workflows, which should sit in the root of your project.

Here is the workflow I decided upon: 

```yaml
name: Deploy Hugo site to GitHub Pages

on:
  push:
    branches:
      - main  

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout source
        uses: actions/checkout@v3

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: '0.123.8'
          extended: true

      - name: Cache Hugo modules
        uses: actions/cache@v3
        with:
          path: ~/.cache/hugo
          key: ${{ runner.os }}-hugo-${{ hashFiles('**/go.sum') }}
          restore-keys: |
            ${{ runner.os }}-hugo-

      - name: Install dependencies (for Hugo Modules)
        run: hugo mod tidy

      - name: Build the site
        run: hugo --minify

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

It's important that once you push your site to Github, that you ensure that your permissions for the repo are correct, otherwise the Github actions won't be able to resolve.

For the repo you want to deploy, go to Settings > Actions > General > Workflow permissions, and make sure that the "Read and write permissions" button is selected. And remember to save!

You'll then need to make a small change to your site, and push again to Github, so that workflow can run, and create the gh-pages branch for you.

Once this happens, you'll need to get Github Pages set up.

Go to Settings > Pages > Build and Development and choose "Deploy from a branch." Choose gh-pages and leave it set as /root.

Further down the page you can add your custom domain. You'll also need to make sure your DNS records / name servers are correct for Github at your domain registrar. My registrar is [Porkbun](https://porkbun.com/), who had a nifty little button for Github, that got this set up for me.

I hope this helps! 

## Got any feedback?

Please get in touch! I'm learning as I go and appreciate any tips and tricks! 😊