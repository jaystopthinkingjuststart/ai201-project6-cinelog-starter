# PR Response Doc — CineLog Watchlist Feature

## AI Usage
<!-- Fill in at the end — how you used AI tools during this project -->

## Comment 1 — Rename
**What I did:** renamed `save_to_watchlist()` to `add_to_watchlist()` in services/watchlist_service.py so it matches the verb_to_noun convention used by `add_to_collection()`. updated the one call site in routes/watchlist/watchlist.py, both the import and the function call.
**How I verified:** ran `grep -rln "save_to_watchlist" .` across the repo before and after the change. before the change it returned services/watchlist_service.py and routes/watchlist/watchlist.py. after the change it returned nothing, confirming every reference was updated. also ran `pytest tests/ -v` and all 4 existing tests passed.

## Comment 2 — Deduplication
**What I did:** added an `AlreadyInWatchlistError` exception to services/watchlist_service.py and a lookup in `add_to_watchlist()` that checks for an existing `WatchlistEntry` with the same `user_id` and `film_id` before creating a new one, following the same shape as `AlreadyInCollectionError` in services/collection_service.py. also updated routes/watchlist/watchlist.py to catch `FilmNotFoundError` and `AlreadyInWatchlistError` and return 404 and 409 respectively, since the route did not handle either exception before and would have returned a raw 500 on a duplicate.
**How I verified:** ran a manual script against an in memory sqlite db that added the same film to a user's watchlist twice. the first call succeeded and returned an entry, the second call raised `AlreadyInWatchlistError` with the expected message instead of creating a second row. also reran `pytest tests/ -v` to confirm the existing 4 tests still pass. a dedicated automated test for this comes in comment 3's file, though the milestone only asked for a nonexistent film test there.

## Comment 3 — Missing test
**What I did:** created tests/test_watchlist.py and wrote `test_add_to_watchlist_nonexistent_film_raises`, modeled directly on `test_add_to_collection_nonexistent_film_raises` in tests/test_collection.py. it reuses the same `app` and `sample_user` fixtures (no `sample_film` fixture is needed since the whole point of the test is that the film does not exist), calls `add_to_watchlist()` with a fake uuid, and asserts that `FilmNotFoundError` is raised.
**How I verified:** ran `pytest tests/test_watchlist.py -v` and confirmed the new test passes on its own. then ran `pytest tests/ -v` and confirmed all 5 tests across both files pass together, so the new file does not interfere with the existing collection tests.

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
