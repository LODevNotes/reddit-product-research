# Reddit Product Research

Turn Reddit posts and comments into practical product opportunity insights, especially for Amazon product research.

This repository contains a Codex skill plus a read-only Reddit JSON helper script. It is designed for research workflows where you collect public Reddit posts/comments, check data completeness, and then analyze user pain points, buying intent, product language, risks, and validation steps.

## What Is Included

- `SKILL.md` - Codex skill instructions for Reddit product research.
- `scripts/reddit-readonly.mjs` - A read-only CLI for public Reddit JSON endpoints.
- `agents/openai.yaml` - Agent metadata for Codex/OpenAI skill usage.

## Requirements

- Node.js 18 or newer.
- Public network access to `reddit.com`.
- No Reddit login, cookies, posting, voting, or moderation access is required.

## Quick Start

Run the script directly with Node:

```bash
node scripts/reddit-readonly.mjs search all "kitchen organizer" --limit 10
node scripts/reddit-readonly.mjs posts CampingGear --sort top --time year --limit 10
node scripts/reddit-readonly.mjs thread "https://www.reddit.com/r/CampingGear/comments/example/" --commentLimit 50 --depth 6
```

Or use the npm script aliases:

```bash
npm run reddit -- search all "kitchen organizer" --limit 10
npm run reddit -- thread "<post_id_or_reddit_url>" --commentLimit 50 --depth 6
```

The CLI prints JSON:

- Success: `{ "ok": true, "data": ... }`
- Failure: `{ "ok": false, "error": ... }`

## CLI Commands

```text
posts <subreddit> [--sort hot|new|top|controversial|rising] [--time day|week|month|year|all] [--limit N]
search <subreddit|all> <query> [--sort relevance|top|new|comments] [--time all|day|week|month|year] [--limit N]
comments <post_id|url> [--limit N] [--depth N] [--includeDeleted true|false] [--maxChars N]
recent-comments <subreddit> [--limit N] [--maxChars N]
thread <post_id|url> [--commentLimit N] [--depth N] [--includeDeleted true|false] [--maxChars N]
find --subreddits "a,b" [--query "..."] [--include "k1,k2"] [--exclude "k3"] [--maxResults N]
```

If your network requires a proxy:

```bash
node scripts/reddit-readonly.mjs search all "camping storage" --limit 10 --proxy http://127.0.0.1:7890
```

## Research Workflow

1. Define the product category, target user, market, subreddit candidates, and English keywords.
2. Collect post-list JSON with `posts` or `search`.
3. Select high-value posts for comment analysis.
4. Collect thread JSON with `thread`.
5. Check whether comments are complete before making conclusions.
6. Extract pain points, buying intent, exact user language, product hypotheses, counter evidence, and Amazon validation steps.

The skill instructions in `SKILL.md` describe the full Chinese-language analysis format and evidence rules.

## Safety And Scope

This project is read-only. It does not log in to Reddit, post, reply, vote, moderate, scrape private data, or request Reddit credentials.

Use Reddit as qualitative evidence, not final market proof. Validate promising ideas with Amazon keyword research, competitor reviews, pricing, compliance checks, and small product tests.

## License

MIT
