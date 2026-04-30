# Side-project / Internal archetype

For personal projects, weekend builds, opinionated tools with a single author, and internal monorepo packages or services that won't be open-sourced. The reader is either someone who found the project through a tweet or blog post, or a teammate looking at it for the first time.

## When to pick this archetype

Side-project flavor:

- Single author or very small team.
- The project exists because the author had a specific complaint with the status quo.
- The reader's goal is "understand the vibe and decide if I care."

Internal flavor:

- Repo is part of a monorepo, used by other teams or services inside an org.
- Most readers are coworkers, not strangers from the internet.
- The reader's goal is "figure out what this thing does and who owns it."

The archetype combines both because they share the same shape: minimal visuals, fast orientation, no marketing.

## Default tone

For side projects: narrative and personal. First person is fine. Sentence-case headings. Short sentences. Willing to name what the project is *not* and what it won't do.

For internal repos: dry and operational. No personality, just facts. Sentence-case or capitalized headings (match the rest of the repo). Always include who owns it and how to reach them.

Pick the flavor based on the project; don't try to do both in one README.

## Visual elements toolkit

Both flavors are visually minimal.

Side-project flavor:

- **No logo, no badges** unless the project has earned them. Stars and downloads on a 50-star side project look sad.
- **Optional one screenshot** if the project is visual (a UI app, a CLI with notable output). One, not three.
- **No comparison tables, no mermaid, no features grid.**
- **Code blocks** for any actual usage. Always real, never pseudo.

Internal flavor:

- **No badges.**
- **No screenshots** unless they meaningfully reduce questions.
- **An "Owner" or "On-call" line near the top.** Names and a Slack channel or paging contact.
- **Run-locally or deploy section** that actually works.
- **Link out to internal docs** rather than duplicating them.

## Section structure

Side-project:

```md
# <name>

<one-line tagline or opening fragment>

<two to four short paragraphs: why this exists, what it does, what it won't do>

## How it works
<prose plus one or two code blocks, conversational>

## Running it
<install + smallest useful invocation; can share a section with How it works>

## Things it won't do
<honest scope, optional but valuable>

## Status
<real talk: where it is, what's broken, whether you'd recommend it>

## License
<one line>
```

Internal:

```md
# <name>

<one-line description: what this service / package / tool does>

**Owner:** <team or names>  ·  **Slack:** `#<channel>`  ·  **On-call:** <pager link>

## What it is
<one paragraph: what it does, who consumes it, where it runs>

## Run locally
<install, env, run; tested commands only>

## Deploy
<one paragraph or link to runbook>

## Architecture
<one paragraph or link to design doc; do not duplicate the design doc>

## Things to know
<gotchas, recent migrations, known bad areas>

## Contacts
<who to ping for what>
```

## Mini example skeletons

**Side-project:**

```md
# comite

A reading-first manga platform. I wanted a place to read that wasn't trying to sell me NFTs, push notifications, or an algorithmic feed. This is that.

It's a single Next.js app on Vercel with a Postgres database and a small set of cron jobs that pull from public chapter feeds. There is no account system, no recommendation engine, no comments.

## How it works

You bookmark a series. You read it. The site remembers your scroll position. That's it.

```bash
git clone https://github.com/me/comite
cd comite
pnpm install
pnpm dev
```

## Things it won't do

- Host pirated content. The cron jobs only pull from feeds the publishers run themselves.
- Run on something cheaper than Vercel. I tried; the cold starts ruined the reading experience.
- Add accounts. If you want sync across devices, this isn't the project.

## Status

Hobby project. I use it daily. About 60 other people seem to use it too. PRs welcome but slow to review.

## License

AGPL-3.0
```

**Internal:**

```md
# pricing-svc

Calculates per-tenant pricing for invoices. Consumed by `billing-svc` and the admin dashboard.

**Owner:** Billing team  ·  **Slack:** `#billing-eng`  ·  **On-call:** [PagerDuty](https://acme.pagerduty.com/services/PRC)

## What it is

A Go service that exposes a gRPC API for pricing lookups. Backed by Postgres (`pricing` schema) with a Redis cache. Deployed on the standard `infra/k8s` chart.

## Run locally

```bash
make dev          # starts Postgres, Redis, and the service
make seed         # loads the staging price catalog
make test
```

Requires Docker, Go 1.22+, and an `INFRA_TOKEN` for staging Vault access.

## Deploy

CI/CD via the standard `deploy` workflow. Production deploys are gated on the Billing team's approval. Runbook: [pricing-svc deploys](https://internal.acme.com/runbooks/pricing-svc).

## Architecture

See the [design doc](https://internal.acme.com/design/pricing-svc-v2). The README intentionally does not duplicate it.

## Things to know

- Cache TTL was reduced from 5m to 30s in March; if you see throughput drops, check `cache_hit_ratio` in Datadog.
- The legacy `/v1/quote` endpoint is deprecated; use `/v2/quote`. v1 is removed in Q3.
- Tests rely on a frozen clock; if you add real time logic, plumb a `Clock` interface.

## Contacts

- Routing / API changes: `@billing-platform`
- Pricing rules: `@pricing-rules`
- Incidents: PagerDuty above
```

## Anti-patterns specific to side-projects and internal repos

Side-project:

- **Pretending it's bigger than it is.** A side project with a 12-section README, a logo, and a Discord that's empty looks worse than the project actually is.
- **Generic "Features" lists.** Either tell the story or list real things you'd brag about to a friend.
- **Adding badges for stats that don't flatter the project.** Skip them.

Internal:

- **No owner field.** The first thing a coworker needs is who to ping.
- **Aspirational sections** ("we plan to refactor," "tests coming soon") that have been there for two years.
- **Duplicating the design doc.** The README points; the doc explains. Otherwise both rot.
- **Skipping "Things to know."** That section is where institutional knowledge lives. It's the most valuable part of an internal README.
