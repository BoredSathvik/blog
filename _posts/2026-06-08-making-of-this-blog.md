---
layout: post
title: "Making of this Blog"
date: 2026-06-08 12:26:00 +0530
categories: programming blog
---

### Backstory
So in the making of this blog I had done lots of reasearch (mostly due to my procrastination) looked at Astro, Hugo and finally sat on Jekyll (cause gemini told me it can work directly github pages, and I am lazy). So I was looking on how to do it using docs or some other blog, that didn't workout so I looked at [the series by Giraffe Academy][giraffe-academy] (back in Tutorial Hell) it was great I recommend you watch it instead of reading this blog ;)

After Setting it up I got greedy and forgot about a principle of MVP (Most Viable Product) and decided on trying out [chirpy theme][chirpy] that went to shit, I tried to follow the tutorial on their page, but had to install docker desktop, but it kept spinning so I left it there.
Then I tried simply using it like a normal theme but it needed ruby 3.0.0, I installed ruby 4.0.5.

Now finally giving up on that back to where I started.

### What Worked
1. Installed Ruby from [rubyinstaller][ruby] (look giraffe academy tutorial for more nuance)
2. Run the following commands in cmd
```cmd
gem install jekyll bundler
```

3. Create a new project folder and cd into it and run
that should make a new project and install the dependences
```cmd
jekyll new .
bundler install
```

4. To serve your newly created Blog run this command and navigate to http://127.0.0.1:4000/
```cmd
bundler exec jekyll serve
```

Now your site is running, mess around a little, look at docs and you will learn about jekyll, (or Just watch that series).

*For my purposes of a MVP that is decent enough, we shall go **onwards** to github pages.*

Make a git repo out of this stuff and uploded to github (I am not gonna explain it, I am feeling lazy, look at series)




[giraffe-academy]: https://www.youtube.com/playlist?list=PLLAZ4kZ9dFpOPV5C5Ay0pHaa0RJFhcmcB
[chirpy]: https://chirpy.cotes.page/
[ruby]: https://rubyinstaller.org/