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

I tried direct approch giraffe academy gave me for gh-pages it kinda worked but I was having issues (github was deprecating node 20 in actions soon).
Stumbled up on [GH Actions method][gh-action] in the jekyll docs after looking around. So I used the Github Actions approch (It was excruciating I am dead inside) after lots of trial and error got it to work by updating all the versions and deleting the lock file (don't forget to delete the lock files after adding it to .gitignore).

Tbh I don't really understand lot of the stuff here but got it working so here I am.

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

1. So you have 2 choices you could make this on root of your gh pages for that you have to make a repo called "\<username>.github.io", the second approach is making a repo called blog or something else. if you picked option 2 then change this baseurl in your `_config.yml` file
```yml
baseurl: "/<repo-name>"
```
2. Add `Gemfile.lock` to `.gitignore` and delete the file in your local copy

3. Go to your github repo -> `settings` -> `code and automation` -> `pages`<br> under `Build and deployment` change source to `Github Actions`<br><br>
![Build and deploy]({{site.baseurl}}/assets/images/2026-06-08-gh-actions-build-and-deployment.png)<br><br>
4. Add jekyll.yml to `.github/workflows` folder and paste this into it.

```yml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.

# Sample workflow for building and deploying a Jekyll site to GitHub Pages
name: Deploy Jekyll site to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches: ["main"]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v6
      - name: Setup Ruby
        # https://github.com/ruby/setup-ruby/releases/tag/v1.207.0
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: '4.0' # Not needed with a .ruby-version file
          bundler-cache: true # runs 'bundle install' and caches installed gems automatically
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v6
      - name: Build with Jekyll
        # Outputs to the './_site' directory by default
        run: bundle exec jekyll build --baseurl "${{ steps.pages.outputs.base_path }}"
        env:
          JEKYLL_ENV: production
      - name: Upload artifact
        # Automatically uploads an artifact from the './_site' directory by default
        uses: actions/upload-pages-artifact@v5

  # Deployment job
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v5

``` 

Finally you gonna have your blog site ready and deployed. I the future I am gonna try to use chirpy and make a cooler looking blog *with dark mode*.
Next project is probably gonna be **raytracing in one weekend** to restart my rusty math brain.


[giraffe-academy]: https://www.youtube.com/playlist?list=PLLAZ4kZ9dFpOPV5C5Ay0pHaa0RJFhcmcB
[chirpy]: https://chirpy.cotes.page/
[ruby]: https://rubyinstaller.org/
[gh-action]: https://github.com/actions/starter-workflows/blob/main/pages/jekyll.yml