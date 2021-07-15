+++
date = "2021-07-15T01:44:17Z"
title = "How Hugo Setup action works"
description = "Quick look on Hugo site deployment with GitHub Actions"
tags = ["servers", "hugo", "github", "deployment"]
+++

It's really easy to [host your Hugo site on GitHub](https://gohugo.io/hosting-and-deployment/hosting-on-github/), and [GitHub Actions for Hugo](https://github.com/marketplace/actions/hugo-setup) makes deploy a breeze. 
And this is how it's works.

# Flow diagram
```
|files| /archetypes, /content, /static, /themes, config.toml| -+ [branch] main] -> (trigger) Build)
                                                                                    |
                                                                                    *
|files| /assets, /categories, /img, /page, /tags, index.html, 404.html, index.xml, sitemap.xml |
                                                                                        |
                                                                                        +
                                                                                [branch] gh-pages]
                                                                                            |
                                                                                            *
                                                                                    /site.github.io/
```

# Notes
Don't forget to change your GitHub Pages settings to
* Branch: ```gh-pages```
* Directory: ```/ (root)```