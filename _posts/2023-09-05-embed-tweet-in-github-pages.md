---
title:  "How to embed a tweet in GitHub Pages (2023)"
date:   2022-09-05
tags: 
  - "blogging"
---
Although there are plugins for jekyll to do that, However it is not enabled in GitHub Pages due to security concerns.

But there is still a way to do that:
In order to embed a tweet in your markdown file for GitHub Pages, do this:

1. Open the tweet you want to embed in twitter (recently X.com):
2. Click on the `...` button on the top-right side of the tweet:
![How to embed a tweet in GitHub Pages - Step 1](/img/posts/embed-tweet-1.png)
3. Select `Embed Post`
![How to embed a tweet in GitHub Pages - Step 2](/img/posts/embed-tweet-2.png)
4. It opens that tweet in `publish.twitter.com` where you can copy the embed code
![How to embed a tweet in GitHub Pages - Step 3](/img/posts/embed-tweet-3.png)
5. Click `Copy Code` and copy this code directly in your *Markdown* file. You can paste a html blockquote in your markdown file, and it will be rendered exactly the same in your output HTML file.

This is an example of the same tweet above, embedded here:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Which frontend or backend framework will make you instantly hireable? 🤔</p>&mdash; Arman 💻 (@programmerByDay) <a href="https://twitter.com/programmerByDay/status/1698818446795145521?ref_src=twsrc%5Etfw">September 4, 2023</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>


There you go! As easy as that :) 