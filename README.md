# Trove

Data warehouse for scraped business data. Pulls reports from various sources (starting with iClassPro), stores in SQLite, enables natural language queries via Clawdbot.

## Status

🚧 **Planning** - See [Issue #1](https://github.com/atriumn/trove/issues/1) for spec

## Overview

Trove scrapes data from business systems that lack good APIs, normalizes it, and stores it for querying. Think of it as a poor man's data warehouse for small business ops.

**Current Sources:**
- iClassPro (class management for Ultimate Ninjas Academy)

**Tech Stack:**
- Python
- SQLite
- Playwright (browser automation)
- Clawdbot skill for queries

## Usage

```bash
# Pull latest class report
trove pull classes

# Query via CLI
trove query "what classes have trials this week"
```

Or via Clawdbot:
> "Hey Todd, what classes have openings this Saturday?"

## License

Private - Atriumn LLC
