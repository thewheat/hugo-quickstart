---
title: "My First Post"
date: 2023-01-14T08:47:11+08:00
draft: false
---

# Hello

Test 

https://gohugo.io/getting-started/quick-start/

```
hugo new site quickstart
cd quickstart
git init
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke themes/ananke
echo "theme = 'ananke'" >> config.toml
hugo server
```

```
hugo new posts/my-first-post.md
```


https://gohugo.io/hosting-and-deployment/hosting-on-github/

`github/workflows/gh-pages.yml`
```
name: github pages

on:
  push:
    branches:
      - main  # Set a branch that will trigger a deployment
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v3
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          # extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: github.ref == 'refs/heads/main'
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

```
GitHub pages setting

By default, the GitHub action pushes the generated content to the gh-pages branch. This means GitHub has to serve your gh-pages branch as a GitHub Pages branch. You can change this setting by going to Settings > GitHub Pages, and change the source branch to gh-pages.
Change baseURL in config.toml
Don’t forget to rename your baseURL in config.toml with the value https://<USERNAME>.github.io for your user repository or https://<USERNAME>.github.io/<REPOSITORY_NAME> for a project repository.
```