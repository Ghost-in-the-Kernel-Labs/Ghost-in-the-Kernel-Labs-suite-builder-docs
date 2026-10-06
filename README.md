# Suite Builder

**Automated testing for your website, written for you.** Suite Builder reads a website the way a
visitor does and writes a complete, runnable automated test suite for it, in the framework your
engineers already use: Playwright (Java), Selenium (Java) or Cypress (TypeScript). The suite comes
with an audit of the site's health and the tooling to keep it current as the site changes.

## What it does for your team

| You get | So your team |
| --- | --- |
| A ready test suite: page objects, locators, actions, smoke, navigation and menu tests | Starts from working automation, not a blank project |
| A site audit: broken links, failing scripts, slow pages, security headers, accessibility and search issues | Sees the site's problems, most serious first, with the likely fix |
| Pipeline files for GitHub Actions, GitLab CI and Azure Pipelines, and a Dockerfile | Runs the suite on every change from the first week |
| AI assistance (Claude Code): user stories turned into tests, failures explained | Extends the suite in plain language; ambiguous stories come back as questions, not guesses |
| A Jira connection: stories marked ready are pulled in, and each card is updated with its tests or questions | Keeps analysts in Jira and QA work visible on the board |
| Rebuilds that keep your changes | Updates the suite when the site changes without losing your engineers' work |

Every suite is checked by machine before it is delivered: each test rests on what the crawl actually
observed, the three frameworks are held to the same meaning, and every generated line traces back
to the pages and the decision behind it.

## Partner pilot

We are inviting a small number of companies to a free pilot: with your permission we build a suite
for your site, your engineers evaluate it for 60 days, and you decide whether to continue.
**[PILOT.md](PILOT.md)** has the details and terms; **[sample/](sample/)** shows what a suite and its
audit look like.

## Quick start (licensed users)

```
suite build www.example.com
```

The [user guide](USER-GUIDE.md) covers building a suite, what it contains, running it and keeping
your changes.

This repository is Suite Builder's public documentation. The tool's source is not public.

## Are you a site owner?

If you found `SuiteBuilder` in your server logs, read **[CRAWLER.md](CRAWLER.md)**: what the crawler
does, the limits it keeps, and how to block it with robots.txt.

## Documents

| Document | For |
| --- | --- |
| [CRAWLER.md](CRAWLER.md) | Site owners: what the crawler is, how it behaves, how to block it or report a problem |
| [PILOT.md](PILOT.md) | Companies: the free partner pilot and its terms |
| [sample/](sample/) | Anyone: a sample suite and site audit, from a demonstration site |
| [USER-GUIDE.md](USER-GUIDE.md) | People using Suite Builder: building a suite, what it contains, running it, keeping your changes |
| [GENERATED-OUTPUT.md](GENERATED-OUTPUT.md) | Who holds a generated test suite: the owner of the site it tests |
| [LICENSE](LICENSE) | The Suite Builder Personal and Educational License 1.0, the license of the tool |
| [COMMERCIAL-LICENSE.md](COMMERCIAL-LICENSE.md) | Every other use, and how to ask for a license |

## License, in short

Suite Builder is proprietary. Copyright (c) 2026 ghost-in-the-kernel. All rights reserved.

- **The tool:** the [Suite Builder Personal and Educational License 1.0](LICENSE). Free for
  educational use (study, coursework, teaching) and for validating your own personal projects with
  no commercial use. Every other use, including any business, nonprofit or government use, needs a
  [commercial license from the author](COMMERCIAL-LICENSE.md).
- **What it generates:** each suite carries its own `LICENSE`. A suite generated under a valid
  license belongs to the owner of the site it tests, to use, change and share for any purpose,
  commercial use included ([GENERATED-OUTPUT.md](GENERATED-OUTPUT.md)).

## Contact

For a pilot, a licence or a partnership: **[j_be_nimble@hotmail.com](mailto:j_be_nimble@hotmail.com)**.

Or open an issue on this repository:

- [The crawler visited my site](https://github.com/Ghost-in-the-Kernel-Labs/Ghost-in-the-Kernel-Labs-suite-builder-docs/issues/new?template=crawler.md)
- [License request](https://github.com/Ghost-in-the-Kernel-Labs/Ghost-in-the-Kernel-Labs-suite-builder-docs/issues/new?template=license-request.md)
- [Anything else](https://github.com/Ghost-in-the-Kernel-Labs/Ghost-in-the-Kernel-Labs-suite-builder-docs/issues/new)

The maintainer is Ghost ([ghost-in-the-kernel](https://github.com/ghost-in-the-kernel)) and replies
there.
