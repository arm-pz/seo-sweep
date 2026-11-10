# seo-sweep

**An agent skill that fixes a site's SEO with the Skillsmith by Caffeinity SEO skills, and fixes the skills as it goes.**

Point it at a site you own. It checks whether search engines have the site indexed at all, crawls it with [seo-crawl](https://github.com/arm-pz/seo-crawl), audits brand and task searches with [findable](https://github.com/arm-pz/findable), settles which page owns each query with [keyword-guard](https://github.com/arm-pz/keyword-guard), and rewrites with [wordsmith](https://github.com/arm-pz/wordsmith). Then it changes the site's code, proves each fix with a re-crawl, and writes a report. When one of those skills gets something wrong on your site, it logs the defect, reproduces it as a failing test, and fixes the skill.

Works in Claude Code, Codex, Cursor and any agent that loads a SKILL.md. No API keys.

## Install

```bash
npx skills add arm-pz/seo-sweep
npx skills add arm-pz/seo-crawl
npx skills add arm-pz/findable
npx skills add arm-pz/keyword-guard
npx skills add arm-pz/wordsmith
npx skills add arm-pz/get-indexed
```

## Use

```text
Fix the SEO on https://example.com (the site's code is in this repo).
Why doesn't my site show up when I search its name?
Run the SEO skills on my site and improve them as you run them.
```

## What you get

- A baseline: whether the domain is indexed, who ranks for its name and its tasks, and a crawl with every check complete or explained.
- Fixes in the site's code, in order of impact: indexability, content crawlers can read, brand and entity signals, then on-page copy.
- Proof: a re-crawl compared by finding ID, plus the built HTML and a browser check. Then [get-indexed](https://github.com/arm-pz/get-indexed) tells search engines about the changed pages.
- Skill fixes: each defect a skill showed on your site, with a test that failed before the fix and passes after, committed or exported as a patch.
- `seo-sweep-report.md`, ending with the steps only you can take, such as Search Console and Bing Webmaster verification.

## What it does not do

- Promise rankings, or read Search Console or Bing data unless you provide it.
- Give report-only rewrite options; use [seo-polish](https://github.com/arm-pz/seo-polish) for that.
- Resolve two pages competing for one query on its own; use [keyword-resolver](https://github.com/arm-pz/keyword-resolver) for that.
- Crawl sites you don't own.

First run: skillsmith.tech, October 2026. The crawl was clean, but the domain was missing from search results even for its own name. The run fixed five seo-crawl defects and two gaps in findable.

## License

MIT
