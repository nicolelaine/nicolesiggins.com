---
title: "2021 London Missing Maps - Making a MapComplete Theme"
description: "A talk about making a MapComplete theme for postboxes and post offices"
layout: "single"
draft: false
date: 2021-11-02
categories: ["Projects"]
tags: ["Programming", "Mapping", "OpenStreetMap", "Open Data"]
coverCaption: "The MapComplete Postbox and Post Offices Theme - displaying these features in Hamburg, Germany. 😊"
coverAlt: "An image of the Postboxes and post offices theme on the MapComplete website."
featureAlt: "The MapComplete Postbox and Post Offices Theme - displaying these features in Hamburg, Germany. 😊"
thumbnailAlt: "An image of the Postboxes and post offices theme on the MapComplete website."
---

[MapComplete](https://mapcomplete.org/) is a thematic OpenStreetMap viewer and question-based editor with the aim of being really easy to use. It hopes to get folks contributing their local knowledge to OpenStreetMap, without necessarily needing to understand the OSM tagging system. It is meant to be for easy entry and getting people excited about mapping!

I was approached by the developer of [Postcrossing](https://www.postcrossing.com/) (a truly fabulous postcard sharing and sending website that you should definitely check out!) about creating a tool that would allow would-be postcard senders to find the closest and most accessible postbox or post office in their vicinity to be able to send their cards - especially when in an unfamiliar environment, like on holiday. 

The hope was for a product that could do the following: 

- Displays a map of all the post boxes and post offices in the world - in real time...
- Has the ability to add an image of each post box or post office
- Has the ability to add new post boxes and post offices that are not yet on the map
- Be able to add the opening hours of the post offices and filter by if they are open
- Be able to add the collection times of the post boxes

I dove into the project and in the process found MapComplete. A true gem of a tool with an amazing helpful community for folks who want to make a custom theme. Everyone was so helpful as I worked my way through the ins and outs of making the theme and getting it accepted as an official theme on the MapComplete website. This means that others can now either improve on the theme, or take parts of it for their own themes. Yay open source! 

### How to make a MapComplete theme

MapComplete themes are made of a JSON file that links to other assets (such as icons, licensing, OSM data using the Overpass API). Depending on what you want to showcase, each feature must be a separate layer within the JSON file. The icons are licensed under CC-BY-4.0, are sourced from Wikimedia Commons, and attributed on the licensing page of the theme. You can also add some CSS in the lineRendering of the JSON file.

I gave a short presentation on my experience making this theme at London Missing Maps on November 2, 2021.

{{< button href="https://mapcomplete.org/postboxes.html?" target="_blank" >}}
View my theme here
{{< /button >}}

<br>
<br>

{{< button href="https://slides.com/nicolelaine/making-a-mapcomplete-theme" target="_blank" >}}
View the presentation slides
{{< /button >}}

If you have any questions about making your own MapComplete theme, please reach out. I'm happy to help you get started! 😊