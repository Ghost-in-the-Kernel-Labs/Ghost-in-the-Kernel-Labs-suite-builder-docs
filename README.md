# Suite Builder

Suite Builder is a command-line tool that crawls a website in a real browser and writes a runnable
test suite for it: Playwright or Selenium in Java (JUnit 5, Maven), or Cypress in TypeScript. It is
proprietary, and its source is private; this repository is its public documentation.

## The crawler

If your server logs show this User-Agent, someone ran Suite Builder against your site:

```
Mozilla/5.0 (compatible; SuiteBuilder/1.0; +https://github.com/Ghost-in-the-Kernel-Labs/Ghost-in-the-Kernel-Labs-suite-builder-docs)
```

It reads one page at a time, about one a second, logged out, and follows links only. It never sends
a form, signs in or buys anything, and it stays on your site. It obeys robots.txt. To block it:

```
User-agent: SuiteBuilder
Disallow: /
```

To slow it down instead, put `Crawl-delay: <seconds>` in that group.

Everything it does, and how to reach the maintainer: **[CRAWLER.md](CRAWLER.md)**.

## Pages

| Page | For |
| --- | --- |
| [CRAWLER.md](CRAWLER.md) | Site owners: the crawler in full, and how to block or slow it |
| [USER-GUIDE.md](USER-GUIDE.md) | Licensed users: the commands, the build options, what a suite contains |
| [GENERATED-OUTPUT.md](GENERATED-OUTPUT.md) | Anyone holding a generated suite: who it belongs to |
| [LICENSE](LICENSE) | The tool's licence: the Suite Builder Personal and Educational License 1.0 |
| [COMMERCIAL-LICENSE.md](COMMERCIAL-LICENSE.md) | Every other use, and how to ask for a licence |

## Contact

Open an issue on this repository:

- [About the crawler on my site](https://github.com/Ghost-in-the-Kernel-Labs/Ghost-in-the-Kernel-Labs-suite-builder-docs/issues/new?template=site-owner.md)
- [License request](https://github.com/Ghost-in-the-Kernel-Labs/Ghost-in-the-Kernel-Labs-suite-builder-docs/issues/new?template=license-request.md)

The maintainer is Ghost ([ghost-in-the-kernel](https://github.com/ghost-in-the-kernel)), who
replies there.
