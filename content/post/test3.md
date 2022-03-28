---
title: "Test3"
description: "Desc Text."
date: 2022-03-25T14:36:15+09:00
draft: false
series: ["the very first"]
categories: ["test list"]
tags: ["test"]
draft: false
---

Shows Index/Home page as Full Page with Social Links and Image

add following to config file

# asdf

params:
profileMode:
enabled: true
title: "<Title>" # optional default will be site title
subtitle: "This is subtitle"
imageUrl: "<image link>" # optional
imageTitle: "<title of image as alt>" # optional
imageWidth: 120 # custom size
imageHeight: 120 # custom size
buttons: - name: Archive
url: "/archive" - name: Github
url: "https://github.com/"

    socialIcons: # optional
        - name: "<platform>"
            url: "<link>"
        - name: "<platform 2>"
            url: "<link2>"

Search Page
PaperMod uses Fuse.js Basic for seach functionality

Add the following to site config, config.yml

outputs:
home: - HTML - RSS - JSON # is necessary
