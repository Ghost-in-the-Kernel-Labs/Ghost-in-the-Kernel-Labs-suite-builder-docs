# The SuiteBuilder crawler

If you run a website and found this in your logs:

```
Mozilla/5.0 (compatible; SuiteBuilder/1.0; +https://github.com/Ghost-in-the-Kernel-Labs/Ghost-in-the-Kernel-Labs-suite-builder-docs)
```

someone ran Suite Builder against your site. Suite Builder is a tool for test engineers: it reads a
site's pages in a real browser and writes an automated test suite for that site (the checks a QA
team would otherwise write by hand). It is not a search engine, a scraper for content or prices, or
a security scanner, and it is not run as a service: each crawl is started by a person, on their own
computer, for a site they name.

Its users are told to crawl only sites they own or have permission to test.

## How it behaves

- **One site only.** Links to other sites are recorded, never followed. A redirect to another site
  is recorded, never requested.
- **robots.txt is obeyed**, as [RFC 9309](https://www.rfc-editor.org/rfc/rfc9309) describes: rules for
  `SuiteBuilder`, or for `*` when none name it; the longest matching rule wins; `*` and `$`
  wildcards are understood. Every redirect is checked against robots.txt too. If your robots.txt
  answers with a server error (5xx), nothing is crawled.
- **A delay between pages**: 1 second by default. A longer `Crawl-delay` in your robots.txt wins.
- **A page limit**: 300 pages by default (50 for a quick crawl). Most crawls stop sooner, once 30
  pages in a row show nothing new.
- **It backs off.** It stops after 3 failures in a row (network errors or 5xx answers), and at once
  on `429 Too Many Requests`. Only the first page is asked for a second time, once, when it doesn't
  finish loading within 30 seconds (a server waking from sleep can take that long).
- **Only what a test needs.** No images, video or fonts are downloaded. Known advertising hosts
  are not requested.
- **It reads, and does nothing else.** It reads public pages, logged out: GET requests only, no
  form is sent, and sign-in links are skipped. It never records cookies or request headers.

A user can change the User-Agent string the crawler sends (some sites need a particular browser
name). Even then, robots.txt is still read as `SuiteBuilder`, so your rules for it still hold.

## Blocking it

To keep Suite Builder off your whole site, add this to your robots.txt:

```
User-agent: SuiteBuilder
Disallow: /
```

To keep it off part of the site:

```
User-agent: SuiteBuilder
Disallow: /account/
Disallow: /search
```

To slow it down (seconds between pages):

```
User-agent: SuiteBuilder
Crawl-delay: 10
```

## Reporting a problem

If the crawler misbehaved on your site (it ignored your robots.txt, or came too fast), or you want
to reach the maintainer for any other reason,
[open an issue](https://github.com/Ghost-in-the-Kernel-Labs/Ghost-in-the-Kernel-Labs-suite-builder-docs/issues/new?template=crawler.md).
The date and time of the visit, and the lines from your logs, help.

Suite Builder runs on its users' computers, so the maintainer cannot see or stop another person's
crawl. robots.txt is the way to keep the crawler out; a report is how a fault in the crawler itself
gets fixed.
