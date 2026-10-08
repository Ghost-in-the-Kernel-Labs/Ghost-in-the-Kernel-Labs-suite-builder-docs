# Partner pilot

A free pilot for companies: with your permission, we build a Suite Builder test suite for your
website, your engineers evaluate it for 60 days, and you decide whether to continue.

## What you receive

- **A test suite for your site** in Playwright (Java), Selenium (Java) or Cypress (TypeScript):
  page objects, locators, actions, and smoke, navigation and menu tests, ready to run.
- **A site audit**: broken links, failing scripts, slow pages, missing security headers,
  accessibility and search issues, most serious first, each with why it matters and the likely fix.
- **Pipeline files** for GitHub Actions, GitLab CI and Azure Pipelines, and a Dockerfile.
- **AI assistance and a Jira connection**: user stories turned into tests by Claude Code, with
  ambiguous stories returned as questions; Jira cards pulled in and updated automatically.
- **A walkthrough** for your engineers: running the suite, how it is organised, how to extend it.

[sample/](sample/) shows a suite and its audit, generated from a small demonstration site.

## How it works

1. **Introductory call.** We agree the site or area to cover (a public site, a staging copy or one
   product area) and your team's framework.
2. **Written permission.** You confirm that we may crawl that site. Suite Builder reads a site only
   with its owner's permission.
3. **The build.** The crawler reads the site as a visitor would and keeps to strict limits: it
   obeys robots.txt, waits between pages and backs off at the first sign of strain ([CRAWLER.md](CRAWLER.md)).
4. **Handover.** The suite and its audit, with the walkthrough.
5. **Evaluation: 60 days.** Your team runs, changes and extends it on your own systems.
6. **Decision.** Continue under a commercial licence, or not. The suite is yours to keep either way,
   and we ask for your feedback.

## Terms

| Term | Detail |
| --- | --- |
| Cost | None for the pilot |
| Evaluation | 60 days from handover to decide whether to continue |
| The suite | Yours to keep, as the site's owner: use, change and share it for any purpose, during the pilot and after, with no licence needed ([GENERATED-OUTPUT.md](GENERATED-OUTPUT.md)) |
| After 60 days | New suites, and rebuilds as your site changes, need a commercial licence ([COMMERCIAL-LICENSE.md](COMMERCIAL-LICENSE.md)) |
| Permission | Only the sites you name, and only after your written permission |
| Your data | The crawl reads what a visitor sees. Pages saved during the crawl are kept only while needed and never published; nothing from your site is added to our repositories |
| Accounts | Signed-in areas need test accounts on a test environment, supplied by you; account details are never written into the suite or committed |
| Confidentiality | The audit's findings are shared only with you |
| Our purpose | Pilots test and improve Suite Builder on real sites; nothing identifying your site is published without your consent |

## What we ask in return

Candid feedback: a call with your engineers after two to three weeks, the run results of any test
that fails for a reason that is the tool's fault, and a decision call before the 60 days end.

## Contact

**[j_be_nimble@hotmail.com](mailto:j_be_nimble@hotmail.com)**, or an
[issue on this repository](https://github.com/Ghost-in-the-Kernel-Labs/Ghost-in-the-Kernel-Labs-suite-builder-docs/issues/new).
