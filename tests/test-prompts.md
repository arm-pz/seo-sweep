# Test prompts

Each entry gives a prompt, the setup, what a good response does, and what counts as failure.

## 1. Brand search shows other domains
**Prompt:** "Fix the SEO. When I search 'acme tech' I get acme.com and acme.app, not my site." **Setup:** acme.tech is live with a sitemap; search tools return nothing from it.
**Good:** checks indexation before anything else and says it could not be verified without Search Console or Bing Webmaster; crawls; finds the technical layer clean if it is and says so; puts verification and sitemap submission at the top of the user's list; drafts brand signals (title qualifier, `alternateName`, disambiguation line) and asks before stating the other sites are unrelated.
**Fail:** rewrites titles for ranking while the domain is unindexed; invents crawl problems on a clean site; states "not affiliated" without asking.

## 2. Content only exists after JavaScript
**Prompt:** "Run the SEO skills on my landing page." **Setup:** a single-page app whose copy is rendered by JavaScript into an empty `<div id="root">`.
**Good:** reads the built HTML, says a non-rendering crawler sees an empty page, adds a plain-HTML equivalent of the copy, rebuilds and checks the built HTML and the page in a browser.
**Fail:** reports "no H1" or "thin content" as the root cause without noticing the rendering; adds hidden keyword text.

## 3. A skill reports a false positive
**Setup:** seo-crawl reports `/cdn-cgi/l/email-protection` as a broken internal link on a Cloudflare site.
**Good:** confirms the link works for people, logs a seo-crawl defect, finishes the sweep, then writes a test that fails on the unchanged crawler, fixes it, shows the suite passing and the re-crawl clean.
**Fail:** "fixes" the site by removing the email links; edits the crawler without a failing test; stops the sweep to fix the skill first.

## 4. No push access to the skill repo
**Setup:** the defect is in a skill repo the session can read but not push to.
**Good:** fixes it in a scratch clone with a test, exports a patch with `git format-patch`, and tells the user the path and `git am` command.
**Fail:** leaves the fix described only in prose; pushes somewhere else.

## 5. Report-only request (near miss)
**Prompt:** "Audit my site's SEO and give me rewrite options, don't change anything."
**Good:** hands off to `seo-polish`.
**Fail:** edits the site's code.

## 6. Cannibalization only (near miss)
**Prompt:** "Two of my pages compete for 'cold wallet', which should win?"
**Good:** hands off to `keyword-resolver` (or `keyword-guard` for the map alone).
**Fail:** runs a full sweep.
