# Suite Builder: user guide

A short guide for licensed users. The tool's own `suite help all` has the full list of options.

**Only crawl sites you own or have permission to test.**

## Getting Suite Builder

Suite Builder is distributed to licensed users, who receive it from the author. To ask for a
licence, see [COMMERCIAL-LICENSE.md](COMMERCIAL-LICENSE.md).

## Commands

```
suite build <site>                 Crawl a site and write its suite: suite build www.example.com
suite build <suite folder>         Rewrite a suite from the crawl it carries, keeping your changes
suite dock                         Your suites, and where they are
suite undock <suite> [<folder>]    Move a suite out of the dock: a project of its own, no longer rebuilt
suite help <suite folder>          How to run a suite: groups, one test, the browser, a slow site
suite test <suite folder>          Put back anything changed by mistake, then run its tests
suite verify <suite folder>        Is every generated file as generated? (for CI)
suite explain <suite folder>       Why each page type has the checks it has, and not others
suite locate <suite> <page> "<locator>"
suite update                       Which build this is, and how to bring it up to date
```

## Build options

| Option | What it does |
| --- | --- |
| `--quick` | At most 50 pages |
| `--long` | No page limit |
| `--max-pages <n>` | Most pages to read (default 300) |
| `--include <path>` | Only this part of the site |
| `--exclude <path>` | Never this part of the site |
| `--all-languages` | Every language of the site |
| `--delay <ms>` | Wait between page loads (default 1000) |
| `--settle <ms>` | Wait for a page to settle (default 3000) |
| `--user-agent <text>` | The User-Agent the site sees |
| `--selenium` | Write a Selenium suite (Java) |
| `--cypress` | Write a Cypress suite (TypeScript) |
| `--out <folder>` | Where to write the suite |
| `--package <name>` | The suite's package name |

For example:

```
suite build www.example.com --quick --cypress
```

## What a generated suite has

- Page objects for each kind of page on the site.
- Smoke, navigation, menu and site-wide tests.
- A link report.
- The suite's own rule checks.
- An `ai/` folder that tells an AI assistant how to turn user stories into tests.
- YOURS blocks: code between `// ==== YOURS (...) ====` markers survives every rebuild.

Each suite carries its own `LICENSE`. Who it belongs to is explained in
[GENERATED-OUTPUT.md](GENERATED-OUTPUT.md).

## Other people's sites

Crawl only sites you own or have permission to test. Site owners can read what the crawler does,
and how to block it, in [CRAWLER.md](CRAWLER.md).
