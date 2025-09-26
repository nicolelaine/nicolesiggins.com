---
title: "Building an Institute Archive with Blowfish"
description: "Walking through the bits of how the Institute archival website."
layout: "single"
draft: false
date: 2025-07-28T15:04:05Z
tags: ["Programming"]
coverCaption: "The Institute website is alive again!"
coverAlt: "A screenshot of the Institute website."
featureAlt: "The Institute website is alive again!"
thumbnailAlt: "A screenshot of the Institute website."
---

I created a website archive for the Institute for Infinitely Small things, an art and research group who conduct creative, participatory research that aims to temporarily transform public spaces and instigate dialogue about democracy, spatial justice and everyday life. The Institute's projects use performance, conversation and unexpected interventions to investigate social and political "tiny things".

I decided to build the site in Hugo, using the Blowfish theme, which is a fork of the Congo them, with some enhancements. Because I already knew Congo well (I built this site using it!) it was very exciting to dig into Blowfish and use it to design the archive. 

I also wanted to keep track of any adjustments I made to the theme so that I a.) would be able to remember how I did stuff and b.) in case anyone else wanted to build a Hugo site with Blowfish and wanted to know how I did certain things.

{{< button href="https://www.infinitelysmallthings.net/" target="_blank" >}}
View the website here!
{{< /button >}}

So here goes! 😊

## Removing the "Recents" text at the top of the homepage in cardView

This text pulls from the EN file in the i18n folder. I created an en.yaml file in this folder, and inserted the following:

````yaml
shortcode:
  recent_articles: ""
````

Removing the text from within the quotation marks leaves this text empty, so then nothing shows up in it's place. 

## Upping the number of cards in recents on the homepage to more than 10

I wanted to ensure that every project listed in "works" showed up under the recents area on the homepage, to give the page the grid look that I was going for. 

This required making a partial in my files under layout/partials/recent-articles.cardview.html

and replacing: 

````go 
{{ $recentArticles := 5 }}
{{ $recentArticles = .Site.Params.homepage.showRecentItems }}


<section class="w-full grid gap-4 sm:grid-cols-2 md:grid-cols-3">
  {{ range first $recentArticles (.Paginate (where .Site.RegularPages "Type" "in"
    .Site.Params.mainSections)).Pages
  }}
    {{ partial "article-link/card.html" . }}
  {{ end }}
</section>
````

with 

````go
{{ $pageSize := .Site.Params.homepage.showRecentItems | default 50 }}
{{ warnf "CARDVIEW PARTIAL USED — pageSize: %v" $pageSize }} // you can leave this part out, it's only to check that the partial being called in the override, not the one as part of the original theme

<section class="w-full grid gap-4 sm:grid-cols-2 md:grid-cols-3">
  {{ range (.Paginate (where .Site.RegularPages "Type" "in" .Site.Params.mainSections) $pageSize).Pages }}
    {{ partial "article-link/card.html" . }}
  {{ end }}
</section>
````

## If you want the topics page to have a different title at the top

I decided to keep the topics as topics, but I did call it "Browse" in the nav bar. 

In menus.en.toml I wrote the following

````yaml
[[main]]
  name = "Browse"
  pageRef = "topics"
````

and if you also wanted a different title at the top of the topics page, such as "Browse By", you would add a topics folder under content, put an _index.md in it and write the following:

````yaml
---
title: "Browse By"
---
````

## If you want to change the default favicon

Blowfish has a very cute favicon of a fish, but I wanted the Institute site to have our logo instead. 

If you want to use your own custom image for your favicon, the easiest way to do so is to go to [favicon.io](https://favicon.io/) and upload your image for conversion. When you click on the download button, get a zip folder of files with names like this:

- android-chrome-192x192.png
- android-chrome-512x512.png
- apple-touch-icon.png
- favicon-16x16.png
- favicon-32x32.png
- favicon.ico
- site.webmanifest

Upzip the folder and then drop all these files into your static folder of your site. 

In case you end up with a permission error when running your site, here is what you can do.

1. Remove the public folder from your site by running the following:

````bash
rm -rf public
````

2. Then rebuild the server from scratch:

````bash
hugo server
````

## Removing the title at the top of the page

The Blowfish theme has a title at the top of the page by default. I didn't want this, as I already have the title in the header, and I thought it looked visually redundant. To do this, you'll want to create an _index.md at the root of your content folder and put the following inside to overwrite the title to be blank.

````yaml
---
title: ""
hideTitle: true
---
````

## Got any feedback?

Please get in touch! I'm learning as I go and appreciate any tips and tricks! 😊