---
name: About the crawler on my site
about: SuiteBuilder showed up in your logs and you want it to stop, slow down, or have a question
title: "Crawler on my site"
labels: site-owner
---

The fastest way to stop the crawler is robots.txt. Add this to yours:

```
User-agent: SuiteBuilder
Disallow: /
```

To slow it down instead, add `Crawl-delay: <seconds>` to that group. CRAWLER.md has the details.

**Your site:** <!-- the domain -->

**When you saw it:** <!-- dates and times, with time zone -->

**What you'd like:** <!-- stop, slow down, or a question -->
