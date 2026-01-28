# CLAUDE.md

## Project Overview

Trove is a data warehouse for scraped business data. It pulls reports from systems like iClassPro (which lack good APIs), stores them in SQLite, and enables queries.

## Commands

```bash
# Run tests
pytest

# Pull a report
python -m trove.cli pull classes

# Query
python -m trove.cli query "what classes have openings"
```

## Architecture

- `src/trove/scrapers/` - Browser automation to pull reports
- `src/trove/db/` - SQLite schema and query helpers
- `src/trove/cli.py` - Command line interface
- `skill/` - Clawdbot skill for natural language queries
- `data/trove.db` - SQLite database (gitignored)

## Key Decisions

- **Python** - sqlite3 built-in, good for data work
- **SQLite** - Simple, no server, portable
- **Playwright** - Browser automation for scraping (iClassPro has no API)
- **Historical data** - Each pull creates a report record, classes linked to it

## Credentials

iClassPro credentials are in 1Password. The scraper uses Clawdbot's browser (already authenticated) or needs creds passed in.
