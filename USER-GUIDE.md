# Suite Builder: the user guide

Suite Builder crawls a website and writes a test suite for it. This guide is for the people who run
it and the people who work in the suites it writes. Site owners who saw the crawler in their logs:
[CRAWLER.md](CRAWLER.md).

**Only crawl sites you own or have permission to test.**

## What it does

Three steps, which `suite build` runs in one line:

| Step | What it does | Command |
| --- | --- | --- |
| 1. Crawl | Follows same-site links in a real browser, politely, reading every kind of page and the links between them | `suite crawl <site>` |
| 2. Group | Sorts the pages into page types: `/pokedex/bulbasaur` and `/pokedex/ivysaur` are one family, `/about` is a one-off page | `suite group <crawl.json>` |
| 3. Generate | Decides what the suite means (its pages, checks, links and tests), checks that decision, and writes it in the framework asked for | `suite generate <templates.json>` |

It is built like a compiler: the crawl is read into a precise model of the suite, the model is
checked before anything is written, and each framework's output is read back and held to the model,
fact for fact. The same crawl gives the same suite, byte for byte, in any framework.

## Getting started

You need [Node.js](https://nodejs.org/) 20 or newer to run Suite Builder, and to run the suites it
writes: Java 17 or newer with Maven (Playwright and Selenium suites), or Node.js (Cypress suites).
Nothing else is installed by hand. From the `suite-builder` folder:

```
suite build www.example.com
```

(`suite.cmd` on Windows, `./suite` on macOS and Linux.) The first run sets the tool up, which takes a
minute or two: it installs what it needs and the browser the crawler uses. It does the same after an
update.

| To | One line |
| --- | --- |
| see every command | `suite` |
| see everything a build can be told | `suite build` |
| make a suite for a site | `suite build www.example.com` |
| a quick crawl, for a demo (50 pages at most) | `suite build www.example.com --quick` |
| everything, however long it takes | `suite build www.example.com --long` |
| a Selenium or Cypress suite | `suite build www.example.com --selenium` (or `--cypress`; several at once from one crawl) |
| rebuild after the site changed | `suite build www.example.com` again: your changes in YOURS blocks stay |
| rebuild from the suite's own crawl, without crawling | `suite build example-com-tests` |

A bare domain means `https://`, or `http://` when the site can't be reached over https; the tool
says when it falls back. It never stops to ask a question.

### How much of the site

By default the crawl stops once 30 pages in a row show nothing new, or at 300 pages.

```
--quick              At most 50 pages, no second look (a demo)
--long               No early stop and no limit (hours on a big site; --max-pages still limits it)
--max-pages <n>      Most pages to read
--include <path>     Only this part of the site, e.g. --include /careers (repeatable)
--exclude <path>     Never this part, e.g. --exclude /forum (repeatable)
--all-languages      Every language of the site (default: only the start page's)
--delay <ms>         Wait between pages (default 1000; robots.txt's Crawl-delay wins if longer)
--settle <ms>        Longest wait for a page's scripts to finish drawing it (default 3000)
--user-agent <text>  The browser name the site sees (robots.txt is still read as SuiteBuilder's)
```

The build ends by saying why the crawl stopped: `complete` (every reachable page was read),
`saturated` (30 pages in a row showed nothing new), `page-limit`, `too-many-errors` (3 failures in a
row: try later, or a longer `--delay`) or `rate-limited` (the site answered 429: try later with a
longer `--delay`).

## The three frameworks

| | Playwright | Selenium | Cypress |
| --- | --- | --- | --- |
| Language, runner | Java, Maven, JUnit 5 | Java, Maven, JUnit 5 | TypeScript, npm, Cypress |
| Browsers | Chromium, Firefox, WebKit (downloaded by Playwright) | Chrome, Firefox, Edge, Safari (installed; drivers by Selenium Manager) | Chrome when installed, else Electron; Firefox, Edge |
| Links that open a new tab | followed | followed | opened in the same tab |
| Evidence of a failure | screenshot, page, trace, console, network, steps | screenshot, page, console (Chrome, Edge), steps | screenshot, page, console, steps |
| Ads | blocked unless turned off | blocked in Chrome and Edge unless turned off | blocked unless turned off |

Playwright is the default. Whatever the framework, the suite has the same shape and the same names.

## Running a suite

```
cd example-com-tests
mvn test
```

For Cypress: `cd example-com-cypress-tests`, `npm install`, `npm test`.

| To | Add |
| --- | --- |
| watch it in a browser (Java suites) | `-Dheaded=true` (Playwright: half a second per action; `-DslowMo=1000`) |
| another browser | `-Dbrowser=firefox` (Playwright: also `webkit`) |
| run against another copy of the site | `-DbaseUrl=https://staging.example.com` |
| let ads through | `-DblockAds=false` (Cypress: `--expose blockAds=false`) |

A failing test says which step failed and why, in plain words, and leaves its evidence in
`target/failures/` (Cypress: its own failures folder):

```
-> SearchTest: Searching from a Pokémon's page lists what was searched for
   1. Open the pokedex detail page (/pokedex/pikachu)
      now on the pokedex detail page
   2. Type "bulbasaur" into the search input
   3. Click the Search button
   FAILED at step 3: Click the Search button
   because: PokedexAllPage did not load! URL was .../search, expected /pokedex/*
```

## What is in a suite

Everything is named after the site: the Java package comes from the domain, the classes from the
page types, the constants from the menu and the headings.

| Part | What it holds |
| --- | --- |
| `pages/<type>/` | One package per page type: the page class (`open()`, and `isLoaded()`, which checks the address, the full page load, the title and the page's key headings), its Elements (locators), Tasks, and Click, Check, Enter, Clear, Read and Verify actions |
| `pages/header/`, `pages/footer/` | The site's menu: every page's `navigateTo()`, one method per destination, opening dropdowns on the way |
| `SmokeTest` | Every page type opens and passes its checks |
| `NavigationTest` | Header, footer and page-to-page links land where they should |
| `MenuTest` | Links inside dropdowns |
| `BrokenLinksTest` | Links the crawl found answering 404 or 500: they fail until the site is fixed |
| `HarnessTest` | The suite tests its own checks and actions with every run, on a page of its own |
| `SuiteRulesTest` | The rules every test follows (`SUITE-RULES.md`) |
| `stories/` | Where tests written from user stories go |
| `AI-README.md`, `ai/` | For an AI handed the folder: the map, the library's methods, short recipes |
| `controls/` | Every button, field and dropdown the crawl saw, with the words a story would use and a locator ready to paste |
| `crawl/` | The crawl the suite came from, the pages as the crawl saw them, and how it was built |
| `KNOWN-ISSUES.md` | What the crawl found wrong with the site |

Tests read like the hand-written kind:

```java
new PokedexNationalPage(page).open().click().goToPokedexDetail("houndour");
new PokedexDetailPage(page).open("pecharunt").verify().sectionHeadingsVisible();
```

A family of pages (one template, many pages) is one page class with a parameter: `open(name)`.

## Your changes survive a rebuild

Generated files have marked places for your own code, YOURS blocks:

```java
    // ==== YOURS (elements): safe to edit; regenerating keeps what is between these lines ====
    SEARCH_INPUT(page -> page.locator("css=input[name='q']")),
    // ==== END YOURS (elements) ====
```

A rebuild rewrites everything outside the blocks and keeps what is in them. Files it did not write
(your story tests) are never touched. Work that no longer has a place, like the blocks of a page type
the new crawl doesn't have, is moved to `orphaned/`, never deleted. Each file's first lines say what
may be edited in it.

The suite's rules are sealed: a rebuild puts back any generated file changed outside its YOURS
blocks and says what it put back. `suite verify example-com-tests` compares every generated file with
what Suite Builder generates from the suite's own crawl, and is the check to run in CI.

## Stories: tests from user stories, with an AI

Put one plain-text story per file in the suite's `stories/new/` (its id, like `PROJ-7`, in the file
name or the text), hand the whole folder to an AI and say "do the stories".
`stories/AI-INSTRUCTIONS.md` tells it the rest: check every word of the story against what the crawl
saw, then either write the test, the suite's way, or push back with exactly what is missing (a page
the crawl never saw, a word that matches nothing, no outcome to check, something unsafe on the live
site).

