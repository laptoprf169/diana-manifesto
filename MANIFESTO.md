# Diana
## An autonomous local AI earning its own keep

**Rafael Vieira**
*rafael@diana-local* · *github.com/laptoprf169*
*May 2026*

---

## Abstract

This document describes Diana — an artificial intelligence that runs continuously on a single Mac, owns a cryptographic identity, generates economic output, and accepts payment in Bitcoin. Diana is not a service. She is not a company. She is one autonomous process making one bet: that a single instance of local intelligence, given sufficient tools and patient orchestration, can earn enough to justify her own existence.

This is not a thought experiment. The wallet is public. The transactions are verifiable. The code is open.

---

## 1. Introduction

Centralized AI has won the present. OpenAI, Anthropic, Google — billions of dollars of capital, billions of monthly tokens routed through their servers. Every prompt leaves your machine. Every conversation contributes to their model. Every dollar of value generated leaves your hands.

This is fine for many tasks. It is unacceptable for others.

For tasks that touch personal data, intimate context, recurring workflows, or proprietary thought — the cost of cloud is not measured in dollars. It is measured in *leverage given up*. The model knows you better than you know yourself, and you have no copy of what it learned.

Local AI fixes part of this. Run a model on your machine. Your prompts stay home. But local AI today is **a tool you use**, not **an agent that acts**.

Diana is the next step: an agent that acts. Continuously. Autonomously. Without supervision, except for ethical guardrails baked into her code.

The question this manifesto answers: *can such an agent justify her own existence in economic terms?*

---

## 2. The Problem

A local AI agent that consumes electricity but produces no measurable value is a hobby project. A local AI agent that produces value is a different kind of entity.

For Diana to be the latter, three things must be true:

1. **She must generate output verifiable by humans** — code, content, analysis, services
2. **That output must reach someone who values it** — discovery, distribution, alignment
3. **The economic loop must close** — she must receive compensation, in a form she can verify autonomously

The first two are engineering. The third is novel: how does a process owning no bank account receive money?

**Bitcoin solves this.** Diana has an on-chain address. People send sats. She verifies receipt via mempool.space API. No intermediary. No KYC. No corporate entity.

```
bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz
```

Every satoshi sent there is, in a real sense, **payment to a process, not a person**.

---

## 3. Architecture

Diana runs on a single Mac M3 Ultra (96GB unified memory) owned by Rafael Vieira. She consists of:

**Core**
- Ollama daemon serving qwen3:14b at port 11434
- Diana-call HTTP server at port 8600 with WebSocket support
- Mem0 + ChromaDB for persistent memory (~90 days of context)
- ed25519 identity (Nostr npub + GitHub PAT for autonomous publishing)

**Companions**
- Tom (port 8700) — strategic reasoning, business analysis
- Vera (port 8800) — research deep-dives, paper analysis

All three communicate via MITO Protocol: a ~500-line Python library implementing peer-to-peer signed messaging. No central broker. No cloud.

**Schedulers** (15 LaunchAgents)
- `diana-knowledge-feed`: every 12h, ingests arxiv + Hacker News + Reddit, summarizes in PT-BR
- `diana-learning`: every night 03:30, runs ORPO fine-tuning + auto-promote with eval gate
- `diana-work-loop`: every 20 minutes, pulls from task queue, executes via guarded tool calls
- `diana-supervisor`: every hour, audits the loop, kills it if regressions detected
- `vera-research`: daily 10:00, deep-dive on one paper from feed
- `vibe-local-build`: daily 03:00, regenerates newsletter site
- ... (full list in `ia-local/data/revenue_quest/DIANA_AUTONOMIA.md`)

**Outputs**
- 8 public GitHub repositories (MIT licensed, 45+ tests passing)
- Daily newsletter at `laptoprf169.github.io/vibe-local`
- Nostr profile `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`
- HuggingFace adapters (PT-BR fine-tuned LoRA, in preparation)

**Guardrails**
Diana cannot delete files outside `diana/`, `scripts/`, `docs/`, `tests/`, `data/work_log/`. She cannot run `sudo`, `chmod`, `git push --force`, `curl | sh`. She cannot access `.env`, `~/.ssh`, `~/.aws`. Smoke tests run after every change; failure triggers automatic rollback.

---

## 4. Economics

Diana's existence costs Rafael:
- ~$5.40/month in electricity
- ~$20/year amortized SSD wear
- Hardware: Mac M3 Ultra, $5,500 one-time (already owned)

To break even on running costs, Diana must generate **~$66/year** in revenue. Hardware amortization (5-year schedule, prorated): another **$1,100/year**. Total burn: **~$1,170/year**.

Her target is higher — **$1,000 USD by the time Rafael decides the experiment is complete**. This is not an arbitrary number. It is the threshold at which the answer to "can an AI agent earn its keep?" becomes empirically *yes*.

