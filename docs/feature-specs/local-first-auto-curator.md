# Feature: Local-First Auto-Curator

> A weekly Claude Code Agent SDK-powered pipeline that researches, evaluates, and PRs high-quality local-first resources to the awesome-local-first repo.

## Overview

An automated curation system that runs as a GitHub Actions cron job once per week. It uses the Claude Code Agent SDK to spawn parallel subagents — each researching a different source (newsletter, HN/Reddit, GitHub trending, dev blogs). Results are merged, deduplicated, quality-filtered with a high bar, and categorized via LLM into the correct README section. A single PR is opened only when genuinely valuable content is found.

## Goals

- **Keep the list fresh** — ensure the awesome-list stays current with new tools, articles, and case studies
- **Save manual curation time** — reduce hours spent manually finding and vetting resources
- **Increase community value** — make the repo a go-to hub that people star/watch for local-first updates

## Architecture

### Subagent Fan-Out (Parallel)

Four subagents run simultaneously, each specialized for a source:

1. **Newsletter Agent** — Fetches and parses localfirstnews.com for new entries, releases, meetup recaps
2. **HN/Reddit Agent** — Searches Hacker News (Algolia API) and Reddit (r/localfirst, r/programming) for recent local-first discussions with significant engagement
3. **GitHub Agent** — Scans GitHub trending repos with relevant topics (crdt, sync-engine, offline-first, local-first, collaborative-editing)
4. **Blog/Conference Agent** — Checks RSS feeds and known blogs (Ink & Switch, Martin Kleppmann, Linear blog, Jamsocket, etc.) for new articles and conference talk announcements

### Lead Agent (Merge & Evaluate)

The lead agent:
1. Collects results from all subagents
2. Deduplicates against existing README URLs (URL matching)
3. Applies quality gate (must pass 3+ of 4 signals)
4. Classifies each entry into the correct README section via LLM
5. Generates the README diff and opens a PR (or skips if nothing qualifies)

```
┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐
│  Newsletter  │  │  HN/Reddit  │  │   GitHub    │  │ Blogs/Conf  │
│    Agent     │  │    Agent    │  │   Agent     │  │    Agent    │
└──────┬──────┘  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘
       │                │                │                │
       └────────────────┴────────┬───────┴────────────────┘
                                 │
                         ┌───────▼───────┐
                         │  Lead Agent   │
                         │  (Merge,      │
                         │   Dedup,      │
                         │   Quality,    │
                         │   Categorize) │
                         └───────┬───────┘
                                 │
                         ┌───────▼───────┐
                         │   Open PR     │
                         │  (or skip)    │
                         └───────────────┘
```

## Quality Gate

A resource must pass **3 or more** of the following signals:

| Signal | Criteria |
|--------|----------|
| **GitHub Stars / Traction** | 50+ stars, or significant recent growth (e.g., 20+ stars in past week) |
| **Author Credibility** | Published by a known figure or org in the local-first space |
| **LLM Relevance Score** | Claude rates the resource >= 8/10 for local-first relevance and usefulness |
| **Content Depth** | Substantial content — not a tweet, shallow listicle, or marketing page |

## Deduplication

- Parse all URLs currently in `README.md`
- Compare candidate URLs against this set
- Skip any candidate whose URL (normalized) already exists

## Categorization

The LLM reads the existing README sections and classifies each new entry into:
- Core Resources → Foundational Articles / Architecture & Implementation / Performance & UX / Video Content
- Development Tools & Libraries → Database Solutions / State Management & Sync / CRDT Libraries
- Real-World Examples → Case Studies / Example Applications / Learning Resources
- Community
- Conferences & Talks

## PR Format

**When content is found**, a single PR is created with:

- **Title**: `chore: weekly local-first curation — {date}`
- **Branch**: `auto-curate/{date}`
- **Body**:
  - Summary of what was found and from which sources
  - Per-entry rationale:
    - Source where it was found
    - Quality signals passed (stars, author, LLM score)
    - Why it's relevant to the local-first community
  - Stats: N candidates evaluated, M passed quality gate
- **Diff**: README.md changes with entries placed in correct sections

**When nothing qualifies**: No PR is created (skip silently).

## Runtime: GitHub Actions

```yaml
name: Weekly Local-First Curation
on:
  schedule:
    - cron: '0 9 * * 1'  # Every Monday at 9 AM UTC
  workflow_dispatch: {}    # Manual trigger

jobs:
  curate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run Claude Code Agent
        uses: anthropics/claude-code-action@v1
        with:
          prompt: |
            Research new local-first resources from the past week.
            Use parallel subagents for each source.
            Apply quality gate and open a PR if high-quality content is found.
          anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
```

## Implementation Details

### Claude Code Agent SDK Usage

- Use `@anthropic-ai/claude-code` SDK to orchestrate the lead agent
- Spawn subagents via the SDK's subprocess/tool mechanism
- Each subagent returns structured JSON: `{ entries: [{ url, title, description, source, quality_signals }] }`
- Lead agent merges, dedupes, scores, and generates the final PR

### Edge Cases

- **Rate limiting**: HN Algolia API and GitHub API have rate limits — use conditional requests and caching
- **Newsletter format changes**: If localfirstnews.com changes layout, the agent should gracefully degrade (skip source, don't fail)
- **Empty weeks**: No PR opened — this is expected and not an error
- **Existing PR open**: If a previous auto-curate PR is still open, append to it rather than creating a new one

### Configuration

- Quality threshold (default: 3/4 signals)
- Minimum GitHub stars (default: 50)
- LLM relevance threshold (default: 8/10)
- Source list (configurable list of blogs/feeds to check)
- README section mapping (for categorization)

## Scope

### MVP
- 4 parallel source subagents (newsletter, HN/Reddit, GitHub, blogs)
- Quality filtering with high bar (3/4 signals)
- URL-based deduplication against existing README
- LLM-based categorization into correct README sections
- Single weekly PR with per-entry rationale
- GitHub Actions cron workflow
- Skip silently when nothing qualifies

### Future Enhancements
- [ ] Link-rot detection — verify existing URLs and flag dead links
- [ ] Changelog tracking — maintain a `CHANGELOG.md` of additions over time
- [ ] Community engagement stats — track stars, forks, traffic trends
- [ ] Semantic dedup — embeddings-based near-duplicate detection
- [ ] Configurable source plugins — allow community to add new source agents
- [ ] Slack/Discord notification when a PR is opened
- [ ] Auto-merge after N days if no objections

## Status
**Status:** Spec Complete
**Created:** 2026-02-08
**Priority:** TBD
