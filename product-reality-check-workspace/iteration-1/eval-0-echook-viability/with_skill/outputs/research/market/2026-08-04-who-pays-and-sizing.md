# echook — Who Pays, and How Much: Bottom-Up Sizing

**Date:** 2026-08-04
**Subject:** [github.com/ChanMeng666/echook](https://github.com/ChanMeng666/echook) — MIT, Python, solo maintainer, 9 months, zero revenue, no telemetry
**Question:** Is there a business here, who exactly would pay, and should the owner keep going or keep it a free portfolio piece?

**Sourcing:** every external claim carries a URL fetched or queried this session, graded `[PAGE]` (fetched, read the number), `[PRIMARY]` (queried a live API myself), `[SNIPPET]` (search-result snippet only), `[UNVERIFIED]`. No top-down sizing appears anywhere in this document — not one sentence of it.

---

## THE VERDICT, FIRST

> **No — not as stated. This is a $0–$200/year business, which is not a business, and not the one nine months of full-time-quality engineering is priced for.**

The reasoning follows. The conditions under which this answer changes are in the final section, and two of them are cheap enough to test this month.

---

## Measured facts about the subject (first-hand, this session)

These are not inferences. I queried them directly on 2026-08-04.

| Fact | Value | Source |
|---|---|---|
| echook stars | **78** (brief said 79 — it lost one) | GitHub REST API `/repos/ChanMeng666/echook` `[PRIMARY]` |
| Forks / open issues | 7 / 1 | same `[PRIMARY]` |
| Created | 2025-11-01 | same `[PRIMARY]` |
| Last push | 2026-07-19 | same `[PRIMARY]` |
| Licence | MIT | same `[PRIMARY]` |
| On PyPI? | **No — HTTP 404.** Install is `git clone` / plugin-marketplace add | `pypi.org/pypi/echook/json` `[PRIMARY]` |
| Owner followers | 222 | GitHub GraphQL `[PRIMARY]` |
| Owner has a GitHub Sponsors listing? | **Yes** | GitHub GraphQL `[PRIMARY]` |
| Owner public sponsors | **0** | GitHub GraphQL `[PRIMARY]` |
| Funding config | `github: ChanMeng666` + `buy_me_a_coffee: chanmeng66u` | repo `.github/FUNDING.yml` |
| README already carries a hire-me pitch | Yes — "Need a custom app like this one? I build them — let's talk" + `mailto:` | repo `README.md` line 429 |

**Read the fourth-from-last row twice.** The monetisation hypothesis this report was commissioned to evaluate has *already been run as a live experiment*, for nine months, in front of 222 followers, and it has returned exactly zero. Everything below is an attempt to find a pool that experiment did not test.

---

## The two constraints that dominate every archetype

Before any archetype, two structural facts. They are not opinions and they cap every price in this document.

### Constraint 1 — There is no payment rail. In any of the three ecosystems.

This is the single most decisive finding in the report, and it is established at the *schema* level, not from commentary:

- **Claude Code.** A marketplace is a git repository containing `.claude-plugin/marketplace.json`; installation is a `git clone` of a pinned SHA into `~/.claude/plugins/cache`. An exhaustive grep of the full marketplace documentation (73.8 KB) for `price|paid|payment|billing|monetiz|purchase|licens|commercial|cost|subscri` returns **exactly two hits: the `license` SPDX field, and the string `"license": "MIT"` in an example.** The full plugin manifest schema has no price, payment, entitlement, or licence-key field. [code.claude.com/docs/en/plugin-marketplaces](https://code.claude.com/docs/en/plugin-marketplaces) + [code.claude.com/docs/en/plugins-reference](https://code.claude.com/docs/en/plugins-reference) `[PAGE, exhaustive grep]`
- **Cursor.** "Cursor uses the Open VSX extension registry for third-party extensions, with Cursor's marketplace proxy applying automated malware and supply-chain analysis before extensions are offered for install." No paid tier, no selling mechanism. [cursor.com/help/customization/extensions](https://cursor.com/help/customization/extensions) `[PAGE]`
- **Codex CLI.** A `/plugins` browser that groups plugins by marketplace and installs or uninstalls entries. No pricing, no monetisation. [learn.chatgpt.com/docs/plugins](https://learn.chatgpt.com/docs/plugins) `[PAGE]`
- **And the mature analogue has never had one either.** VS Code's `package.json` `pricing` property "Allowed values are: `Free` and `Trial` (case-sensitive)." **There is no `Paid` value.** The canonical request, [microsoft/vscode#90648 "Add support for premium extensions"](https://github.com/microsoft/vscode/issues/90648), was opened 2020-02-14 and is **still open** as of this session. `[PAGE]` × 2

Corroborating measurement across all public GitHub: **15,728** `.claude-plugin/marketplace.json` files exist. Three of them mention Gumroad. One mentions Polar. `[PRIMARY, GitHub code search 2026-08-04]`

There is no gate to put a paywall behind, because installing a plugin is `git clone`.

### Constraint 2 — echook is MIT and already public, so the price ceiling is set by echook itself.

Any buyer — an individual, a 5,000-developer bank, Anthropic — can decline to pay and keep the software forever, including forking every future version. This is not a risk; it is a completed, irreversible act. It means:

- **No ACV in this document can be defended as a price for the software.** Every non-zero number below is a price for something echook does *not* currently sell: support, integration labour, hosting, a warranty, or a person's time.
- The one thing MIT does not give away is **the maintainer**. That observation is the thread the verdict section pulls on.

**A note on the native-feature question, because the brief's premise is half wrong and the correction matters.** A regex sweep of the entire Claude Code changelog (v0.2.6, 2025-02-24 → v2.1.221) for `sound|audio|bell|chime|speech|TTS` returns **14 hits, none of them an audio notification feature** — all are voice *input* (dictation, mic, SoX, ALSA) or terminal-bell bug fixes. [anthropics/claude-code CHANGELOG.md](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md) `[PAGE]`. **Claude Code has never shipped native audio notifications.** What it shipped is a statusLine *API* (pre-calculated `context_window.used_percentage` v2.1.6, 2026-01-13; `rate_limits` v2.1.80, 2026-03-19) and *mobile push* via Remote Control (v2.1.110, 2026-04-15). So echook's status-line track faces a native equivalent; its audio track does not. That is a genuine residual — and it still does not produce a payable pool, for the reasons in A1.

---

## ARCHETYPE A1 — The individual Claude Code / Cursor / Codex power user

### Who — a real, enumerable population

I cannot name five *companies* here because the buyer is a person; the brief's alternative is "a real findable population," and this one is findable to the individual username:

1. **The 12,205 stargazers of `sirmalloc/ccstatusline`** — a literally enumerable GitHub list of humans who cared enough about a Claude Code status line to star it. `[PRIMARY, GitHub API 2026-08-04]`
2. **The 17,700 stargazers of `ryoppippi/ccusage`** — same, for usage monitoring. `[PAGE, GitHub API]`
3. **407,682 monthly npm installs of `ccstatusline`** (2026-07-04 → 08-02) and **445,521 of `ccusage`** — the behavioural, not aspirational, size of the customisation habit. Downloads are not humans (CI, re-installs, containers inflate them); I use them as an upper bound and the star counts as the human floor. `[PRIMARY, api.npmjs.org]`
4. **380,000+ monthly visitors to claudemarketplaces.com**, a directory indexing "23,500+ skills, 2,600+ marketplaces, 12,700+ MCP servers." `[PAGE]`
5. **echook's own 78 stargazers + 7 forkers**, plus the owner's 222 followers. `[PRIMARY]`

### Price anchor `[PAGE]`

**Pushover — $4.99 USD one-time purchase on each platform** (iPhone/iPad, Android, Desktop), free for 30 days, "There are no subscription fees for individuals," 10,000 messages/month free. [pushover.net/pricing](https://pushover.net/pricing) `[PAGE]`

**Analogy label — and it runs against echook.** Pushover is the closest *shape* (a notification utility sold to individuals at a one-time price) but it is not the same *good*: Pushover operates a hosted push-delivery network, publishes native mobile apps on three stores, and is closed-source. The $4.99 buys access to infrastructure the buyer cannot reproduce. echook is a local Python script under MIT. **Pushover's $4.99 is an upper bound on echook's price, not a comparable.**

Secondary anchors, both survivors of exactly the platform-absorption event echook faces, both showing what a *defensible* one-time licence looks like:
- **Alfred Powerpack — £34 single-user, £59 Mega Supporter with lifetime upgrades**, one-time perpetual. [alfredapp.com/powerpack](https://www.alfredapp.com/powerpack/) `[PAGE]` — closed source.
- **Raycast — Free $0; Pro $8/mo annual; Teams Pro $12/user/mo.** Note precisely *what* is behind the paywall: the free tier includes Window Management and Clipboard History; the $8 buys **cloud sync and AI**. [raycast.com/pricing](https://www.raycast.com/pricing) `[PAGE]`

And the buyer's existing spend, for context on the wallet: Claude Pro is **"$17 Per month with annual subscription discount ($200 billed up front). $20 if billed monthly"**; Max **"From $100 Per month."** [claude.com/pricing](https://claude.com/pricing) `[PAGE]`

### Buyer count — exists vs. reachable, kept strictly separate

| | Count | Basis |
|---|---|---|
| **Exists** (whole archetype) | **12,000–30,000 identifiable humans** | union of ccstatusline + ccusage stargazers, as the enumerable human floor under the ~850k combined monthly npm installs `[PRIMARY]` |
| **Reachable** by an unknown solo maintainer with 78 stars, no mailing list, no PyPI package, no telemetry | **~300 people, generously** | 78 stargazers + 7 forkers + 222 followers, overlap unknown and probably large `[PRIMARY]` |

The gap is **40× to 100×**. Conflating these two numbers is exactly where this kind of sizing inflates by an order of magnitude, so I am naming the gap rather than averaging it away.

Two aggravating details on reachability. **echook is not on PyPI** — there is no registry that surfaces it to a stranger and no download counter that would tell the owner how many users he has `[PRIMARY, HTTP 404]`. And the acquisition curve is decelerating: 19 new stars in April 2026, 4 in July 2026, net −1 since this brief was written (established earlier this session; 78 measured `[PRIMARY]`).

### Realistic ACV — reasoning visible

Start at Pushover's **$4.99 one-time**. Discount for what echook does not provide, itemised:

| Discount for | Effect |
|---|---|
| No hosted delivery network (Pushover's actual product) | −large |
| No native mobile apps on three stores | −large |
| No support obligation, no SLA, no warranty | −moderate |
| No team features, no SSO, no audit trail | n/a at this tier |
| **A free substitute that is byte-identical to the product, under MIT, already public** | **→ the price is not a price; it is a voluntary tip** |

The last row is not a discount, it is a change of category. So the honest ACV is **not $4.99 — it is "whatever fraction of users voluntarily tip, times whatever they tip."** And that quantity has been measured, twice, in this exact niche:

- **The owner's own GitHub Sponsors listing: 0 sponsors, 222 followers, 9 months.** `[PRIMARY]`
- **In the 70–90-star band across GitHub, 85% of repo owners have no Sponsors listing at all and 93% have zero public sponsors; the median is 0.** `[PRIMARY, 94 sampled owners, GitHub GraphQL, 2026-08-04]`

**Realistic ACV: $5 one-time, at a 0–10% conversion of the reachable population.**

### Realistic pool

300 reachable × 0–10% × $5 = **$0–$150 one-time**. Allowing for a trickle of new arrivals: **$0–$200/year. The median outcome is $0**, and the expected value is dominated by the fact that the experiment has already run and returned $0.

### Stretch pool — LABELLED

If the *entire archetype* — all 12,000–30,000 identifiable Claude Code customisers, across every notification and status-line utility in the ecosystem, not this one — paid a $5 one-time licence: **$60,000–$150,000, one-time, spread across every vendor in the category.** This is the whole industry's ceiling at Pushover pricing, not echook's revenue, and no single project could capture more than a slice of it.

**The stretch pool has already been falsified by the one project that owns that audience.** `ccstatusline` has 12,205 stars and 407,682 monthly installs — 156× echook's stars — and its entire monetisation apparatus is one line: `buy_me_a_coffee: sirmalloc`. `[PRIMARY, .github/FUNDING.yml fetched 2026-08-04]`

### Adversarial note (mandatory)

**The strongest reason this archetype does not pay: it is being asked to pay for something it already owns, for a job it can do in twenty lines.** Claude Code hooks are available on *every* provider and every plan (Anthropic's own feature matrix lists "Subagents, **hooks**, commands, and skills" under "Features available on every provider" [code.claude.com/docs/en/feature-availability](https://code.claude.com/docs/en/feature-availability) `[PAGE]`). A developer who wants a sound when the agent finishes writes a `Stop` hook that calls `afplay`/`paplay`/`powershell` in an afternoon — and echook's own MIT source is the reference implementation for doing so. echook's value is breadth (39 events × 3 editors × TTS × webhooks × status line), and breadth is precisely what an individual does not need: they need one sound, once.

### Structural volume ceiling

There is nothing to meter. No server, no seats, no per-message cost, no storage — by design, and the design is correct. Revenue can therefore only ever be a **one-time payment per human**, never a subscription, which means the pool cannot compound and is capped by the audience-acquisition rate (currently 4 stars/month and falling).

---

## ARCHETYPE A2 — Organisations locked out of the native path (Bedrock / Vertex / Foundry / gateway / API-key / ZDR)

This archetype **absorbs the "engineering orgs running fleets of parallel agents" archetype**, and I want to be explicit about why rather than quietly dropping it: I could not name five real companies verifiably running fleets of background Claude Code agents *and* plausibly buying a notification utility, and the brief's rule is that an archetype that fails the five-names test is imaginary and must be deleted or merged. It is merged here because the populations overlap almost entirely (both are large enterprises with central Claude Code deployments) and because the product a fleet operator would actually buy is a **fleet dashboard**, not a sound at one developer's desk — a different product, which echook is not.

### Who — the population is first-party documented, but I could not name five members

The exclusion is real, precise, and published by Anthropic. From the feature-availability matrix, under **"Features that require a Claude subscription"** — "These require signing in with a claude.ai account and are **not reachable with an Anthropic Console API key or from a third-party provider**" — the list includes **Remote Control**, Claude Code on mobile, Claude Code on the web, Desktop, Routines, and voice dictation. [code.claude.com/docs/en/feature-availability](https://code.claude.com/docs/en/feature-availability) `[PAGE]`

Remote Control is the carrier for native push. So every organisation authenticating via **Amazon Bedrock, Claude Platform on AWS, Google Cloud's Agent Platform (formerly Vertex AI), Microsoft Foundry, an Anthropic Console API key, or an LLM gateway** — the gateway case being explicit: "If you authenticate through an LLM gateway, feature availability matches the underlying provider" `[PAGE]` — provably **cannot receive a native notification when its agents finish or need a decision.** Meanwhile **hooks work on every one of those providers** `[PAGE]`. The gap echook fills is real, documented, and dated.

Anthropic's enterprise deployment page confirms the same six-way deployment split and the corporate-proxy / `ANTHROPIC_BASE_URL` gateway configurations. [code.claude.com/docs/en/third-party-integrations](https://code.claude.com/docs/en/third-party-integrations) `[PAGE]`

**But I could not name five such organisations this session** (the session-wide WebSearch budget was exhausted before this analysis began; see Open Gaps). The population is *findable in principle* — AWS Bedrock and Google Cloud publish customer case studies — but I did not enumerate it, and I will not manufacture names. **This is the report's highest-value open gap, and it is closeable by outreach in days, not by more research.**

### Price anchor `[PAGE]`

- **Pushover for Teams — "$5 USD per-user, per-month"**, all platforms included. [pushover.net/pricing](https://pushover.net/pricing) `[PAGE]` — the closest team-notification analogue: **$60/user/year**. Analogy caveat: again a hosted service with mobile apps.
- **PagerDuty Professional — $25/user/month monthly, $21/user/month annual; Business $49/$41.** [pagerduty.com/pricing](https://www.pagerduty.com/pricing/) `[PAGE]` — **$252/user/year** at the annual Professional rate. Analogy caveat, and it is severe: PagerDuty sells on-call scheduling, escalation policies, incident timelines, an audited event pipeline and an availability SLA. echook shares only the word "notification."

### Buyer count — exists vs. reachable

| | Count | Basis |
|---|---|---|
| **Exists** | Unknown, but provably non-zero and structurally large — every Bedrock/Vertex/Foundry/gateway/ZDR Claude Code deployment | Anthropic's own exclusion matrix `[PAGE]` |
| **Reachable** by an unknown solo maintainer with 78 stars, no company, no SOC 2, no case study, no reference customer | **0 named, 0 verified** | this session |

### Realistic ACV — reasoning visible

Anchor at Pushover Teams' **$60/user/year** and discount:

| Discount for | Effect |
|---|---|
| No hosted delivery, no mobile app | −large |
| No SSO, no audit log, no admin console, no central policy | −large (these are the *only* things enterprises buy notification tooling for) |
| No SLA, no support contract, no security review artefacts, no SBOM | −large |
| No seats to meter — nothing recurring exists to sell | recurring ACV → **$0** |
| **MIT, public, forkable forever** | any procurement lawyer's first observation |

**Realistic recurring ACV: $0.** Not "small" — structurally zero, because there is no metered unit and no contract surface. If an org paid at all it would be a **one-off integration/support engagement**, and Clutch's first-party data puts custom software projects in the **$10,000–$49,999** band [clutch.co/developers/pricing](https://clutch.co/developers/pricing) `[PAGE]` — but that is **consulting revenue, not a product ACV**, and it belongs to the portfolio/lead-gen path in the companion base-rates file, not here.

### Realistic pool

**Reachable (0) × ACV = $0/year.** This stays $0 until a single named organisation exists. It is not $0 because the need is fake; it is $0 because nobody has been asked.

### Stretch pool — LABELLED

If a hypothetical company (not this maintainer) sold a *supported, hosted, SSO-equipped* agent-notification product at Pushover-Teams pricing into 50 locked-out orgs averaging 200 developers: 50 × 200 × $60 = **$600,000/year** — for the whole category, for a product with a server and a support team, i.e. **not echook and not this owner.** Reaching it requires building the four things the discount table above just removed.

### Adversarial note (mandatory) — this one inverts the premise

**The compliance-constrained org is the *hardest* buyer for an unknown solo maintainer, not the easiest.** The reason an org is on Bedrock, an LLM gateway, or Zero Data Retention is that its security function has veto power over what touches developer machines and what leaves the network. That same function will not approve an unaudited third-party Python package, installed by `git clone` from a 78-star personal GitHub repo, that opens the microphone-adjacent audio stack and **fans out webhooks to Slack, Discord, Teams and ntfy** — an egress path, on the machines whose egress is the entire reason they chose ZDR. The very property that creates the need destroys the purchase.

And the fallback is trivially available: hooks work on every provider `[PAGE]`, so a platform team writes an internal 20-line notifier — reviewed, owned, and inside the trust boundary — in an afternoon. They may well read echook's MIT source to do it. That is a compliment, not a transaction.

One further deflation specific to this population: echook's **rate-limit bars are meaningless here.** Bedrock, Vertex and Foundry bill pay-as-you-go through the cloud provider `[PAGE, third-party-integrations]`; there are no 5-hour/7-day subscription rate limits to visualise. Half of echook's status-line value proposition does not apply to the archetype that most needs its other half.

---

## ARCHETYPE A3 — The AI-coding-tool vendors themselves (would one license or acquire it?)

### Who — five real, named, correctly-scoped organisations

Anthropic · Anysphere (Cursor) · OpenAI · GitHub/Microsoft · Sourcegraph. (Replit, Vercel and Warp are adjacent and were also checked.) These are real and reachable — a cold email to any of them is deliverable. Whether it is *answerable* is the question.

### Price anchor — **the absence IS the finding**

**No licensing deal of this shape was found to exist.** Not "the price is low" — *the transaction type has no observed instance.* Across every acquisition and hire I could verify in this ecosystem, no AI-coding vendor has ever licensed a third-party desktop utility for a fee while leaving it independent. What exists instead is **acquisition**, and the observed entry price is adoption, not code:

| Deal | Adoption at the moment of the deal | Date | Source |
|---|---|---|---|
| **Anthropic acquires Bun (Oven Inc.)** | **"more than 7 million monthly downloads," "over 82,000 stars on GitHub"** | 2025-12-03 | [anthropic.com/news/anthropic-acquires-bun…](https://www.anthropic.com/news/anthropic-acquires-bun-as-claude-code-reaches-usd1b-milestone) `[PAGE]` |
| Vercel hires Rich Harris for Svelte | "over 200,000 weekly downloads, more than 50,000 GitHub stars" | 2021-11-11 | [vercel.com/blog/vercel-welcomes-rich-harris…](https://vercel.com/blog/vercel-welcomes-rich-harris-creator-of-svelte) `[PAGE]` |
| GitLens / Eric Amodio → GitKraken | "11 million active users and 71 million downloads over five years" | 2021-10-08 | [prnewswire.com/news-releases/gitlens-…](https://www.prnewswire.com/news-releases/gitlens-for-visual-studio-code-and-its-creator-eric-amodio-join-gitkraken-301396298.html) `[PAGE]` |
| Don Jayamanne → Microsoft (VS Code Python ext.) | "over 4.2 million downloads" | 2017-11-09 | [devblogs.microsoft.com/python/don-jayamanne-joins-microsoft](https://devblogs.microsoft.com/python/don-jayamanne-joins-microsoft/) `[PAGE]`; download figure `[SNIPPET]` |
| Anthropic acquires Stainless | funded company, ~$300M reported | 2026-05-18 | `[SNIPPET]` |
| Anthropic / Humanloop | **acqui-hire of the team; no assets or IP acquired** | 2025-08-13 | [techcrunch.com/2025/08/13/…](https://techcrunch.com/2025/08/13/anthropic-nabs-humanloop-team-as-competition-for-enterprise-ai-talent-heats-up/) `[PAGE]` |
| Anysphere ← Supermaven | venture-backed company, $12M Series A led by Bessemer | 2024-11-12 | `[SNIPPET]` |
| Anysphere ← Koala | enterprise CRM startup, hired for enterprise-readiness team | 2025-07-18 | `[SNIPPET]` |

**Every AI-coding-era deal is a funded company with a team, or a project with tens of thousands of stars and millions of downloads. Not one is a solo, unfunded ecosystem utility.**

### Buyer count

Exists: 5–8 vendors. **Reachable: all of them** (cold email is deliverable). **Reachable-with-a-transaction-they-recognise: 0**, because the transaction does not exist in their history.

### Realistic ACV

**Undefined — deliberately not a number.** Writing "$25,000 licence" here would be inventing an ACV for a deal type with zero observed instances, which is the failure mode this report is built to avoid. The observed price of the *nearest real* transaction (acquisition) is 82,000 stars and 7M monthly downloads `[PAGE]` — roughly **three orders of magnitude** above echook's 78 stars.

And Constraint 2 bites hardest here: **Anthropic can vendor echook's MIT code into Claude Code tomorrow, for free, with attribution, and owes nothing.** A vendor's alternative to paying is not "build it" — it is "copy it, legally, today."

### Realistic pool

**$0/year.**

### Stretch pool — LABELLED

An acquihire. Priced in the companion base-rates file as a lottery ticket at 3–5 orders of magnitude above current adoption, with **zero precedent of any Claude Code community plugin/hook/status-line maintainer being hired or acquired by anyone**. Not addable to anything.

### Adversarial note (mandatory)

**A vendor's reason not to pay is stronger than "we'd build it" — it is "we already shipped it, deliberately, as an API, and third parties rendering it is the design."** Anthropic did not merely add a status line; it shipped `statusLine` as an extension point in v1.0.71 (2025-08-07) and then spent eight months making third-party status lines *easier* to write (`context_window.used_percentage` v2.1.6, 2026-01-13; `rate_limits` v2.1.80, 2026-03-19) `[PAGE, CHANGELOG + npm publish timestamps]`. A vendor that wants an ecosystem of free status-line renderers has no reason to buy one of them. Buying one would end the ecosystem it just built.

---

## ARCHETYPE A4 — Agent-observability SaaS wanting a notification layer

### Who — five real, named companies

**Langfuse** · **Helicone** · **LangSmith (LangChain)** · **PagerDuty** · **Datadog** (LLM Observability). All real, all funded, all with published pricing, all reachable by email.

### Price anchors `[PAGE]` — all fetched this session

| Vendor | Pricing | Source |
|---|---|---|
| **Langfuse** | Hobby $0 (50k units, 2 users) · **Core $29/mo** · **Pro $199/mo** · **Enterprise $2,499/mo**; overage "$8/100k units"; open source and self-hostable free | [langfuse.com/pricing](https://langfuse.com/pricing) `[PAGE]` |
| **Helicone** | Hobby free (1 seat, 10,000 requests) · **Pro $79/mo** unlimited seats · **Team $799/mo** · Enterprise custom | [helicone.ai/pricing](https://www.helicone.ai/pricing) `[PAGE]` |
| **LangSmith** | Developer **$0/seat** (5k traces) · **Plus $39/seat/mo** (10k traces) · Enterprise custom, self-hosted available; usage at "$1.50 / LCU", "$1.00 / LSU" | [langchain.com/pricing-langsmith](https://www.langchain.com/pricing-langsmith) `[PAGE]` |
| **PagerDuty** | Free (5 users) · **Professional $21/user/mo annual** · **Business $41/user/mo annual** · Enterprise custom | [pagerduty.com/pricing](https://www.pagerduty.com/pricing/) `[PAGE]` |

**Analogy label, and it is fatal.** Look at what every single one of these prices is *denominated in*: units, traces, requests, LCUs, storage, seats-with-a-server. Langfuse charges $8 per 100k units. LangSmith charges per trace. Helicone counts requests. **Every one of these businesses sells hosted storage and compute over data the customer sends them.** echook, by explicit design, **has no telemetry of any kind** — it produces zero data, sends nothing anywhere, and stores nothing. It is definitionally unmeterable by every pricing model in this table.

### Buyer count

Exists: 5–15 vendors in agent/LLM observability. **Reachable by an unknown solo maintainer: all 5 by email; 0 with a warm intro or a reference.**

### Realistic ACV

An observability vendor buying a "notification layer" would be buying either (a) code — free under MIT, so $0 — or (b) an engineer's time to integrate it. Discount from the smallest paid tier in the table ($29/mo Langfuse Core) for: no data, no hosting, no multi-tenancy, no SDK, no auth model, no dashboard, and a free identical substitute.

**Realistic ACV: $0.** The nearest defensible non-zero figure is a contract-engineering rate — freelance AI/ML specialists at **$100–$250/hour** `[SNIPPET, freelanly.com]`, or Clutch's $24–$49/hr agency band `[PAGE]` — which is, again, consulting revenue, not a product sale.

### Realistic pool

**$0/year.**

### Stretch pool — LABELLED

If an observability vendor built and *sold* an agent-notification tier at Langfuse Core's $29/mo to 500 customers: **$174,000/year — for that vendor's product, with that vendor's server, brand, and support**, not for echook and not for this maintainer.

### Adversarial note (mandatory)

**Notifications are not a moat, they are a sprint — and the MIT licence removes even the negotiation.** A funded observability company with a Slack webhook already in its codebase adds "notify when the agent finishes" in one iteration; a desktop *sound* is not something a cloud-hosted observability product wants at all, because its customers are watching a dashboard, not sitting at the terminal echook makes noise on. And in the one case where it *did* want the code, it can copy it today for free. There is no version of this conversation in which money changes hands for the artefact.

---

## SUM — realistic pools

Summed arithmetically. Stretch pools are **not** included and are never added.

| Archetype | Reachable buyers | Realistic ACV | **Realistic annual pool** |
|---|---|---|---|
| A1 · Individual power user | ~300 | $5 one-time @ 0–10% conversion | **$0–$200** |
| A2 · Locked-out / compliance-constrained org | 0 named | $0 recurring (no meterable unit) | **$0** |
| A3 · AI-coding-tool vendors | 5 reachable, 0 with a known transaction type | undefined — no deal of this shape exists | **$0** |
| A4 · Agent-observability SaaS | 5 | $0 (unmeterable: zero telemetry by design) | **$0** |
| | | **TOTAL REALISTIC** | **$0–$200 / year** |

**Median outcome: $0.** The band's entire width comes from A1 tips, and A1's conversion rate has already been measured at zero on this exact repository, by this exact owner, over nine months.

**Stretch pools, reported separately and never added to the above:** A1 $60k–$150k one-time *across the whole ecosystem and every vendor in it*; A2 $600k/yr *for a hypothetical hosted, supported, SSO-equipped company that is not this one*; A4 $174k/yr *for an observability vendor's own product line*. **None of these is echook's revenue under any reading**, and each requires building precisely the things (server, support, seats, data) that the discount tables removed.

**A percentage, stated with its pool, as the brief requires:** capturing **100% of the realistic total annual pool** ($200) would be **less than 1%** of what nine months of engineering at the freelance AI-specialist rate of $100–$250/hour `[SNIPPET]` would have billed.

---

## THE VERDICT

> **No — not as stated. This is a $0–$200/year business, which is not a business, and not the one nine months of work is priced for.**

It is, however, a genuinely good piece of software with a real and documented gap to fill — and those two sentences are not in tension. See "What this report does NOT say."

### Conditions under which the answer changes

Each is precise enough to go test. **Researched** means I have evidence bearing on it; **HYPOTHESIS (unresearched)** means I do not, and it must be read as a question, not a lane.

**C1 — A payment rail ships in the Claude Code plugin marketplace. `[RESEARCHED — currently false]`**
Today the manifest schema has no price field and installation is `git clone` `[PAGE, exhaustive grep]`. If Anthropic ships paid plugins, A1's ACV becomes a real price instead of a tip, and the whole analysis is re-run. Note this changes the rail, **not** Constraint 2: echook would still be MIT and forkable, so it would have to ship a *new* proprietary component to have anything to sell. **Test:** watch the plugin manifest schema. Free, ongoing.

**C2 — echook grows an unmeterable-to-meterable component. `[RESEARCHED — this is the one structural change that works]`**
Every paid comparable in this report charges for something the user cannot self-host: Langfuse's units, LangSmith's traces, Helicone's requests, Raycast's cloud sync, PagerDuty's seats, Pushover's delivery network. The single exception is **Wallaby/Quokka — proprietary, fully local, no server, sustained perpetual-licence business** `[PAGE]` — and its distinguishing property is that its *core is closed*, which echook's cannot become retroactively (the MIT grant on shipped versions is irrevocable; only *future* versions could be relicensed, and a fork of the last MIT commit would remain legal and free forever). **Test:** build one hosted thing (a team notification relay, a hosted fleet dashboard) and try to sell it. Weeks, not days.

**C3 — A named organisation asks for a quote. `[UNRESEARCHED — HYPOTHESIS]`**
I could not name five locked-out orgs. **This is the highest-value unknown in the report**, and I am marking it as a hypothesis rather than a lane precisely because an unsized lane at the same visual weight as a sized one reads as the most valuable thing on the page. It is not more valuable; it is merely unmeasured. **Test:** 20 emails. Days.

**C4 — Fleets of background agents become the default working mode. `[UNRESEARCHED — HYPOTHESIS]`**
If a developer routinely supervises 5–20 concurrent agents, out-of-band notification stops being a nicety and becomes a control surface, and the product category changes from "utility" to "console." I have no evidence on the timing and neither does anyone I could reach. **This is the steelman, below. Do not read it as a plan.**

**C5 — The maintainer, not the software, becomes the product. `[RESEARCHED — the only path with an existing, sourced price]`**
MIT gives away the code; it does not give away Chan Meng. Clutch's first-party data puts custom software projects at **$10,000–$49,999**, with an average Clutch project of **$132,480.29** over ~13 months `[PAGE]`. **One landed client is 50× to 250× the entire realistic product pool in this report.** The channel is already shipped (the README pitch + `mailto:`) and entirely unmeasured. **Test:** replace the `mailto:` with a tracked landing URL and read GitHub Insights → Traffic. One hour.

### What this report does NOT say

Read this section before reacting to the verdict.

1. **It does not say echook is a bad project.** "Not venture-scale" and "not good" are unrelated propositions, and the evidence here bears only on the first. echook does something Claude Code still does not do natively — a changelog sweep across 24 months and 200+ releases found **zero** native audio-notification features `[PAGE]` — for a population Anthropic's own documentation confirms is locked out of the alternative `[PAGE]`. That is a real gap, correctly identified, competently filled.
2. **It does not say the work was wasted.** Nine months produced a cross-platform, three-editor, 39-event system with an agent-operated configuration interface. C5 is the live monetisation path *because* the artefact is good, and the base-rates file finds the only quantified evidence in this space runs through exactly that mechanism ("I found your package, liked the code quality, and that's why I reached out" `[PAGE]`).
3. **It does not say the platform will kill it.** The evidence points the other way and it surprised me: `ccstatusline` grew **25×** in monthly installs *after* Anthropic shipped the native pre-calculated status-line fields, and `ccusage` grew **6×** after native `/usage` `[PRIMARY, npm downloads API]`. Extension points grow their ecosystems. The absorption risk here is low; the *revenue* is what is absent.
4. **It does not say "stop."** It says the current path returns $0 and a different, cheaper path (C5) has a sourced price 50–250× higher. That is a redirection, not a shutdown.
5. **It does not say the owner priced this wrong out of naivety.** There was no price to get wrong: no rail exists to charge on `[PAGE]` × 4.

### What would prove this wrong — ordered by cost to test

| # | Prove-wrong signal | Why it decides things | How to test, in days |
|---|---|---|---|
| **1** | **≥25 people pay $5 within 14 days** | A1 is ~100% of the realistic pool, and its ACV rests entirely on "the free MIT substitute means nobody pays." 25 payers falsifies that directly and cheaply. | Open a $5 one-time "supporter licence" on Polar or Lemon Squeezy (both bypass the missing marketplace rail entirely). Announce to the 78 stargazers, the plugin directories, and the README. **One afternoon. This is the cheapest decisive test in the report.** |
| **2** | **≥2 of 20 named orgs reply asking for a quote** | A2 is $0 only because nobody has been asked. Two quote requests move it off zero and simultaneously close the report's biggest gap. | Build the list (AWS Bedrock + Google Cloud customer case studies name them publicly), send 20 emails with a concrete offer: "$2,000 site licence + 4 hours of integration for your Bedrock/gateway deployment." **~3 days.** |
| **3** | **≥1 inbound consulting lead attributable to the repo in 60 days** | Validates C5, the only path with a sourced price 50–250× the product pool. | Swap the `mailto:` for a tracked landing page; read GitHub Insights → Traffic weekly. **One hour to instrument, 60 days to read.** |
| **4** | **A payment rail appears in the plugin manifest schema** | Removes Constraint 1 and forces a full re-run. | Diff `plugins-reference` for a price/entitlement field. **Free, ongoing.** |
| **5** | **Any Claude Code / Cursor / Codex add-on publicly discloses >$1,000 MRR** | The base-rates file found precisely zero. One credible instance breaks the strongest absence claim in this analysis. | Set alerts on Indie Hackers + X for "MCP server MRR", "Claude Code plugin revenue". **Free, ongoing.** |

**Which combination overturns rather than dents.** Any one of these alone dents the verdict. **Items 1 and 2 landing together overturn it** — paying individuals *and* a named organisational buyer means the willingness-to-pay assumption was wrong at both tiers simultaneously, and the sizing must be rebuilt from scratch. **Items 4 and 5 landing together overturn it differently and more durably**: a rail plus a proven revenue instance means the ecosystem changed underneath the base rates, and every "absence is the finding" conclusion in this report expires on that date.

### The steelman I could not refute

*Stated at full strength, not as a concession:*

**This entire report measures a world that is being replaced while it is being measured.** Claude Code went from general availability in May 2025 to **$1 billion in run-rate revenue in six months** `[PAGE]`. `ccstatusline` went from 11,292 monthly installs in December 2025 to **407,682 in July 2026** `[PRIMARY]`. Anthropic shipped a mobile push tool in April 2026 — after this project started — which is itself an admission that *the agent finishing while you are not watching is now the central UX problem of agentic coding*. If, within two years, the default working mode is a developer supervising five to twenty concurrent background agents, then "a sound when the agent finishes" stops being a preference and becomes the control surface of the job — and a category with no buyers today acquires them in a step change, exactly as observability did after LLM applications went to production. Every count in this document — 78 stars, 300 reachable people, zero named orgs, zero disclosed ecosystem revenue — is a measurement of the pre-fleet world, and is **backward-looking by construction**. Base rates are the correct tool for a stable category and the wrong one for a category that did not exist thirty months ago.

**I cannot refute this, and I am not going to pretend to.** What I can say is that it is **unfalsifiable in the present tense**: no evidence available on 2026-08-04 can confirm or deny it, which is exactly why every prove-wrong item above carries a date and a duration rather than an argument. **So date it rather than reject it:**

> **Re-run this analysis on 2027-02-04 (six months).** The steelman is *confirmed* if by that date any of: a payment rail exists in the Claude Code plugin manifest; any ecosystem add-on discloses >$1,000 MRR; or echook's own reachable population has grown past ~1,000 stargazers. It is *disconfirmed* if the counts have moved and the money still has not — which is precisely what `ccstatusline`'s 25× growth against a Buy Me a Coffee button demonstrates has already happened once, to the closest comparable in existence.

That last clause is the strongest thing I can say against the steelman without overreaching: **in this ecosystem, the fleet future has already partially arrived, adoption has already gone up 25×, and revenue in the closest comparable has not followed.** Growth in this category has been demonstrated to be orthogonal to revenue. The steelman requires that relationship to change, not merely for the growth to continue.

### Open gaps

| Gap | Why it matters | Value |
|---|---|---|
| **Zero named organisational buyers verified** | A2 is $0 by *absence of enumeration*, not by evidence of refusal. It is the only archetype whose realistic pool could plausibly be non-zero. | **HIGHEST — and closeable by 20 emails, not by more research** |
| X/Twitter build-in-public disclosures unreachable (auth wall) | The most likely home of a "$X MRR from an MCP server" post that would break the strongest absence claim in the report | High |
| Reddit fully blocked (WebFetch refuses; curl and proxy both 403) | Contained the SkillHQ / Agent37 seller threads with possible early sales data | Medium |
| echook's actual install base is **unknowable** — no telemetry (by design), no PyPI, no download counter | The owner cannot count his own users, so A1's reachable count of ~300 is a floor built from stars, not a measurement of usage | Medium — and note the *design* choice creating it is a correct one |
| Wallaby/Quokka actual price (pages render prices client-side, five fetch routes returned `"Calculating"`) | It is the single best counter-example to "you need a hosted component to charge" — its *price point* would calibrate C2 | Medium |
| WebSearch budget exhausted session-wide (200/200) before this analysis began | Constrained discovery throughout; primary APIs and direct fetches were used instead, which is why so much here is `[PRIMARY]` | Disclosed, not fatal |

### If the answer is "nobody, yet" — reported as a result

**It is, and here is the anatomy.**

**The adjacent pools that DO exist and are real:**
- **Advertising to the ecosystem's builders.** claudemarketplaces.com serves 380,000+ monthly visitors and its ad inventory is **sold out**, with CodeRabbit, Airtable, 1inch, IdeaBrowser and AppSignal running ads `[PAGE]`. Money moves in this ecosystem — toward whoever aggregates attention, not toward whoever writes the plugins.
- **Metered hosted services delivered through the protocol.** Ref (ref.tools) charges **$9/month for 1,000 credits** with "hundreds of subscribers" `[PAGE]` — and monetises a hosted search index, not a distributable artefact.
- **Consulting.** Clutch's $10,000–$49,999 project band `[PAGE]`. Fifty to two hundred and fifty times the entire realistic product pool in this report.

**Why the direct pool is empty, with each reason classified:**

| Reason | Time-sensitive or structural? |
|---|---|
| **No payment rail** in any of the three marketplaces `[PAGE]` × 4 | **Time-sensitive.** A statement about this quarter. Anthropic could ship one; VS Code's equivalent request has merely been open since 2020-02-14 `[PAGE]`. |
| **No precedent** — zero disclosed revenue from any Claude Code/Cursor/Codex add-on; three commerce layers built for it show 0 sales on their own storefronts `[PAGE]` | **Time-sensitive.** Absences of precedent end. |
| **No metered unit** — no server, no seats, no data, by design | **Semi-structural.** Changeable only by building a different product (C2). |
| **A free MIT substitute that is the same software, already public** | **STRUCTURAL. This is a law, not a market condition.** It cannot be revoked for shipped versions, it survives every future business model, and it caps every price in this report at whatever a buyer volunteers. |

**The variable that has changed since the comparable attempts — and the honest reading of it.** Two things genuinely changed: the market got enormous ($0 → $1B run-rate in six months `[PAGE]`), and the exclusion became first-party-documented and precise (the feature-availability matrix, which names exactly who cannot get native push while confirming hooks work everywhere `[PAGE]`). Both are real. **But the variable that would have to change for a *business* — a payment rail, or a component the buyer cannot self-host — has not changed at all.** And the natural experiment that tests this is already complete: `ccstatusline` rode the same 25× growth, in the same niche, on the same platform, to 12,205 stars and 407,682 monthly installs, and monetises with a Buy Me a Coffee link `[PRIMARY]`.

**When the closest comparable is 156× your size and its business model is a tip jar, the verdict is written.**