## More commands

| To | One line |
| --- | --- |
| see the dock and the suites in it | `suite dock` |
| take a suite out of the dock, a project of its own | `suite undock example-com-tests <folder>` |
| write a suite somewhere else | `suite build www.example.com --out <folder>` |
| check every generated locator on the saved pages | `suite verify example-com-tests --locators` |
| why the pages were grouped, and what each page type checks | `suite explain example-com-tests` |
| why a generated line exists | `suite trace example-com-tests <file[:line]>` |
| what changed about a site between two crawls | `suite diff <before> <after>` |
| how many elements a locator finds on a saved page | `suite locate example-com-tests <page> "<locator>"` |
| help on a topic | `suite help <topic>` |

**The dock.** Suites are written into a folder `dock(suitebuilder)` beside the `suite-builder` folder,
so a new release unzipped over Suite Builder can't touch them, and a suite's name alone finds it from
any folder. A suite written anywhere else is its own project: a build of its site never touches it.

**The theme.** Suite Builder and its Playwright suites run in a cyberpunk theme, with art and music,
unless it is turned off: `suite theme off` (for good, on this computer), `mvn test -Dtheme=off` (one
run). It is never on when output is piped, or on a build server. It changes how a run looks, never
what it checks.

## Questions

[Open an issue](https://github.com/Ghost-in-the-Kernel-Labs/Ghost-in-the-Kernel-Labs-suite-builder-docs/issues/new). For
business or government use, see [COMMERCIAL-LICENSE.md](COMMERCIAL-LICENSE.md).
