# Gated QA for AI-drafted Nutanica pages

Rules, scanner gates and a test harness that stop process notes, slang and broken encoding from reaching public knowledge pages.

## Problem

- AI agents drafted and saved public knowledge pages on Nutanica under my direction.
- Some live pages carried editor notes, sentences about the page itself, and internal process words.
- Every save had a platform cost, so each bad save cost real money.

## Approach

- Standing rules, one file each, versioned with written decision records.
- Read-only scanner gates for process leaks, slang, acronyms, titles, blocked names, plagiarism and edit summaries.
- Pass and fail test cases for each gate, run by one test script.
- A live-first check: fetch the live page, classify it against a checklist, draft, run the gates, then a human PASS or FAIL on a small pilot set before any save.

## Iterations

- Naming rule v1 (Oct 14, 2026): no acronyms in titles; a title gate with 6 tests.
- Naming rule v2 (Oct 16): live titles cannot be renamed, so titles must be right before a page is created.
- Naming rule v3 (Oct 18): full name plus acronym allowed, umbrella acronyms handled, and a cross-check before any title; 14 new test cases. The backlog of missing pages was re-scored: 71 rows, 49 to create, 8 to link only, 14 to skip.
- Slang gate (Oct 12): a term from the source material was wrongly reworded, so source terms were exempted. The exemption proved too broad the same day, so the gate moved to three outcomes: pass, improve, fail.
- Leak scan (Oct 12): sentences about the page itself survived a fix, so new patterns were added and the scan now runs before every approval.
- Encoding (Oct 12): 10 pages went live with garbled dashes and quotes. The rule now saves one page first and checks its bytes before saving the rest.

## Evaluation

- 57 gate test cases; all pass on re-run (Nov 10, 2026).
- A read-only leak audit of 67 live pages: 16 read in full, the rest checked by scoped search.
- Every real failure becomes a reduced test case in the set.

## Results

- 11 pages with real leaks found and fixed. The most serious suspected leak was confirmed absent.
- The encoding miss cost about ten extra saves' worth of platform fees. The one-page-first check exists to prevent a repeat.
- Later batches were gated before publishing. See [live-pages.md](live-pages.md) for the pages.

## Limitations

- One site and one body of source material. The gates match patterns; they are not graded by a model.
- No measured false-positive rate on real drafts yet. That is the next measurement.

## How it was built

I designed the rules, gates, tests and checks and directed AI to write and run the tooling. I have no formal coding training.
