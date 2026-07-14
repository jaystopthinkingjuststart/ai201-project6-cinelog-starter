# PR Response Doc — CineLog Watchlist Feature

## AI Usage
<!-- Fill in at the end — how you used AI tools during this project -->

## Comment 1 — Rename
**What I did:** renamed `save_to_watchlist()` to `add_to_watchlist()` in services/watchlist_service.py so it matches the verb_to_noun convention used by `add_to_collection()`. updated the one call site in routes/watchlist/watchlist.py, both the import and the function call.
**How I verified:** ran `grep -rln "save_to_watchlist" .` across the repo before and after the change. before the change it returned services/watchlist_service.py and routes/watchlist/watchlist.py. after the change it returned nothing, confirming every reference was updated. also ran `pytest tests/ -v` and all 4 existing tests passed.

## Comment 2 — Deduplication
**What I did:**
**How I verified:**

## Comment 3 — Missing test
**What I did:**
**How I verified:**

## Comment 4 — Default visibility
**My position:**
**Reasoning:**
**Tradeoff acknowledged:**

## Comment 5 — Sort order
**My position:**
**Reasoning:**
**Engagement with reviewer's point:**

## Comment 6 — Rebase
**What conflicted:**
**How I resolved it:**
**How I verified no conflict remains:**

## PR Description
<!-- Written at the end — feature overview, design decisions, manual testing steps -->
