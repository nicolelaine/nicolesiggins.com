---
title: "How to Run the MapSwipe Website Locally"
description: "A walk through tutorial on how to run the MapSwipe website locally."
layout: "single"
draft: false
date: 2025-05-15T15:22:30Z
tags: ["Programming", "MapSwipe"]
coverCaption: "The MapSwipe website in action!"
coverAlt: "A screenshot of the MapSwipe website."
featureAlt: "The MapSwipe website in action!"
thumbnailAlt: "A screenshot of the MapSwipe website."
---

A friend recently reached out and wanted to know how to run the [MapSwipe website](https://mapswipe.org/en/) locally, so he could check the format of a blog post he'd written. Good question! I had no idea. Well, now I do, and after you read this, hopefully you will too! 😊 

{{< alert >}}
These are instructions for a Mac computer running zsh. 
{{< /alert >}}

The MapSwipe website is written in Next.js. That does **not** mean that you need to install Next.js to your computer to be able to preview a blog post. Next.js is not a system wide program, it's a per project type of deal. You'll be able to install everything you need from inside the repo using yarn.

So let's start there - with checking that you have yarn installed. 

## Step 1: Make Sure You Have Yarn Installed

You can run this command from anywhere to check if you have yarn installed - you don't need to be in any specific directory.

```bash
yarn version
```

Because I didn't have it, I installed then it using the following.

```bash
npm install -g yarn
```

## Step 2: Clone the Repo to Your Computer

Cd over to where you want to the repo to live, then use SSH to clone it to your computer.

```bash
git clone git@github.com:mapswipe/website.git
```

Then cd into the directory.

## Step 3: Create the env.local File

Make sure you're in the root of the directory, and then create the .env.local file.

```bash
touch .env.local
```

## Step 4: Open the File 

I used nano to open the file.

```bash 
nano .env.local
```

Then I pasted in the following.

```bash
MAPSWIPE_API_ENDPOINT=https://apps.mapswipe.org/api/
MAPSWIPE_COMMUNITY_API_ENDPOINT=https://api.mapswipe.org/graphql/
NEXT_PUBLIC_POSTHOG_KEY=<posthog-key>
NEXT_PUBLIC_POSTHOG_HOST_API=<posthog-host-api>
```

I just kept the placeholders, as you don't need working PostHog tracking just to preview a blog post.

Close the file, making sure you save! 

## Step 5: Running the Site

From the root directory, run the following: 

```bash
yarn install 
```
------------------

Here I unfortunately ran into a hiccup, as I had a version of Node.js that was a higher version than was possible to run this project. I was running version 20.11, but needed to be running 16, 19, or 19.

That error looked like this. 

```bash
yarn install v1.22.22
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
error next-export-optimize-images@2.1.0: The engine "node" is incompatible with this module. Expected version "^16.0.0 || ^18.0.0 || ^19.0.0". Got "20.11.0"
error Found incompatible module.
info Visit https://yarnpkg.com/en/docs/cli/install for documentation about this command.
```
I temporarily switched to Node 18 by installing a Node version manager.

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

And then restarted my shell.

```bash
source ~/.nvm/nvm.sh
```

I then installed Node 18 and told the Node version manager to use that version.

```bash
nvm install 18
nvm use 18
```
Double check the Node version.

```bash
node version
```

Success! Now time to install the dependencies again.

------------------

```bash
yarn install
```

And then the following, to fetch the data.

```bash
yarn fetch-data
# This fetches latest data from MapSwipe database for projects
```
Run this to launch the site.

```bash
yarn dev
```
You'll know if you were successful if you see which port the site has launched on. In my case it was port 3020.

```bash
yarn run v1.22.22
$ mkdir -p cache
$ next dev -p 3020
- ready started server on 0.0.0.0:3020, url: http://localhost:3020
```

## Step 6: Check out the Blog Post! 

This was the local URL:

```bash
http://localhost:3020/en/blogs/2025-04-03-papua-new-guinea-swiping-to-find-airstrips/
```

## Got Any Feedback? 

Get in touch! I'm always learning as I go and would love to hear your thoughts. 😊