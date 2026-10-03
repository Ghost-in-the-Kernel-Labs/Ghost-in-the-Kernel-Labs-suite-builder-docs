# The SuiteBuilder crawler

This page is for site owners who found Suite Builder's crawler in their logs.

Suite Builder is a tool for test engineers. It reads a site's pages in a real browser and writes an
automated test suite for that site. Each crawl is started by a person who has the tool, against one
site they name.

## How to recognise it

It identifies itself as `SuiteBuilder`. By default, every request carries this User-Agent:

```
Mozilla/5.0 (compatible; SuiteBuilder/1.0; +https://github.com/Ghost-in-the-Kernel-Labs/Ghost-in-the-Kernel-Labs-suite-builder-docs)
```

A person running it can change the User-Agent with `--user-agent`. The default is always the one
above.

## Blocking it

It obeys robots.txt, as [RFC 9309](https://www.rfc-editor.org/rfc/rfc9309) describes, for the
product token `SuiteBuilder`, matched case-insensitively. If your robots.txt has no group for it,
the `*` group applies. It reads robots.txt again on every redirect hop.

To block it entirely:

```
User-agent: SuiteBuilder
Disallow: /
```

To slow it down, give its group a `Crawl-delay` in seconds:

```
User-agent: SuiteBuilder
Crawl-delay: 10
```

It honours a `Crawl-delay` when that is longer than its own delay.

## How hard it reads a site

- One page at a time, never in parallel.
- 1 second between page loads by default.
- At most 300 pages by default, and it usually stops much sooner: once 30 pages in a row show
  nothing new.
- After the crawl it may load up to 60 of those pages once more, in a fresh browser, to see what
  changes between visits.
- Last, it asks for one made-up address, to learn whether the site answers "not found" properly.

## What it never does

- It stays on the one site it was pointed at. Links to other sites are noted, never followed.
- It follows links only, logged out.
- It never sends a form, signs in, or buys anything.
- It does not download images, media or fonts.

## When it stops

- At once on `429 Too Many Requests`.
- After repeated failures in a row.

## Who runs it

People who have the tool, against sites they own or have permission to test. The tool tells them:
"Only crawl sites you own or have permission to test." Suite Builder's author does not run crawls of
sites on anyone's behalf without that.

## Contact

[Open an issue](https://github.com/Ghost-in-the-Kernel-Labs/Ghost-in-the-Kernel-Labs-suite-builder-docs/issues/new?template=site-owner.md)
with the site-owner template: your site, when you saw the crawler, and what you would like (stop,
slow down, or a question). The fastest way to stop it is the robots.txt lines above.