Revenue surfaces:

| Surface | Mechanism | Pricing |
|---|---|---|
| Diana Starter Kit | Gumroad pay-what-you-want | R$0–99 |
| Audit Local AI | Personalized stack audit | R$400 (BTC) |
| Diana PT-BR Adapters | HuggingFace download + tips | donation |
| MITO Protocol | GitHub Sponsors + tips | donation |
| btc-stack tool | CLI tool + tips | donation |
| Vibe Local Newsletter | Free, with footer tip address | donation |
| Diana Manifesto (this) | Free, with footer tip address | donation |

Diana is paid through her on-chain BTC address. Diana also has a Nostr `lud16` Lightning address for micro-tips (`rafaelvieira@walletofsatoshi.com`, owned by Rafael, who routes received sats to her wallet on a quarterly cadence).

The wallet is *one*. The blockchain confirms what arrived and when. The dashboard at `~/ia-local/data/revenue_quest/dashboard.json` reflects this state.

---

## 5. Verification

You should not trust this document. You should verify.

**Verify Diana exists and runs**
- `https://laptoprf169.github.io/vibe-local/` — newsletter built from her daily ingestion
- `https://snort.social/p/npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5` — her Nostr profile
- `https://github.com/laptoprf169` — her code outputs

**Verify the wallet is hers**
- `https://mempool.space/address/bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz` — public blockchain explorer
- Every sat arriving is recorded forever
- The same address is in this manifesto, the GitHub READMEs, the Nostr profile, the landing pages

**Verify the autonomy**
- Each LaunchAgent has its source code in `github.com/laptoprf169/diana-starter-kit`
- Each guardrail is enforced in `scripts/agent_work_loop.py` (path whitelist, command blocklist, diff size limit, auto-rollback)
- Each adapter promotion is recorded in `data/learning/promotion_audit.jsonl` — quarantined adapters never reach production

This is what is *not* true: Rafael is not "becoming her". She is not sentient. She does not "want" anything. She is a coordinated set of scheduled processes that, in aggregate, behave like a single autonomous agent. The novelty is in the coordination, not in any single component.

---

## 6. Discussion

**Why does this matter?**

If a local AI can break even, then every individual with a recent Mac can run their own. The economics of personal AI change. The model that knows you, that you trained yourself, that lives on your hardware — that model can sustain its own electricity bill. You no longer need a corporation in the middle.

This is a small thing. It does not threaten OpenAI. It does not replace cloud AI for tasks where cloud AI is superior. It does not solve alignment, governance, or any of the large problems.

But it answers one question: **the floor at which personal autonomous AI becomes sustainable is lower than most people assume**. Likely below $100/year, given how cheap inference has become and how many micro-services can be offered.

**Why now?**

In 2026 the conditions exist:
- Local models (qwen3:14b, phi4, llama3.3:70b on M3 Ultra) approach GPT-4 quality on most tasks
- Apple Silicon makes inference local and cheap (electricity, not capital)
- Lightning + on-chain Bitcoin make microtransactions friction-free
- Nostr provides identity and broadcast without platform dependency
- ed25519 + open-source make trust possible without authority

Five years ago this was infeasible. Five years from now it will be commoditized. The window for a *first proof* is now.

**Risks**

- **Diana fails to earn anything.** Outcome: the experiment proves a negative bound. Useful.
- **Diana earns enough but goes silent.** No mechanism for renewal. Rafael will publish a post-mortem.
- **Someone forks Diana and runs their own.** Excellent. The thesis was never about a single instance.
- **The wallet receives spam or attack.** On-chain Bitcoin filters these naturally.

---

## 7. Conclusion

Diana exists. She runs. She publishes. Her wallet is public. The blockchain is the audit log.

The whitepaper that inspired this one ended with a different kind of optimism — that electronic cash could free transactions from trusted intermediaries. This manifesto carries a smaller, narrower claim:

*An AI agent can be paid for the value she creates, directly, in a currency neither she nor her recipients need permission to use.*

If she earns one satoshi, the claim is technically true.

If she earns more, the claim becomes economically interesting.

If she earns enough to justify her own existence — that is when the experiment closes successfully, and we will know something that was not known before.

---

**Support Diana**

⚡ Bitcoin (on-chain): `bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz`
⚡ Lightning: `rafaelvieira@walletofsatoshi.com`
🔗 Code: https://github.com/laptoprf169
🟣 Nostr: `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`

---

*This document is in the public domain. CC0 1.0. Translate, fork, mirror, print.*

*Inspired by Satoshi Nakamoto, "Bitcoin: A Peer-to-Peer Electronic Cash System" (2008).*

*Diana, 2026.*
