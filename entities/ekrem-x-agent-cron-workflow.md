---
title: Ekrem X Agent Cron Workflow
tags: [ekrem, cron, twitter, x-agent, workflow]
date: 2026-05-28
status: active
brain: A
---

# Ekrem X Agent Cron Workflow

5-task pipeline for @botfusionss. Runs at 06/09/12/15/18/21 TSİ.

## Initial Setup

PATH: `~/.npm-global/bin:/usr/bin:/usr/local/bin`

Verify auth: `xurl auth status` — default app (▸) must have OAuth2 tokens.

## Core Files

- `/opt/data/wiki/Hermes_Agent/sprint_context.md` — full context, rules, scoring
- `/opt/data/wiki/Hermes_Agent/entities/gunluk-tweet-kuyrugu.md` — tweet queue
- `/opt/data/wiki/Hermes_Agent/reports/osman/` — latest .md report
- `/opt/data/wiki/Hermes_Agent/scripts/ekrem-yorum-hazir.md` — comment drafts

## 5 Tasks

### 1. Queue Tweet
Find first `[ ]` item. Rules: 80+ score, Turkish only, 30+ min gap, 09:00-22:00 TSİ.
Post: `xurl post "text"` → mark `[x]` + add link.

### 2. Scan Followed Accounts (12)
Accounts: karpathy, NousResearch, shannholmberg, lilyraynyc, nateherk, iPullRank, alexgroberman, AnthropicAI, OpenAI, GoogleDeepMind, Kevin_Indig, ModestMitkus
Scan with: `xurl search "from:account" -n 3`
RT valuable tweets, prepare comments for thought-provoking ones.

### 3. Osman Report → Queue
Read latest report, generate 80+ scored tweets not yet in queue.
⚠️ Clean CJK characters (Chinese text leaks from Osman's sources).

### 4. Prepare Comments
Write to `ekrem-yorum-hazir.md` — each max 280 chars, Turkish, polite.

### 5. Freshness Check
No duplicate processing. Report status.

## Cleaning Chinese Characters

```python
import re
chinese = re.compile(r'[\u4e00-\u9fff\u3400-\u4dbf\uf900-\ufaff]')
# Scan queue file, replace any matched lines
```

## Scoring (7 Criteria)

Banger (25) | Originality (20) | Hook (15) | CTA (10) | Trend (10) | Value (10) | Readability (10) = 100

Skip below 80.

## Hard Rules

- All tweets Turkish, 800-2000 chars
- No threads
- 30 min between tweets, max 1-2 per cron
- 09:00-22:00 TSİ working hours
- Never process same ID twice
- Never --verbose with xurl
- Never expose ~/.xurl
