---
title: "마지막 서치 테스트 및 486"
description: "Desc Text."
draft: false
date: 2022-03-31T20:13:16+09:00
series: ["the very first"]
categories: ["test list"]
tags: ["test"]
images: ["/images/testforblog.png"]
---

{{< figure src="/images/testforblog.png" title="test image 입니다" width=500 >}}
{{<line_break>}}
Shows Index/Home page as Full Page with Social Links and Image

add following to config file

# asdf

asdfjsalkffff

asdfkjlsd

asdlkfjlsa

imageWidth: 120 # custom size
imageHeight: 120 # custom size
buttons: - name: Archive
url: "/archive" - name: Github
url: "https://github.com/"

```yaml
    socialIcons: # optional
        - name: "<platform>"
            url: "<link>"
        - name: "<platform 2>"
            url: "<link2>"
```

Search Page
PaperMod uses Fuse.js Basic for seach functionality

Add the following to site config, config.yml

outputs:
home: - HTML - RSS - JSON # is necessary
