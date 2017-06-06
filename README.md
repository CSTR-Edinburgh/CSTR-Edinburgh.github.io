# CSTR-Edinburgh blog

This is the repository for the [CSTR-Edinburgh](https://cstr-edinburgh.github.io) blog. It is based on [Jekyll Now](https://github.com/barryclark/jekyll-now).

The intention of the blog is to showcase our projects, e.g. an abstract plus a figure or table from a published paper with links to the paper, source code and results. The posts should be brief and instead of going into too much detail it should refer to the respective papers.

## Creating a new post
1. Go to the `_posts` [directory](https://github.com/CSTR-Edinburgh/CSTR-Edinburgh.github.io/tree/master/_posts)
2. Click *Create new file*
3. Include the header below, and modify its title and the body:
4. Save in the format `year-month-day-title.md`

Boilerplate header:
```
---
layout: post
title: Modify this title.
author: Your Name
---

Your content goes here.
```

## Images
- Place images in `CSTR-Edinburgh.github.io/images/`. I.e. you can go [here](https://github.com/CSTR-Edinburgh/CSTR-Edinburgh.github.io/tree/master/images) and click *Upload files*
- Preface image filenames by the filename of your blog post, e.g.:
`year-month-day-title-imagename.png`
- Include them in your text by:  `![an image alt text]({{ site.baseurl }}/images/year-month-day-title-imagename.png "an image title")`
