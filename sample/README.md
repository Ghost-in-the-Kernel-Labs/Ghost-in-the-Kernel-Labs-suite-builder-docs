# Sample: three complete suites for The Internet

[The Internet](https://the-internet.herokuapp.com/) is a well-known practice site for test
automation: login forms, frames, alerts, dynamic loading, drag and drop, tables, file upload and
more, on 40-odd pages. These are the three complete projects Suite Builder wrote for it from one
crawl, unedited: clone this repository, open a folder, and run it against the live site.

| | [Playwright (Java)](the-internet-playwright-tests/) | [Selenium (Java)](the-internet-selenium-tests/) | [Cypress (TypeScript)](the-internet-cypress-tests/) |
| --- | --- | --- | --- |
| Files written | 374 | 376 | 334 |
| Tests | 136 | 136 | 130 |
| Run it | `mvn test` | `mvn test` | `npm install`, then `npm test` |

From one crawl of 84 pages, Suite Builder recognised **49 page types** and wrote, in each framework:

- a **page object** for every page type, with its elements, locators and actions (click, type, read,
  verify), and the actions grouped as a test engineer would use them;
- a **smoke test** for every page type (49 of 49): each opens and shows what proves it loaded;
- **navigation tests** for 52 of the site's 54 links between page types: each lands where it promises;
- a **link report** that asks every address the site links to again on each run;
- **pipeline files** for GitHub Actions, GitLab CI and Azure Pipelines, and a Dockerfile;
- the **site audit** (`AUDIT.html`) and `KNOWN-ISSUES.md`: the site's broken links and other problems,
  most serious first;
- **AI assistance** for Claude Code (`ai/`, `.claude/`) and the **Jira loop** (`jira-loop/`): stories in,
  tests or questions out;
- the suite's own **rules check**, which keeps generated and hand-written code apart so a rebuild
  never loses an engineer's work.

Before publishing, each was checked here: both Java projects compile with their real dependencies
and pass their rules check; the Cypress project typechecks and passes its rules check.

Published as a sample by Suite Builder's author: anyone may clone, read and run these suites to evaluate Suite Builder. Each folder's `LICENSE` is the one every generated suite carries, naming the site's owner.

Start with each folder's `README.md`. A suite like these, for your own site, is what the
[partner pilot](../PILOT.md) delivers.
