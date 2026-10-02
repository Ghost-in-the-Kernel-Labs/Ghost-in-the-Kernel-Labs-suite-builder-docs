# Suite Builder

**A compiler for test suites.** Give it a website's address: it crawls the site in a real browser,
works out what kinds of pages it has and how they link, and writes a complete, runnable test suite
for it in Playwright (Java), Selenium (Java) or Cypress (TypeScript): page objects, locators, click
and verify actions, the site's menu, and smoke, navigation, menu and broken-link tests.

```
suite build www.example.com
```

This repository is Suite Builder's public documentation. The tool's source is not public.

## Are you a site owner?

If you found `SuiteBuilder` in your server logs, read **[CRAWLER.md](CRAWLER.md)**: what the crawler
does, the limits it keeps, and how to block it with robots.txt.

## Documents

| Document | For |
| --- | --- |
| [CRAWLER.md](CRAWLER.md) | Site owners: what the crawler is, how it behaves, how to block it or report a problem |
| [USER-GUIDE.md](USER-GUIDE.md) | People using Suite Builder: building a suite, what it contains, running it, keeping your changes |
| [GENERATED-OUTPUT.md](GENERATED-OUTPUT.md) | Who may use a generated test suite, and how |
| [LICENSE](LICENSE) | The Suite Builder Noncommercial License 1.0, the license of the tool |
| [COMMERCIAL-LICENSE.md](COMMERCIAL-LICENSE.md) | Business and government use, and how to ask for a license |

## License, in short

Suite Builder is source-available, not open source. Copyright (c) 2026 ghost-in-the-kernel.

- **The tool:** the [Suite Builder Noncommercial License 1.0](LICENSE). Personal, noncommercial use
  is free. Business use (at work, for clients, in a product) and any government use need a
  [license from the author](COMMERCIAL-LICENSE.md).
- **What it generates:** a test project built under a valid license belongs to whoever it was built
  for, to use freely, commercial use included ([GENERATED-OUTPUT.md](GENERATED-OUTPUT.md)).

## Contact

Open an issue on this repository:

- [The crawler visited my site](https://github.com/Ghost-in-the-Kernel-Labs/Ghost-in-the-Kernel-Labs-suite-builder-docs/issues/new?template=crawler.md)
- [License request](https://github.com/Ghost-in-the-Kernel-Labs/Ghost-in-the-Kernel-Labs-suite-builder-docs/issues/new?template=license-request.md)
- [Anything else](https://github.com/Ghost-in-the-Kernel-Labs/Ghost-in-the-Kernel-Labs-suite-builder-docs/issues/new)

The maintainer is Ghost ([ghost-in-the-kernel](https://github.com/ghost-in-the-kernel)) and replies
there.
