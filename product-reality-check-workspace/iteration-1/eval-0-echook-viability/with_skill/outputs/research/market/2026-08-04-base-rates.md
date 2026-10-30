# echook — Base Rates: What Happened to Everyone Who Tried This

**Date:** 2026-08-04
**Companion to:** `2026-08-04-who-pays-and-sizing.md` (Part A + verdict)
**Subject:** [github.com/ChanMeng666/echook](https://github.com/ChanMeng666/echook) — MIT, Python, solo maintainer, 9 months, zero revenue, 78 stars (measured), no telemetry

**Sourcing:** every external claim carries a URL fetched or an API queried this session, graded `[PAGE]` (fetched, read the number), `[PRIMARY]` (I queried a live API and computed the number myself), `[SNIPPET]` (search-result snippet only), `[UNVERIFIED]`. The session-wide WebSearch budget was exhausted (200/200) before this research began, so a large share of what follows is `[PRIMARY]` measurement built from the GitHub, npm and Open Collective APIs rather than secondary reporting. Where that cost me something, it is disclosed.

---

## EXECUTIVE SUMMARY — VERDICT FIRST

> **The base rates are more decisive than the arithmetic, and all six point the same way: the direct-revenue path for a 78-star MIT dev utility returns $0, the platform will probably not kill it, and the only path with a sourced price 50–250× larger than the product pool is the maintainer's own time.**

The six answers, compressed:

| # | Question | Answer | Confidence |
|---|---|---|---|
| **1** | Donation ceiling at ~79 stars | **$0 — the median, literally, by four independent measurements.** Non-trivial donation income does not reliably begin below ~25,000–50,000 stars, and fails about half the time even there | **High** — 2 primary datasets + a peer-reviewed study |
| **2** | Any Claude Code / Cursor / Codex add-on with disclosed revenue? | **No. And there is no payment rail to earn it on** — established by exhaustive grep of three first-party manifest schemas | **High** — schema-level, not commentary |
| **3** | What separates VS Code extensions that CAN charge | **A component the buyer cannot self-host, plus team/seat procurement.** echook has neither, and is additionally MIT | **High** — 8 extensions mapped against 5 characteristics |
| **4** | Platform-absorption base rate | **~40% die / ~45% survive / ~15% zombie — a coin flip, not a death sentence.** And the sorting variable is *extension-point vs. competing-product*, not free-vs-paid | **High** — 16 cases, 3 of them in-ecosystem with npm download curves |
| **5** | Acquihire path | **Real, but the observed entry price is 82,000 stars / 7M monthly downloads. Zero precedent for any Claude Code plugin maintainer.** A lottery ticket, 3 orders of magnitude out | **High** on the threshold, **Medium** on completeness |
| **6** | Portfolio / lead-gen path | **The only path with a sourced price 50–250× the product pool — and the literature is narrower than the folklore: contribution *volume* pays nothing; earned *rank* paid up to 18%** | **Medium** — one strong study, one on-point anecdote, no conversion data anywhere |

**The variable that has changed since the comparable attempts:** the market got enormous ($0 → $1B run-rate in six months) and the exclusion of non-subscription deployments from native push became precisely documented. **The variable that has not changed: there is still no payment rail and still no meterable unit.** The closest comparable in existence, `ccstatusline`, rode a 25× growth wave in exactly this niche to 12,205 stars and 407,682 monthly installs — and monetises with a Buy Me a Coffee link.

---

## Q1 — The donation ceiling

### Primary measurement A: 368 open-source collectives, stars vs. money actually received

I pulled Open Collective's public GraphQL API for collectives tagged `open source`, extracted the 435 with a parseable GitHub repo URL, and joined each to its GitHub star count. 368 matched. `[PRIMARY]` — `api.opencollective.com/graphql/v2` + `api.github.com/repos/{owner}/{repo}`, 2026-08-04.

| Star band | n | Received $0 | Received >$0 | Best result | **Median** |
|---|---|---|---|---|---|
| 0–49 | 287 | 284 | 3 | $598.00 | **$0.00** |
| **50–99** (echook's band) | **15** | **14** | **1** | **$1,530.00** | **$0.00** |
| 100–499 | 36 | 31 | 5 | $1,111.00 | **$0.00** |
| 500–999 | 13 | 13 | 0 | $0.00 | **$0.00** |
| 1,000–9,999 | 13 | 11 | 2 | $600.00 | **$0.00** |
| 10,000+ | 4 | 3 | 1 | $112.00 | **$0.00** |

**356 of 368 (96.7%) received exactly $0.**

**Stated caveat, because it matters:** this cohort is *new* collectives (created 2026-04-16 → 2026-08-04), so the accrual window is weeks-to-months, not a year. It measures "what a freshly-opened donation page brings in during its first months" — which is precisely the decision a 78-star project faces — but it is **not** a steady-state annual figure and must not be read as one.

### Primary measurement B: does anyone at ~79 stars even have a sponsor?

Sampled 100 GitHub repos in each of three star bands (pushed since 2026-01-01), deduped to owners, queried `hasSponsorsListing` and `sponsors{totalCount}` via GitHub GraphQL. `[PRIMARY]`, 2026-08-04.

| Tier | Owners | Has a Sponsors listing at all | ≥1 **public** sponsor | Median public sponsors | Max |
|---|---|---|---|---|---|
| **~70–90★** | 94 | 14 (15%) | 7 (**7%**) | **0** | 29 |
| 1,000–1,500★ | 96 | 19 (20%) | 12 (12%) | **0** | 27 |
| 10,000–30,000★ | 93 | 16 (17%) | 13 (14%) | **0** | 662 |

**The median owner has zero public sponsors at every tier — including above 10,000 stars.** Caveat: GitHub's public `sponsors.totalCount` excludes private sponsors, so these are lower bounds; and it is owner-level, not repo-level.

### Primary measurement C: echook's own owner, directly

`[PRIMARY, GitHub GraphQL, 2026-08-04]` — `ChanMeng666`: **222 followers · `hasSponsorsListing: true` · `sponsors.totalCount: 0`.** Plus `buy_me_a_coffee: chanmeng66u` live in `.github/FUNDING.yml`.

**The donation experiment is not hypothetical here. It has been running for nine months, in front of 222 followers, with both rails open, and it has returned zero.**

### The published literature

**Overney, Meinicke, Kästner & Vasilescu, "How to Not Get Rich: An Empirical Study of Donations in Open Source," ICSE 2020.** [cmustrudel.github.io/papers/overney20donations.pdf](https://cmustrudel.github.io/papers/overney20donations.pdf) `[PAGE]`, quoted verbatim:

- Prevalence: "**25,885 out of 77,934,441** repositories of our GitHub corpus (**0.04%**)" ask for donations; in npm, "**1,145 out of 537,640** … (**0.2%**)".
- Amounts, for the 817 npm projects using Patreon/OpenCollective over **nine months**: "**min 0 USD, median 55 USD, mean 6108 USD, max 589,382 USD**".
- "only 575 (**70%**) received any funding at all, and only **45 repositories (5%) received more than 1000 USD/month** — the level at which donations could support a single developer at the 2018 US income poverty guidelines."
- Whole-GitHub corpus: "**58% of repositories received donations; only 10% received 1000 USD/month or more.**"
- Stars dominate: "only popularity (*number of stars*, **74%**; and *number of downloads*, 12%) correlates with the amounts received"; and for whether a project asks at all, "num stars, **81% of the variance explained**".

**A median of $55 over nine months — for a project that has already gone to the trouble of opening a donation page.**

**2024 Tidelift Maintainer Impact Report, p.2** `[PAGE]` [sonarsource.com/the-2024-tidelift-maintainer-impact-report.pdf](https://www.sonarsource.com/the-2024-tidelift-maintainer-impact-report.pdf): "**Sixty percent of maintainers report they are unpaid hobbyists, and only 12% of maintainers consider themselves professionals who earn most or all of their income from their maintenance work.**"

**Platform totals** (reported without dividing, because neither page discloses a denominator of sponsored maintainers): GitHub Sponsors "**$40M+** Given back to our maintainers", "4.2K+ Organizations sponsoring" [github.com/sponsors](https://github.com/sponsors) `[PAGE]`. Open Collective "**$40 Million**" managed across "**10,000+** Collectives" [opencollective.com](https://opencollective.com/) `[PAGE]`.

### Named public ledgers at the 10,000+ star tier — where donations are *supposed* to work

Open Collective publishes every collective's estimated annual budget at `opencollective.com/<slug>.json` (cents). The cents interpretation was verified byte-exactly against three rendered pages: `mochajs` `2441487` ↔ "**$24,414.87 USD**"; `husky` `41000` ↔ "**$410.00 USD**"; `gulpjs` `198860` ↔ "**$1,988.60 USD**" `[PAGE]` ×3. Stars from the GitHub API the same day. `[PRIMARY]`

| Project | ★ | Est. annual budget | | Project | ★ | Est. annual budget |
|---|---|---|---|---|---|---|
| babel | 43,973 | **$276,238** | | jest | 45,460 | **$9,682** |
| socket.io | 63,188 | $196,550 | | parcel | 44,023 | $8,600 |
| vue | 54,105 | $195,446 | | typeorm | 36,611 | $5,219 |
| eslint | 27,437 | $166,059 | | **gulp** | **32,957** | **$1,989** |
| webpack | 65,883 | $157,387 | | express | 69,306 | $1,720 |
| axios | 109,169 | $145,498 | | lodash | 61,284 | $1,636 |
| vite | 82,182 | $111,513 | | **husky** | **35,249** | **$410** |
| prettier | 52,173 | $71,758 | | ramda | 24,060 | $364 |
| core-js | 25,512 | $25,068 | | hoppscotch | 79,961 | $120 |
| mocha | 22,905 | $24,415 | | d3 · tailwindcss · koa · nestjs · ava · bruno · standard · semantic-release | 20k–113k | **$0.00** |

**19 of these 36 collectives — for projects with 11,000 to 113,000 stars — run on under $10,000/year. 16 are under $2,000/year.**

The sharpest fact available: **husky has 35,249 stars, describes itself on its own collective page as "used by 1.2M+ projects on GitHub," has 96 financial contributors and $31,749.54 lifetime — and its estimated annual budget is $410.00.** [opencollective.com/husky](https://opencollective.com/husky) `[PAGE]`

**Required caveat:** a $0 collective does not prove a project earns nothing (Tailwind Labs is a company; express sits under the OpenJS Foundation; NestJS solicits on its own site). What the table *does* prove is that **a public donation ledger is not a reliable income stream even at enormous star counts** — the same instrument that gives babel $276k gives gulp $1,989.

### The two famous "open source pays" cases are both *not donation income*

- **Caleb Porzio** (Livewire, Alpine.js) `[PAGE]` [calebporzio.com/…-100000yr-on-github-sponsors…](https://calebporzio.com/i-just-hit-dollar-100000yr-on-github-sponsors-heres-how-i-did-it): "$112,680/yr" annual revenue, "~$25k" in Sponsors cash at time of writing, "535 people" at "$14/mo". But the mechanism was **paywalled product** — sponsorware raised revenue "by $11k in a matter of days," and sponsor-gated private screencasts "raised his annual revenue by ~$80k in 90 days." **The bulk is paid video sold through Sponsors as a billing rail, not donations for a library.**
- **Filippo Valsorda** (Go cryptography) `[PAGE]` [words.filippo.io/full-time-maintainer](https://words.filippo.io/full-time-maintainer/): "I now have six amazing clients"; "All tiers are in the five-figures range (USD, yearly)"; income "equivalent to my Google total compensation package." **B2B retainer contracting with named corporate clients**, explicitly not crowdfunding. No total is disclosed and I will not compute one.

### The deliverable answers

**"What is the median/expected annual donation income for a dev utility at ~79 stars?"**

**$0.** Not "close to zero" — literally zero, as the median, by four independent measurements: (1) 14 of 15 collectives in the 50–99★ band received $0 `[PRIMARY]`; (2) 85% of 70–90★ repo owners have no Sponsors listing and 93% have zero public sponsors `[PRIMARY]`; (3) the median npm project that has *already opened* a donation page received **$55 over nine months** `[PAGE]`; (4) only 0.04% of GitHub repositories ask at all `[PAGE]`. Including the tail: total receipts across the whole 50–99★ band were $1,530, essentially all captured by one outlier.

**"What star count must a project reach before donations are non-trivial income?"**

Using the paper's own threshold — **$1,000/month, "the level at which donations could support a single developer"** — only **5% of npm projects with a donation page** and **10% of the GitHub corpus** clear it `[PAGE]`. The ledger table locates it empirically: **$12k/yr is not reliably reached until roughly 25,000–50,000 stars, and fails about half the time even there** (jest 45,460★ → $9,682; parcel 44,023★ → $8,600; husky 35,249★ → **$410**). A living wage effectively requires being one of a dozen load-bearing ecosystem primitives at 25k–110k stars *plus* a corporate sponsor programme.

> **What this implies for echook:** the donation path is not "underperforming" — it is returning its median result, and the median result at 78 stars is $0. Nothing about echook's quality changes this; the variable that moves donation income is stars (81% of the variance in whether a project even asks), and echook is roughly 300–600× below the threshold where the instrument starts working at all.

---

## Q2 — Has any Claude Code / Cursor / Codex add-on made disclosed money?

### The decisive sub-question: does a payment rail even exist? **No. On all three platforms.**

Established at the schema level, which is stronger than any press statement:

- **Claude Code.** A marketplace is a git repo containing `.claude-plugin/marketplace.json`; install is a `git clone` of a pinned SHA into `~/.claude/plugins/cache`. An exhaustive grep of the full marketplace doc (73.8 KB) for `price|paid|payment|billing|monetiz|purchase|licens|commercial|cost|subscri` returns **exactly two hits: the `license` SPDX field and `"license": "MIT"` in an example.** The full plugin manifest schema (`name`, `displayName`, `version`, `description`, `author`, `homepage`, `repository`, `license`, `keywords`, `skills`, `commands`, `agents`, `hooks`, `mcpServers`, `outputStyles`, `lspServers`, `experimental`, `dependencies`) has **no price, payment, entitlement or licence-key field.** [plugin-marketplaces](https://code.claude.com/docs/en/plugin-marketplaces) + [plugins-reference](https://code.claude.com/docs/en/plugins-reference) `[PAGE, exhaustive grep]`. The public catalogue at [claude.com/plugins](https://claude.com/plugins) shows no price, cost, subscription or purchase text anywhere `[PAGE]`.
- **Cursor.** "Cursor uses the Open VSX extension registry for third-party extensions, with Cursor's marketplace proxy applying automated malware and supply-chain analysis before extensions are offered for install." [cursor.com/help/customization/extensions](https://cursor.com/help/customization/extensions) `[PAGE]`
- **Codex CLI.** A `/plugins` browser: "groups plugins by marketplace… switch sources, open a plugin to inspect details, install or uninstall marketplace entries." No pricing mechanism. [learn.chatgpt.com/docs/plugins](https://learn.chatgpt.com/docs/plugins) `[PAGE]`. OpenAI *does* have a Checkout API, but "**current approval is limited to plugins for physical goods purchases**" and it is a ChatGPT surface — [developers.openai.com/plugins/build/monetization](https://developers.openai.com/plugins/build/monetization) `[PAGE]`. **Not a rail for selling a Codex CLI plugin.**
- **VS Code, the mature analogue.** The `pricing` property "Allowed values are: `Free` and `Trial` (case-sensitive)." **There is no `Paid` value.** The only money feature is a `sponsor` link-out. [publishing-extension.md](https://github.com/microsoft/vscode-docs/blob/main/api/working-with-extensions/publishing-extension.md) `[PAGE]`. [microsoft/vscode#90648 "Add support for premium extensions"](https://github.com/microsoft/vscode/issues/90648) opened **2020-02-14**, **still open** `[PAGE]`; [#111800 "Find a way to allow us to monetize the extensions"](https://github.com/microsoft/vscode/issues/111800) opened 2020-12-03, **closed 2020-12-06** `[PAGE]`.

### Corroborating measurement: nobody is even *trying*

GitHub code search across all public repos `[PRIMARY, 2026-08-04]`: **15,728** `.claude-plugin/marketplace.json` files exist. Of those, `"price"` appears in 174 (~1.1%) — and the top hits are `anthropics/financial-services`, `quant-sentiment-ai/claude-equity-research`, `moonpay/skills`, i.e. **finance-domain plugins that mention prices as subject matter.** `gumroad`: **3**. `lemonsqueezy`: **2**. `polar.sh`: **1**.

### The only genuinely disclosed add-on revenue found

**Ref (ref.tools), by Matt Dailey.** [pulsemcp.com/posts/pricing-the-unknown-a-paid-mcp-server](https://www.pulsemcp.com/posts/pricing-the-unknown-a-paid-mcp-server) (2025-09-10) `[PAGE]`, verbatim: "**$9/month for 1,000 credits ($0.009 per search)**" with "200 free credits that never expire"; and "Since launching with this pricing and packaging **3 months ago, Ref has thousands of weekly users and hundreds of subscribers**." **No revenue figure is stated** — "hundreds × $9" is arithmetic, not disclosure, and I am not fusing it into one. Dailey names the structural problem himself: "nearly everything else is free" in the MCP ecosystem, so you are "competing against free alternatives."

**Ref is not a plugin sale.** It is a **hosted search service with a metered backend** delivered through MCP. The customer pays for server-side compute and an index — the thing that *can* be metered. Unavailable to anything that runs locally.

### Where the money in this ecosystem actually is: advertising

`claudemarketplaces.com` indexes "**23,500+ skills, 2,600+ marketplaces, 12,700+ MCP servers**" with "**380,000+ monthly visitors**." Asked whether anything costs money: "**Yes. Completely free and open. Browse and install anything at no cost.**" Its own revenue is ad slots — "**Sold out** — book a call to claim a future slot. Advertise to Claude Code builders," with "CodeRabbit, Airtable, 1inch, IdeaBrowser, and AppSignal already run ads." [claudemarketplaces.com](https://claudemarketplaces.com/) `[PAGE]`

**The directory selling ads *to* plugin builders is sold out. The plugins themselves are free.**

### The commerce layers built to fix this — all showing zero sales

- **SkillHQ** (`skillhq.dev`) `[PAGE ×3]` — the most developed. "Earn **80% (Starter) or 85% (Pro)**. No listing fees. Anti-piracy built in." Concrete fee mechanics (€10 sale → €8.50 seller, €1.10 platform, €0.40 Stripe). Homepage: "**439+ Curated Skills**," prices €2–$50. **Every featured listing displays "No ratings · 0 sales."** No seller count, sales total, or payout figure is published anywhere on the site.
- **Agent37** `[PAGE]` [agent37.com/blog/monetize-claude-code-skills](https://www.agent37.com/blog/monetize-claude-code-skills) — concedes the point in its own marketing: the official "Plugin marketplace: Add repo as plugin source | Open distribution, free products | **No (no payments)**," and "the default distribution path is still painfully developer-centric: share a repo or a zip file…customer pays you… *somehow?*" **Names no creator and no earnings.**
- **skills4agents.com, skillmarketplace.ai, mcpmarket.com/tools/skills, MCPize (85% rev share)** — all exist, all early, **none discloses revenue** `[SNIPPET]`.

### Search paths exhausted, and what each returned

| Path | Result |
|---|---|
| Claude Code plugin + marketplace docs, full fetch + exhaustive grep | **No payment rail. No price field.** Decisive. |
| claude.com/plugins official catalogue | No pricing anywhere |
| Cursor extension docs | Open VSX; no payment mechanism |
| VS Code Marketplace publishing docs | `Free`/`Trial` label + external `sponsor` link only |
| Codex CLI plugin docs · OpenAI monetisation docs | `/plugins` browser, no payment · Checkout is ChatGPT + physical goods |
| Official MCP registry (`modelcontextprotocol/registry`, 7,103★) | Community registry; no commerce language |
| Smithery docs | **No monetisation or revenue share for server authors** anywhere in docs (pricing page 429'd) |
| Glama pricing | $9/$26/$80 **AI credits — Glama charging users.** "Free for open-source." **No author revenue share** |
| PulseMCP | Free directory; surfaced the one real case (Ref) |
| Indie Hackers (site: search + direct post fetch) | MCP posts exist (Crawlora, GoldBean/x402, SafeWeave). **None discloses add-on revenue.** SafeWeave's own "honest report": 120+ Discord devs, "Conversion from free to paid is lower than we expected. High install numbers, not enough upgrades" — **and no revenue figure at all** `[PAGE]` |
| Polar.sh | **Pivoted** to AI/usage billing infrastructure. **No aggregate creator revenue, GMV or payout totals disclosed** |
| Gumroad / Lemon Squeezy sellers in niche | No disclosed sales; 3 + 2 references across 15,728 marketplaces |
| mcp.so | **403 Forbidden — could not check.** Gap |
| X/Twitter "$X MRR" build-in-public | ⚠️ **NOT REACHABLE** — auth wall; no engine surfaced any. **Biggest gap** |
| Reddit (SkillHQ, Agent37 threads) | ⚠️ **BLOCKED** — WebFetch refuses; curl and r.jina.ai both 403 |
| MicroConf / SaaS directories | ❌ Not reached before search access collapsed |

### A methodological warning worth carrying forward

A large share of what surfaces on "MCP monetization revenue" is AI-generated SEO content citing itself in a circle. **Two sites give mutually contradictory revenue figures for the same company**: 21st.dev is described as having "hit $10,000 in monthly recurring revenue in 6 weeks" `[SNIPPET, arte.itlibra.com]` and as "generating over **£400** in monthly recurring revenue" `[SNIPPET, ritza.co]`. 21st is also **not a solo dev** — it carries PitchBook and Dealroom company profiles `[SNIPPET]`. **Treat as worthless evidence.** Same for "How a Twitter MCP Server Took a Solo Dev From $12 to $3.4K MRR" (casedistillery.com `[SNIPPET]`), SkillHQ's own unsourced "creators report $600–$20,000/month" marketing claim `[PAGE, but the claim is UNVERIFIED]`, and settlegrid.ai's "less than 5% of MCP servers earn a single dollar" (fetched and specifically probed for methodology: **there is none** — no survey method, no collection period, no definition of "monetized") `[PAGE, methodology UNVERIFIED]`.

> **What this implies for echook:** there is nothing to price *against*, and nothing to price *on*. The absence is not a gap in the search — it is a property of three platforms whose install mechanism is `git clone`. Any plan that begins "charge for the plugin" has to first build a rail that three trillion-dollar-adjacent platforms have chosen not to build, one of them for six and a half years and counting.

---

## Q3 — Paid VS Code extensions: what separates the ones that CAN charge

### Who actually charges (all prices fetched this session)

| Extension | Price | Source |
|---|---|---|
| **GitHub Copilot** | Free $0 · **Pro $10/mo** · Pro+ $39/mo · Max $100/mo | [github.com/features/copilot/plans](https://github.com/features/copilot/plans) `[PAGE]` |
| **Tabnine** | **Code Assistant $39/user/mo**, **Agentic Platform $59/user/mo**, both annual. Token charges at provider rates **+5% handling fee** | [tabnine.com/pricing](https://www.tabnine.com/pricing/) `[PAGE]` |
| **GitLens (GitKraken)** | **Pro list $10/seat/mo** paid annually; Community free | [gitkraken.com/gitlens/pricing](https://www.gitkraken.com/gitlens/pricing) `[PAGE]` |
| **Thunder Client** | Free · **Starter $3** · **Business $7** · **Enterprise $16** per user/mo annual. "All payments are processed by Stripe" | [thunderclient.com/pricing](https://www.thunderclient.com/pricing) `[PAGE]` |
| **SonarQube for IDE** | **The extension is free.** SonarQube Cloud Team "**starts at $34 monthly**"; Server priced per instance per year by lines of code | [sonarsource.com/plans-and-pricing](https://www.sonarsource.com/plans-and-pricing/) `[PAGE]` |
| **Wallaby.js / Quokka Pro** | **Price `[UNVERIFIED]`.** Structure verified: "Perpetual license + 1 year of updates," personal named-user vs company seat, volume discounts 5% at 10–19 / 10% at 20+ | [wallabyjs.com/purchase](https://wallabyjs.com/purchase/) `[PAGE]` for structure. Five fetch routes returned the literal string `"Calculating"` — do not let a number in without a browser |
| **Kite** | **Dead.** Source dumped as `kiteco/kiteco-public`, BSD-3-Clause, 769★, created 2022-01-01, last push 2022-12-01 | [github.com/kiteco/kiteco-public](https://github.com/kiteco/kiteco-public) `[PAGE]` |
| **CodeStream** | **Dead.** Every `TeamCodeStream` repo is `archived=true`; `codestream-server` last push 2024-08-01 | GitHub API `[PAGE]` |
| **Draw.io Integration** | **Free.** GPL-3.0, 9,476★, no FUNDING.yml | GitHub API `[PAGE]` |

### The characteristics, each backed by a specific case

**(a) A hosted component the buyer cannot self-host — the strongest single predictor.**
SonarQube proves it *by contrast within one product*: the IDE extension is free, and every priced SKU on the page is a server or cloud instance `[PAGE]`. Copilot's entire ladder is denominated in hosted inference — the tiers differ by AI credits ($15/mo at Pro → $200 at Max) `[PAGE]`. Tabnine passes through token consumption "at actual provider rates plus 5% handling fee" `[PAGE]`.

**(b) Team/enterprise seat licensing and procurement.**
Thunder Client's ladder is *procurement features, not code features*: Free → Starter (credit card, ≤10 seats) → Business (adds "Credit Card, PO, Invoice") → Enterprise $16 (adds SSO). **The thing sold at the top is purchase-order acceptance** `[PAGE]`. GitLens's free tier is scoped by *repo visibility* — Pro unlocks Commit Graph, Visual File History and Worktrees **on Private Repos**: free for OSS, paid at work `[PAGE]`.

**(c) A proprietary core, so no free substitute exists.** Real, but weak alone — and expensive. Wallaby/Quokka is the purest instance (closed source, fully local, no server) `[PAGE]`, and it must maintain a **complete licence-enforcement apparatus** — store, named-user vs seat licences, renewal discounts — entirely itself, because the Marketplace supplies nothing.

**(d) Proprietary data or a model the buyer can't reproduce. Necessary but demonstrably not sufficient — this is Kite's headstone.**
Kite had exactly this: a GitHub crawl of "about 20 TB" plus a statistical type-induction pipeline ("there is a 51.9% probability that `numpy.matrix.argmin` returns a `numpy.matrix`") `[PAGE]`. **It still died and dumped the whole thing as BSD-3-Clause.** Unreproducible data bought a moat and no business.

**(e) Support/SLA.** Present only at the top of ladders (SonarQube Enterprise "enterprise SLA"; GitLens Advanced "priority support") `[PAGE]` ×2. **No case found where SLA alone was the product.**

### The map

| Extension | (a) hosted | (b) seats | (c) proprietary core | (d) proprietary data | (e) SLA | Charges? |
|---|---|---|---|---|---|---|
| Copilot | ✅ | ✅ | ✅ | ✅ | ✅ | yes |
| Tabnine | ✅ | ✅ | ✅ | ✅ | ✅ | yes |
| GitLens | ✅ | ✅ | ✅ | — | ✅ | yes |
| SonarQube for IDE | ✅ | ✅ | ✅ | — | ✅ | **extension free**, server paid |
| Thunder Client | ✅ | ✅ | ✅ | — | — | yes |
| Wallaby/Quokka | ❌ | ✅ | ✅ | — | — | yes |
| Kite | ✅ | ❌ | ✅ | ✅ | ❌ | **tried, died** |
| Draw.io Integration | ❌ | ❌ | ❌ (GPL) | ❌ | ❌ | no |
| **echook** | **❌** | **❌** | **❌ (MIT)** | **❌ (zero telemetry)** | **❌** | **—** |

**Exactly one extension in the set charges without a hosted component (Wallaby) — and it is proprietary *and* sells by company seat. Zero charge on a proprietary core alone. Every paid case has (b) seats, or is Kite, which is dead.**

### Counter-example hunt: an MIT/OSS, fully-local extension making meaningful money

**I could not find one.** Checked via GitHub API (repo metadata + `.github/FUNDING.yml`) `[PAGE]`: VSCodeVim/Vim (MIT, 15,185★) → a lone `github: [J-Fields]` sponsor link; hediet/vscode-drawio (GPL-3.0, 9,476★) → **no FUNDING.yml at all**; usernamehw/vscode-error-lens (MIT, 833★) → none; Gruntfuggly/todo-tree (1,808★) → none; formulahendry/vscode-code-runner (MIT, 2,430★) → none. `opencollective.com/vscodevim` returns **HTTP 404** — no collective exists `[PAGE]`.

**The ceiling for an MIT fully-local extension appears to be a sponsor link.** With no search budget I could not sweep the long tail, so treat this as a strong negative rather than a proven one — but across the five highest-profile OSS local extensions, the count of paid tiers is **zero**.

> **What this implies for echook:** echook has **none** of the five characteristics — MIT (no c), fully local (no a), zero telemetry by design (no d), no seats or admin surface (no b), no support obligation (no e). It sits in the same row as Draw.io Integration, whose observed monetisation is nothing. To acquire one of them, it would have to become a materially different product; and (c) is the one it can never fully acquire retroactively, because the MIT grant on shipped versions is irrevocable and a fork of the last MIT commit stays legal and free forever.

---

## Q4 — The platform-absorption base rate

### The in-ecosystem cases — where I spent the most effort, and where the surprise is

First the platform timeline. Every native feature date below is joined to its **npm publish timestamp**, so these are real ship dates. [anthropics/claude-code CHANGELOG.md](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md) + [registry.npmjs.org/@anthropic-ai/claude-code](https://registry.npmjs.org/@anthropic-ai/claude-code) `[PAGE]`

| Native feature | Version | Ship date |
|---|---|---|
| "Customizable status line… with /statusline" | 1.0.71 | **2025-08-07** |
| `/usage` command to see plan limits | 2.0.0 | **2025-09-29** |
| `context_window.used_percentage` / `remaining_percentage` in status-line input | 2.1.6 | **2026-01-13** |
| "Expand Remote Control to more users" | 2.1.58 | **2026-02-25** |
| `rate_limits` field (5-hour and 7-day, `used_percentage`, `resets_at`) | 2.1.80 | **2026-03-19** |
| "Push notification tool — Claude can send mobile push notifications when Remote Control and 'Push when Claude decides' are enabled" | 2.1.110 | **2026-04-15** |

**Correction to the brief's premise, and it matters.** A regex sweep of the entire changelog (v0.2.6, 2025-02-24 → v2.1.221) for `sound|audio|bell|chime|speech|TTS` returns **14 hits, none of them an audio notification feature** — all are voice *input* (dictation, mic, SoX, ALSA) or terminal-bell bug fixes `[PAGE]`. **Claude Code has never shipped native audio notifications.** echook's status-line track faces a native equivalent; its audio track does not.

**Finding 1 — the extension-point cases GREW after the native feature. Enormously.**

npm monthly downloads `[PRIMARY, api.npmjs.org]`:

```
ccusage        (native /usage shipped 2025-09-29)
  2025-08 178,069 | 2025-09 121,948 | 2025-10  75,215  <- dip
  2025-11  73,589 | 2025-12 106,488 | 2026-01 143,602
  2026-03 200,681 | 2026-05 329,575 | 2026-07 460,893  <- 6x the trough

ccstatusline   (native pre-calculated % 2026-01-13; rate_limits 2026-03-19)
  2025-12  11,292 | 2026-01  16,506 | 2026-02  73,724
  2026-03 252,169 | 2026-05 317,905 | 2026-07 409,745  <- 25x
```

Verified independently by me on 2026-08-04 `[PRIMARY]`: `ccstatusline` **407,682** and `ccusage` **445,521** downloads in the 2026-07-04 → 08-02 window. Repo state `[PRIMARY]`: `sirmalloc/ccstatusline` **12,205★, MIT, last push 2026-08-03**; `ryoppippi/ccusage` **17,700★, last push 2026-08-04**. **Neither is archived. Neither monetises** — ccstatusline's entire `.github/FUNDING.yml` is `buy_me_a_coffee: sirmalloc` `[PRIMARY]`.

**Finding 2 — the competing-product case COLLAPSED. Same ecosystem, same year, same licence.**

`slopus/happy`, a third-party mobile/web client for Claude Code — MIT, **23,085★**, still actively developed (66 commits in July 2026, last push 2026-08-03) `[PRIMARY]`. Its npm CLI usage `[PRIMARY]`:

```
happy-coder   (native Remote Control 2026-02-25; PushNotification tool 2026-04-15)
  2026-01 19,441 | 2026-02 24,103 | 2026-03 25,302  <- peak
  2026-04 12,883 | 2026-05  5,685 | 2026-06  4,739 | 2026-07 3,775
```
I measured **3,247** in the 2026-07-04 → 08-02 window `[PRIMARY]`. **–87% from peak in five months**, with the inflection landing exactly on the native rollout — in a maintained, 23,000-star, MIT project.

**Finding 3 — the status-line niche has zero archived casualties but visible dormancy.** Across ~25 `claude code statusline` repos queried, **not one is archived** `[PAGE, GitHub search API]`. The two that went quiet: `Haleclipse/CCometixLine` (**3,440★**, no licence, last push **2026-03-14**; commits 40 in 2025-08 → 14 in 2026-01 → 1 → 1) `[PRIMARY, confirmed by me 2026-08-04]` and `nilbuild/claude-statusline` (1,360★, MIT, last push 2026-04-03) `[PAGE]`. Both stopped within ~3 months of the pre-calculated-percentage fields shipping. **Correlation only — no maintainer statement, and I am not claiming causation.**

**Finding 4 — the notification-hook niche barely exists, and this is a market-size finding, not an absorption one.** Searching `claude code notification sound` returns a top result with **1 star**; `claude code hooks notification` tops out at **17 stars** (`BND-1/claude-code-hooks-notification`, last push 2026-07-30) `[PAGE, GitHub search API]`. For calibration: status line peaks at 12,205★, usage monitoring at 17,700★. **echook at 78 stars is near the top of a niche whose visible ceiling is ~17 stars — but that niche has roughly a thousandth the pull of the two adjacent ones.**

**Finding 5 — a warning against pattern-matching on `archived=true`.** `iannuttall/claude-agents` (2,050★, archived, last push 2025-07-25) and `iannuttall/claude-sessions` (1,211★, archived, 2025-06-16) look like absorption cases but carry no archive note saying so `[PAGE]`. And `slopus/happy-cli` is archived for an unrelated reason its README states plainly: "This repository has been merged to the main one" `[PAGE]`. I nearly filed it as absorption; it isn't.

### The classic historical cases

| Utility | Native feature that overlapped | Date | Outcome | Source |
|---|---|---|---|---|
| **Karelia Watson** | Apple Sherlock 3 | **Mac OS X 10.2, 2002** | **Absorbed–died.** Origin of "sherlocking": "Apple releasing a feature that supplants or obviates third-party software." Sale/shutdown dates `[UNVERIFIED]` — karelia.com refused connection | [Sherlock (software)](https://en.wikipedia.org/wiki/Sherlock_(software)) `[PAGE]` |
| **Growl** | macOS Notification Center (OS X 10.8) | retirement ≈2020 `[UNVERIFIED exact date]` | **Absorbed–died.** Its own site: "Growl is a retired project…" and "Developers who integrated Growl with their application are advised to migrate to Apple's solution" | [growl.github.io/growl](https://growl.github.io/growl/) `[PAGE]` |
| **Sparrow** | Gmail / Inbox | acquired **2012-07-20** | **Acquired–died.** Google "announced it would cease further development except for critical bug fixes" | [Sparrow](https://en.wikipedia.org/wiki/Sparrow_(email_client)) `[PAGE]` |
| **Mailbox** | Dropbox strategy shift | launched 2013-02-07, acquired 2013-03, killed **2016-02-26** | **Acquired–died** | [Mailbox](https://en.wikipedia.org/wiki/Mailbox_(application)) `[PAGE]` |
| **Bower** | npm / yarn | last push 2024-10-13 | **Absorbed–died, self-declared.** Its own README: "psst! While Bower is maintained, we recommend yarn and webpack or parcel for new front-end projects!" 14,914★, MIT | GitHub API + README `[PAGE]` |
| **request** | native `fetch` | issue #3142 opened 2019-03-30, **still open**; last push 2024-08-14 | **Absorbed–died.** 25,521★ | [request#3142](https://github.com/request/request/issues/3142) `[PAGE]` |
| **f.lux** | Night Shift (2017) | — | **SURVIVED–FREE.** macOS/Windows/Linux; "Free for macOS," corporate editions sold separately | [justgetflux.com](https://justgetflux.com/) `[PAGE]` |
| **Alfred** | Spotlight | — | **SURVIVED–PAID.** Powerpack **£34 single-user**, **£59 Mega Supporter** with lifetime upgrades, one-time perpetual | [alfredapp.com/powerpack](https://www.alfredapp.com/powerpack/) `[PAGE]` |
| **Raycast** | Spotlight | — | **SURVIVED–FREEMIUM.** Free $0 incl. Window Management + Clipboard History; **Pro $8/mo annual**; Teams Pro $12/user/mo. **The paid tier is cloud sync + AI** | [raycast.com/pricing](https://www.raycast.com/pricing) `[PAGE]` |
| **Rectangle** | macOS window tiling | last push **2026-08-02** | **SURVIVED–FREE** (+ paid Pro sibling; price `[UNVERIFIED]`). 29,619★ | [rectangleapp.com](https://rectangleapp.com/) + GitHub API `[PAGE]` |
| **Luna Display** | Apple Sidecar (2019) | — | **SURVIVED–PAID.** Still **$89.99** in 2026. It is a hardware dongle | [astropad.com/product/lunadisplay](https://astropad.com/product/lunadisplay/) `[PAGE]` |
| **Duet Display** | Apple Sidecar (2019) | — | **SURVIVED**, active in 2026; pricing `[UNVERIFIED]` (/pricing/ 404s) | [duetdisplay.com](https://www.duetdisplay.com/) `[PAGE]` |
| **ccusage** | `/usage` (2025-09-29) | — | **SURVIVED–FREE, 6× growth** | npm + GitHub API `[PRIMARY]` |
| **ccstatusline** | statusLine pre-calc % (2026-01-13) | — | **SURVIVED–FREE, 25× growth.** Monetisation: a Buy Me a Coffee link | npm + FUNDING.yml `[PRIMARY]` |
| **Happy (happy-coder)** | Remote Control (2026-02-25) + push tool (2026-04-15) | — | **SURVIVED-AS-CODE, DIED-AS-PRODUCT.** –87% downloads in 5 months while shipping 66 commits/month | npm + GitHub API `[PRIMARY]` |
| **CCometixLine** | statusLine pre-calc % | — | **DORMANT.** 3,440★, not archived, last push 2026-03-14 | GitHub API `[PRIMARY]` |

### The honest base rate

Of 16 rows: **6 died** (Watson, Growl, Sparrow, Mailbox, Bower, request) · **7 clearly survived** (f.lux, Alfred, Raycast, Rectangle, Luna, ccusage, ccstatusline) · **1 survived-as-code-died-as-product** (Happy) · **1 dormant-but-unburied** (CCometixLine) · **1 survived with unverified economics** (Duet).

**≈40% death / ≈45% survival / ≈15% zombie — a coin flip, not a death sentence.** The sample is biased toward famous cases in both directions and should not be reported as "most utilities die."

**The split is not random, and the sorting variable is not the one people expect.**

**It is NOT free-vs-paid.** Survivors include £34 Alfred, $89.99 Luna and $8/mo Raycast — *and* free f.lux, free MIT Rectangle, free MIT ccusage, free MIT ccstatusline. Casualties include paid Watson and paid Growl *and* free MIT Bower and free Apache request. **Charging money did not predict survival in either direction in this sample, and any claim that it does is unsupported by this data.**

**The variable that does sort it: is the native feature an EXTENSION POINT or a COMPETING PRODUCT?**
- `statusLine` is an API Anthropic ships *so that* third parties render it; the field additions of 2026-01-13 and 2026-03-19 made third-party status lines *cheaper to write*. ccstatusline went **25×**.
- Remote Control is an end-to-end first-party product occupying the same job as Happy. Happy went **–87%**.
- **Same platform. Same year. Same MIT/free/local licensing. Opposite outcomes.** The licensing model explains nothing; the API-vs-product distinction explains everything.

Secondary survivor traits, each with a case: **cross-platform reach the first party won't serve** (f.lux ships macOS + Windows + Linux; Night Shift is Apple-only `[PAGE]`) · **a substrate the platform can't replicate** (Luna is a physical dongle, still $89.99 seven years after Sidecar `[PAGE]`) · **configurability depth** (Rectangle, 29,619★, still shipping 2026-08-02 `[PAGE]`) · and, where survivors charge, **they charge for hosted things** (Raycast's free tier includes Window Management; the $8 buys cloud sync and AI `[PAGE]`) — the same conclusion Q3 reached independently from the VS Code side.

> **What this implies for echook:** the absorption fear is largely misplaced, and this is the report's most *encouraging* finding. echook sits on hooks and statusLine — **extension points**, which Anthropic confirms work on every provider and every plan `[PAGE, feature-availability]` — not against a competing product. It also holds two survivor traits: **cross-platform** (Windows/Linux/macOS) and **cross-editor** (Claude Code + Cursor + Codex), neither of which any first party will serve. The probability that echook is killed is low. The probability that echook *earns* is what the other five sections address, and survival and revenue turn out to be orthogonal: ccstatusline is the same shape, 156× bigger, and its business model is a tip jar.

---

## Q5 — The acquihire path

### Anthropic's complete acquisition history (short, and none of it is a small utility)

| Date | Target | What actually happened |
|---|---|---|
| **2025-08-13** | Humanloop | **Acqui-hire, not an acquisition.** Three co-founders + ~a dozen engineers joined; Anthropic explicitly did **not** acquire assets or IP. Humanloop had raised $7.91M | [techcrunch.com/2025/08/13/…](https://techcrunch.com/2025/08/13/anthropic-nabs-humanloop-team-as-competition-for-enterprise-ai-talent-heats-up/) `[PAGE]` |
| **2025-12-03** | **Bun (Oven Inc.)** | A real acquisition of the OSS project and team, framed around Claude Code infrastructure. **"more than 7 million monthly downloads," "over 82,000 stars on GitHub"** | [anthropic.com/news/…acquires-bun…](https://www.anthropic.com/news/anthropic-acquires-bun-as-claude-code-reaches-usd1b-milestone) `[PAGE]` |
| **2026-05-18** | Stainless | SDK / MCP-server tooling platform; reported "may exceed $300 million" | `[SNIPPET]` |

Wikipedia's Anthropic article lists **only Bun and Stainless** as acquisitions — consistent with Humanloop being a team hire `[PAGE]`.

### Anysphere / OpenAI / Replit

- **Supermaven → Anysphere, 2024-11-12** `[SNIPPET]` — **not a small utility**: venture-backed, **$12M Series A led by Bessemer** in September 2024, founder previously created Tabnine.
- **Koala → Anysphere, 2025-07-18** `[SNIPPET]` — an enterprise CRM startup, acquired for an enterprise-readiness team.
- **OpenAI/Windsurf: the deal collapsed** over IP conflicts tied to the Microsoft partnership; **Google** paid **$2.4B** to license the technology and hire the CEO and key engineers; **Cognition** bought the remaining product and brand. `[SNIPPET, no primary page fetchable]`
- **Statsig → OpenAI, 2025-09-02** (~$1.1B all-stock) and **Alex → OpenAI, 2025-09-05** (a YC-backed team building Xcode AI tooling) `[SNIPPET]`. Alex is the closest to "small ecosystem utility" — and it was a funded company with a team.
- **Replit's first-ever acquisition was OpenInt, 2025-09-30**, a YC W23 integration company `[SNIPPET]`.
- **Sourcegraph and Warp: no acquisitions found.** One search, null result — not proof of absence `[UNVERIFIED]`.

### The strongest individual-maintainer precedents — and their adoption at the moment of hire

- **Don Jayamanne → Microsoft, 2017-11-09.** Microsoft hired the author of the most popular VS Code Python extension after being "impressed by his work"; he had been building it part-time for a couple of years. [devblogs.microsoft.com/python/don-jayamanne-joins-microsoft](https://devblogs.microsoft.com/python/don-jayamanne-joins-microsoft/) `[PAGE]`. The Microsoft post gives **no** download numbers; contemporaneous coverage puts the extension at **over 4.2 million downloads** `[SNIPPET, visualstudiomagazine.com]`.
- **Eric Amodio / GitLens → GitKraken, 2021-10-08.** GitLens was created in 2016 and **maintained nearly single-handedly as a side project**; at acquisition it had **11 million active users and 71 million downloads over five years**. Amodio joined as CTO. [prnewswire.com/…gitlens…join-gitkraken…](https://www.prnewswire.com/news-releases/gitlens-for-visual-studio-code-and-its-creator-eric-amodio-join-gitkraken-301396298.html) `[PAGE]`
- **Rich Harris → Vercel, 2021-11-11**, hired to work on Svelte full-time. Svelte then: **"over 200,000 weekly downloads, more than 50,000 GitHub stars."** [vercel.com/blog/vercel-welcomes-rich-harris…](https://vercel.com/blog/vercel-welcomes-rich-harris-creator-of-svelte) `[PAGE]`
- **Turborepo → Vercel, 2021-12-09** — the only case where the project may have been small, and **nobody published a number**: neither Vercel's post nor TechCrunch disclosed stars, downloads, users or team size. Turborepo had raised no external funding. Its author already carried an established OSS reputation from Formik and TSDX, per Vercel's own post. `[PAGE]` ×2

**One claim discarded rather than softened:** a snippet asserted that Boris Cherny "built an open-source Claude Code tool that gained traction before Anthropic brought him on staff," with a 115K-star figure. No primary source confirmed it and the framing contradicts the commonly-reported history. **Do not use it.**

### The number you asked for

Every verifiable case sits at: **Bun 82,000★ / 7M monthly downloads · Svelte 50,000★ / 200k weekly · GitLens 11M active users / 71M downloads · VS Code Python 4.2M downloads.** Every AI-coding-era deal — Supermaven, Koala, Alex, Statsig, Humanloop, Stainless, OpenInt — was a **funded company with a team**, not a utility.

**Zero precedent, at any of these companies, of a solo unfunded ecosystem utility at double-digit stars leading to a hire or acquisition. And a specific search for any Claude Code community plugin / hook / status-line maintainer being hired or acquired returned nothing.**

> **What this implies for echook:** at 78 stars this is a lottery ticket, and not a well-priced one. The verified entry level is roughly **three orders of magnitude above echook's current adoption** — tens of thousands of stars or millions of installs — and the observed criterion is "the single most popular thing in its category," not "a well-made 78-star utility." The path is *real* (Jayamanne and Amodio are genuine solo-maintainer precedents) but it is an uncontrollable upside, never a plan. Treating it as a plan would be the planning error.

---

## Q6 — The portfolio-piece / lead-generation path

**Take this seriously: it is probably the correct answer, and it is the only path in this document with a sourced price 50–250× the product pool.**

### The academic literature is narrower — and more uncomfortable — than the folklore

The one rigorous study of **economic returns to OSS participation**: **Hann, Roberts & Slaughter, *Information Systems Research* 24(3):520–538 (2013)** — six years, programmers across three Apache Software Foundation projects. [pubsonline.informs.org/doi/abs/10.1287/isre.2013.0474](https://pubsonline.informs.org/doi/abs/10.1287/isre.2013.0474) `[PAGE]`

- **Contribution volume alone produces no wage premium.** "Greater open source participation per se, as measured in contributions made, is not associated with wage increases." `[SNIPPET, quoted across the authors' related papers]`
- **Earned rank inside a meritocracy does** — high rank in the community's merit system was associated with **as much as an 18% wage increase** `[PAGE]`.
- Mechanism: "rank within an OSS meritocracy is a credible and precise signal of participants' productive capacity" `[PAGE]`.

**What this means for echook, plainly:** the measurable return attaches to *earned standing in a community others already care about*, not to *having shipped a thing*. A self-owned 78-star repo is the "contribution volume" variable, which the study found does nothing. **Merged, visible contributions to a project the buyer already uses is the variable that paid 18%.**

**Claims deleted rather than softened.** Everything that came back on recruiter behaviour — "60–80% of tech recruiters glance at linked GitHub profiles," "recruiters spend 11 seconds on a GitHub profile" — traces to SEO content-marketing blogs (fonzi.ai, tierones.in, slategit.com) with **no named survey, sample or year** `[SNIPPET, all]`. HackerRank's 2025 Developer Skills Report is real ("97% of developers use AI assistants," "74% of developers still struggle to land jobs") `[SNIPPET]` but contains **no** percentage on hiring managers weighting GitHub or personal projects. Stack Overflow's 2025 survey (49,000+ developers, 177 countries `[SNIPPET]`) yielded **no survey item** linking OSS contribution to hiring outcomes `[UNVERIFIED]`. **"Recruiters look at your GitHub" has no primary source I could verify this session.**

### The consulting-lead-gen channel: one real, on-point anecdote and nothing quantitative

The single most relevant evidence found is a developer-consultant almost exactly in echook's position. **Stu Mason**, a developer consultant in Folkestone, UK, writes that "open source is the best marketing channel for a developer consultancy. It's trusted more than advertising, it demonstrates competence rather than claiming it." His one concrete attribution: **"I've had clients tell me directly: 'I found your Claudavel package, liked the code quality, and that's why I reached out.'"** Time cost: **3–5 hours/week** on maintenance. He gives **no lead counts, no conversion rate, no revenue**. [stumason.dev/articles/open-source-as-marketing](https://stumason.dev/articles/open-source-as-marketing) `[PAGE]`

That is notable because Claudavel is a *Claude-adjacent package* — the same buyer pool. But it is n=1, self-reported, unquantified.

Everything else was vendor content or low-quality/likely-AI-generated SEO (dev.to/armorbreak claiming "$15K+ freelancing in the past year," dredyson.com, yewiki.org) `[SNIPPET]` — **not treated as evidence.** And one stat cuts *against* passive inbound: "74% of top-earning freelancers found their best clients through direct outreach," 2025 State of Freelance Report `[SNIPPET, low confidence, primary not fetchable]`.

### What a landed client is actually worth

- **Clutch** (first-party reviews from verified clients): software development companies charge **$24–$49/hour**, some **$50–$99+**; custom software projects typically fall in the **$10,000–$49,999** band; the *average* project on Clutch is **$132,480.29** over ~13 months. Sample size not disclosed. [clutch.co/developers/pricing](https://clutch.co/developers/pricing) `[PAGE]`
- Independent freelancers: **$52–$60/hour** generalist, **$100–$250/hour** for AI/ML specialists `[SNIPPET, freelanly.com]`.
- Upwork's own cost page reports a **$20/hour median** for software developers `[SNIPPET — upwork.com returned HTTP 403 to direct fetch]`.
- BLS median pay: `[UNVERIFIED]` — bls.gov returned HTTP 403.

### The "AI-agent-first" angle: a real industry trend, with zero career evidence

"Agent-first" / "agent-native" is a recognised 2026 architectural and investment category `[SNIPPET, agentmarketcap.ai, dev.to]`. **But I found no evidence whatsoever that "I build agent-first software" functions as a hiring credential or a differentiator buyers recognise and search for.** The strongest indirect signal that the *market* is real is that Anthropic paid for Bun explicitly to serve Claude Code, and Claude Code hit **$1B run-rate revenue six months after public launch** `[PAGE]` — that proves the market, not the credential.

### Defensible estimate, reasoning visible

**No false precision.** Here is the arithmetic and every input's provenance:

**Value of one landed client:** a small custom app sits in Clutch's **$10,000–$49,999** band `[PAGE]`. A conservative solo version — no agency overhead, one well-scoped app — is realistically the bottom of that band: **$10,000–$20,000 gross per engagement**, or **100–150 billable hours** at the $100–$250/hr individual-specialist rate `[SNIPPET]`.

**Probability of landing one from an unadvertised README line at 78 stars: I have no basis to estimate it, and neither does anyone I could find.** There is exactly one first-person report of this channel working at all (Stu Mason, unquantified, on a Claude-adjacent package) `[PAGE]`, no conversion data anywhere, and no measurement on echook's own pitch.

**So the honest formulation is a conditional, not a forecast:** this path is worth **one $10,000–$20,000 engagement per year if it converts even once, and $0 if it doesn't** — and there is currently no evidence base to say which. **Anyone quoting an expected annual value here is making it up.**

What the literature *does* license directionally: the 18% return attached to **earned rank in a community others already participate in**, not to owning a repo `[PAGE]`. That is a sourced argument that echook's career value would rise more from **visible contributions inside the Claude Code / Cursor / Codex ecosystems** than from echook's own star count.

### Making it measurable — the actual gap, and it is fixable this week

1. **Instrument the pitch.** The README "let's talk" line is a bare `mailto:` with no attribution — the channel is not underperforming, it is *unmeasured*. A unique tracked landing URL is the minimum viable instrument; then you know *whether* the channel exists before arguing about its size. GitHub's repo Insights → Traffic gives referrer and clone data for free, and nobody is reading it today.
2. **Separate the two funnels.** "Someone installed echook" and "someone considered hiring me" are different events sharing one undifferentiated README.
3. **Case-study framing beats a pitch line.** The one real mechanism was *"liked the code quality"* `[PAGE]` — the artefact did the selling, not the ad. A short "how this was built / what it does for an agent" write-up is closer to what actually converted than a hire-me sentence is.
4. **Fish where the 18% lives.** Merged upstream contributions and visibility inside the Claude Code ecosystem, not more polish on a self-owned repo `[PAGE, Hann et al.]`.

> **What this implies for echook:** this is the only path in the report where the sourced price of a single success ($10,000–$20,000) exceeds the *entire* realistic annual product pool ($0–$200) by **50× to 250×** — and the channel is already shipped and costs nothing more to run. It is also the only one where nine months of visible, high-quality engineering is an *asset* rather than a sunk cost. It is not proven; it is **unmeasured**, which is a different and much cheaper problem.

---

## THE STRONGEST DISCONFIRMING EVIDENCE — at full strength, in its own section

Everything above points one way. Discipline requires finding the cases that point the other way and stating them at full strength before concluding. Here they are. I have not softened any of them.

### 1. `bolagnaise/PowerSync` — 87 stars, 29 public sponsors

`[PRIMARY, GitHub REST + GraphQL, 2026-08-04]`

- Repo: "Intelligent battery optimisation for Home Assistant. Supports a wide range of battery systems, electricity providers, and AC-coupled solar inverters. Includes EV charging coordination and a built-in LP optimiser." **87 stars.**
- Owner `bolagnaise`: bio "Just a geek," **13 followers**. Next-largest repos: 27★, 14★, 2★. **There is no hidden famous project carrying these sponsorships.**
- Public Sponsors listing. **`sponsors.totalCount` = 29.** Active goal `TOTAL_SPONSORS_COUNT`, "50 monthly sponsors," **56% complete**. Recurring tiers: **$4, $8, $15, $25, $50/month**.
- *My arithmetic, explicitly labelled inference and not a disclosure:* 29 sponsors all at the **lowest** $4 tier is a floor of **$116/month ≈ $1,392/year**. GitHub does not publish the actual amount — `monthlyEstimatedSponsorsIncomeInDollars` does not exist on the public `User` type (tested; the API returns `undefinedField`).

**This is a genuine counterexample to everything in Q1: a niche 87-star utility, by a developer with 13 followers, pulling ~30 sponsors.** It is 9 stars above echook and its owner has 209 fewer followers.

### 2. `opendcs` — 50 stars, $1,530 received in under four months

`[PRIMARY, Open Collective GraphQL, 2026-08-04]` — "Open Data Collection System for Hydro/Meteorologic Data." The single best result in the entire 0–99-star band, and it came from a 50-star project.

**What both of these share, and what a general-purpose dev utility does not:** a **specific, non-developer-substitutable user base with money and no alternative** — home-battery owners saving on electricity bills; hydrological agencies with procurement budgets. **Neither is a developer productivity tool.** The people who pay are people who cannot write the software themselves.

### 3. Ref (ref.tools) — a paid MCP server that works

**"$9/month for 1,000 credits ($0.009 per search)"**, 200 free credits, and after three months "**thousands of weekly users and hundreds of subscribers** with more signing up and subscribing everyday." [pulsemcp.com/posts/pricing-the-unknown-a-paid-mcp-server](https://www.pulsemcp.com/posts/pricing-the-unknown-a-paid-mcp-server) `[PAGE]`. Monetisation in this ecosystem is not impossible. It is metered and hosted.

### 4. Wallaby.js / Quokka Pro — the case that breaks "you need a hosted component"

Closed source, **fully local, no server**, and it has sustained a **perpetual-licence business for years**: "Perpetual license + 1 year of updates / upgrades," personal named-user vs company seat licences, volume discounts at 10 and 20 users, renewal discounts of 50% personal / 10% company. [wallabyjs.com/purchase](https://wallabyjs.com/purchase/) + [wallabyjs.com/docs/intro/license.html](https://wallabyjs.com/docs/intro/license.html) `[PAGE]`. **The single strongest refutation of Q3's dominant characteristic (a).** Its distinguishing property is a **proprietary core** — which is the one property echook cannot acquire retroactively.

### 5. Alfred — survived Spotlight for over a decade, and charges

**£34 single-user Powerpack, £59 with lifetime upgrades**, one-time perpetual, still sold in 2026 [alfredapp.com/powerpack](https://www.alfredapp.com/powerpack/) `[PAGE]`. A utility duplicated by a first-party OS feature can charge and endure. (Closed source.)

### 6. The strongest one, and it is in-ecosystem: absorption did not happen — growth did

`ccusage` grew **6×** in monthly npm installs *after* Anthropic shipped native `/usage`. `ccstatusline` grew **25×** *after* Anthropic shipped the native pre-calculated status-line percentages `[PRIMARY]`. **The "the platform will kill you" thesis is directly falsified inside this exact ecosystem, in the last twelve months, twice.**

**And this is where the disconfirming evidence turns back on itself, which is why it belongs here rather than in a footnote.** ccstatusline reached **12,205 stars and 407,682 monthly installs** on a wave that its native "competitor" *caused* — and its entire monetisation apparatus is `buy_me_a_coffee: sirmalloc` `[PRIMARY]`. **The best disconfirming case for absorption is simultaneously the most damning confirming case for revenue.** In this ecosystem, growth and money have been demonstrated to be orthogonal.

---

## EVERY NAMED COMPARABLE

| Name | Adoption | Disclosed revenue | Model | Source | Grade | Date |
|---|---|---|---|---|---|---|
| **echook** (subject) | **78★**, not on PyPI; owner 222 followers | **$0**; Sponsors listing live, **0 sponsors** | MIT, free, local | GitHub REST + GraphQL | `[PRIMARY]` | 2026-08-04 |
| **ccstatusline** | **12,205★**, **407,682 installs/mo** | **none**; `buy_me_a_coffee` only | MIT, free, local | GitHub + npm + FUNDING.yml | `[PRIMARY]` | 2026-08-04 |
| **ccusage** | **17,700★**, **445,521 installs/mo** | none | MIT, free | GitHub + npm | `[PRIMARY]` | 2026-08-04 |
| **happy / happy-coder** | 23,085★, **3,247 installs/mo** (−87% from peak) | none | MIT, free | GitHub + npm | `[PRIMARY]` | 2026-08-04 |
| **CCometixLine** | 3,440★, dormant since 2026-03-14 | none | no licence | GitHub API | `[PRIMARY]` | 2026-08-04 |
| **~79★ tier composite** | 70–90★ band | **$0 median**; 7% of owners have ≥1 public sponsor | donations | GitHub + OC APIs | `[PRIMARY]` | 2026-08-04 |
| median npm project w/ donation page | — | **$55 / 9 months** | donations | [ICSE 2020 PDF](https://cmustrudel.github.io/papers/overney20donations.pdf) | `[PAGE]` | 2020 |
| repos asking for donations at all | 25,885 of 77.9M | **0.04%** | — | same | `[PAGE]` | 2020 |
| repos clearing $1,000/mo | — | **5%** npm / **10%** GitHub | donations | same | `[PAGE]` | 2020 |
| all maintainers | — | **60% unpaid hobbyists**; 12% professional | — | [Tidelift 2024 PDF](https://www.sonarsource.com/the-2024-tidelift-maintainer-impact-report.pdf) | `[PAGE]` | Nov 2024 |
| GitHub Sponsors (platform) | 103 regions | **$40M+ cumulative**, 4.2K+ org sponsors | donations | [github.com/sponsors](https://github.com/sponsors) | `[PAGE]` | 2026-08-04 |
| Open Collective (platform) | 10,000+ collectives | **$40M managed** | donations | [opencollective.com](https://opencollective.com/) | `[PAGE]` | 2026-08-04 |
| **bolagnaise/PowerSync** ⭐DISCONFIRMING | **87★**, owner 13 followers | **29 public sponsors**, tiers $4–$50/mo | GH Sponsors | GitHub GraphQL | `[PRIMARY]` | 2026-08-04 |
| **opendcs** ⭐DISCONFIRMING | **50★** | **$1,530** in <4 months | Open Collective | OC GraphQL | `[PRIMARY]` | 2026-08-04 |
| husky | 35,249★, "1.2M+ projects" | **$410/yr** (lifetime $31,749) | Open Collective | [opencollective.com/husky](https://opencollective.com/husky) | `[PAGE]` | 2026-08-04 |
| gulp | 32,957★ | **$1,989/yr** | Open Collective | opencollective.com/gulpjs | `[PAGE]` | 2026-08-04 |
| jest | 45,460★ | **$9,682/yr** | Open Collective | OC API | `[PRIMARY]` | 2026-08-04 |
| mocha | 22,905★ | $24,415/yr, 1,179 backers | Open Collective | [opencollective.com/mochajs](https://opencollective.com/mochajs) | `[PAGE]` | 2026-08-04 |
| babel | 43,973★ | **$276,238/yr**, 1,258 backers | Open Collective | OC API | `[PAGE]` | 2026-08-04 |
| Caleb Porzio (Livewire) | not stated | $112,680/yr target; ~$25k Sponsors cash | **sponsorware + paid screencasts** | [calebporzio.com](https://calebporzio.com/i-just-hit-dollar-100000yr-on-github-sponsors-heres-how-i-did-it) | `[PAGE]` | — |
| Filippo Valsorda (Go crypto) | — | 6 clients, tiers "five-figures range (USD, yearly)"; total undisclosed | **B2B retainers** | [words.filippo.io](https://words.filippo.io/full-time-maintainer/) | `[PAGE]` | Feb 2023 |
| **Ref (ref.tools)** ⭐DISCONFIRMING | "thousands of weekly users" | "**hundreds of subscribers**" @ $9/mo; total undisclosed | **metered hosted MCP** | [pulsemcp.com](https://www.pulsemcp.com/posts/pricing-the-unknown-a-paid-mcp-server) | `[PAGE]` | 2025-09-10 |
| SkillHQ | 439+ skills | **0 sales on every featured listing** | 80/85% rev share | [skillhq.dev](https://skillhq.dev/) | `[PAGE]` | 2026-08-04 |
| claudemarketplaces.com | 23.5k skills / 380k visitors/mo | **ad inventory sold out**; all plugins free | **advertising** | [claudemarketplaces.com](https://claudemarketplaces.com/) | `[PAGE]` | 2026-08-04 |
| SafeWeave | 120+ Discord devs | none; "conversion from free to paid is lower than we expected" | freemium MCP | [indiehackers.com](https://www.indiehackers.com/post/we-launched-a-security-scanner-for-ai-generated-code-4-weeks-ago-honest-report-2f439a28a4) | `[PAGE]` | 2026 |
| Claude Code marketplaces on GitHub | **15,728** manifests | 3 mention Gumroad, 1 mentions Polar | — | GitHub code search | `[PRIMARY]` | 2026-08-04 |
| **Wallaby/Quokka** ⭐DISCONFIRMING | — | price `[UNVERIFIED]` | **proprietary, LOCAL, perpetual licence** | [wallabyjs.com/purchase](https://wallabyjs.com/purchase/) | `[PAGE]` structure | 2026-08-04 |
| **Alfred** ⭐DISCONFIRMING | — | **£34 / £59** one-time | proprietary, local, perpetual | [alfredapp.com/powerpack](https://www.alfredapp.com/powerpack/) | `[PAGE]` | 2026-08-04 |
| Raycast | — | Free · **Pro $8/mo** · Teams $12/user/mo | **paid tier = cloud sync + AI** | [raycast.com/pricing](https://www.raycast.com/pricing) | `[PAGE]` | 2026-08-04 |
| Luna Display | — | **$89.99** | hardware dongle | [astropad.com](https://astropad.com/product/lunadisplay/) | `[PAGE]` | 2026-08-04 |
| Copilot | — | Free · **$10** · $39 · $100 /mo | hosted inference | [github.com/features/copilot/plans](https://github.com/features/copilot/plans) | `[PAGE]` | 2026-08-04 |
| Tabnine | — | **$39** / **$59** per user/mo annual | hosted + seats | [tabnine.com/pricing](https://www.tabnine.com/pricing/) | `[PAGE]` | 2026-08-04 |
| GitLens | — | **$10/seat/mo** list | private-repo gating + seats | [gitkraken.com/gitlens/pricing](https://www.gitkraken.com/gitlens/pricing) | `[PAGE]` | 2026-08-04 |
| Thunder Client | — | **$3 / $7 / $16** per user/mo annual | seats + PO/SSO | [thunderclient.com/pricing](https://www.thunderclient.com/pricing) | `[PAGE]` | 2026-08-04 |
| SonarQube for IDE | — | **extension FREE**; Cloud Team "starts at $34 monthly" | hosted server | [sonarsource.com](https://www.sonarsource.com/plans-and-pricing/) | `[PAGE]` | 2026-08-04 |
| Kite | 20 TB crawl, proprietary model | **DEAD**, source dumped BSD-3 | proprietary data | [kiteco/kiteco-public](https://github.com/kiteco/kiteco-public) | `[PAGE]` | 2022-12-01 |
| Pushover | — | **$4.99 one-time/platform**; **Teams $5/user/mo** | hosted push | [pushover.net/pricing](https://pushover.net/pricing) | `[PAGE]` | 2026-08-04 |
| ntfy | — | Supporter $6/$5 · Pro $12/$10 · Business $25/$20 per mo | **Apache-2.0/GPLv2 + paid hosting** | [ntfy.sh](https://ntfy.sh/) | `[PAGE]` | 2026-08-04 |
| PagerDuty | — | **$21 / $41** per user/mo annual | seats + SLA | [pagerduty.com/pricing](https://www.pagerduty.com/pricing/) | `[PAGE]` | 2026-08-04 |
| Langfuse | — | $0 · **$29** · **$199** · **$2,499**/mo; "$8/100k units" | **open source + metered hosting** | [langfuse.com/pricing](https://langfuse.com/pricing) | `[PAGE]` | 2026-08-04 |
| Helicone | 5.8K★ | Free · **$79/mo** · **$799/mo** | metered hosting | [helicone.ai/pricing](https://www.helicone.ai/pricing) | `[PAGE]` | 2026-08-04 |
| LangSmith | — | $0 · **$39/seat/mo**; $1.50/LCU, $1.00/LSU | traces + seats | [langchain.com/pricing-langsmith](https://www.langchain.com/pricing-langsmith) | `[PAGE]` | 2026-08-04 |
| Claude Pro / Max / Team | — | **$17–20/mo · from $100/mo · $20–100/seat/mo** | the buyer's existing spend | [claude.com/pricing](https://claude.com/pricing) | `[PAGE]` | 2026-08-04 |
| **Bun → Anthropic** | **82,000★ / 7M downloads/mo** | acquired | acquisition threshold | [anthropic.com/news](https://www.anthropic.com/news/anthropic-acquires-bun-as-claude-code-reaches-usd1b-milestone) | `[PAGE]` | 2025-12-03 |
| **Svelte / Rich Harris → Vercel** | **50,000★ / 200k weekly** | hired | hire threshold | [vercel.com/blog](https://vercel.com/blog/vercel-welcomes-rich-harris-creator-of-svelte) | `[PAGE]` | 2021-11-11 |
| **GitLens / Amodio → GitKraken** | **11M users / 71M downloads** | acquired, joined as CTO | solo-maintainer precedent | [prnewswire.com](https://www.prnewswire.com/news-releases/gitlens-for-visual-studio-code-and-its-creator-eric-amodio-join-gitkraken-301396298.html) | `[PAGE]` | 2021-10-08 |
| **Don Jayamanne → Microsoft** | **4.2M downloads** `[SNIPPET]` | hired | solo-maintainer precedent | [devblogs.microsoft.com](https://devblogs.microsoft.com/python/don-jayamanne-joins-microsoft/) | `[PAGE]` | 2017-11-09 |
| Clutch (custom software projects) | — | **$10,000–$49,999** typical; avg project **$132,480.29** | consulting | [clutch.co/developers/pricing](https://clutch.co/developers/pricing) | `[PAGE]` | 2026-08-04 |
| Hann/Roberts/Slaughter (ISR 2013) | 3 ASF projects, 6 yrs | **rank → up to +18% wages; volume → nothing** | career return | [pubsonline.informs.org](https://pubsonline.informs.org/doi/abs/10.1287/isre.2013.0474) | `[PAGE]` | 2013 |
| Stu Mason (Claudavel) | not stated | **no figures**; "liked the code quality, and that's why I reached out" | OSS→consulting leads | [stumason.dev](https://stumason.dev/articles/open-source-as-marketing) | `[PAGE]` | 2026 |

---

## WHAT WOULD PROVE THIS WRONG

Ordered by cost to test. Full detail and the "which combination overturns vs. dents" analysis lives in the companion sizing file; the base-rate-specific versions are:

| # | Prove-wrong signal | Which base rate it breaks | How to test, in days |
|---|---|---|---|
| **1** | **≥25 people pay $5 for a supporter licence in 14 days** | Q1's $0 median and Q2's zero-disclosed-revenue absence, simultaneously | Open a $5 one-time licence on Polar or Lemon Squeezy (both bypass the missing marketplace rail). Announce to the 78 stargazers + the directories. **One afternoon** |
| **2** | **≥2 of 20 named locked-out orgs reply asking for a quote** | Q3's "you need seats and a hosted component" | Build the list from AWS Bedrock / Google Cloud customer case studies; send 20 emails with a concrete offer. **~3 days** |
| **3** | **≥1 inbound consulting lead attributable to the repo in 60 days** | Q6's "unmeasured, not proven" — the highest-value path | Replace the `mailto:` with a tracked landing URL; read GitHub Insights → Traffic weekly. **1 hour to instrument** |
| **4** | **A price/entitlement field appears in the Claude Code plugin manifest schema** | Q2's decisive finding — removes the structural blocker | Diff `plugins-reference` periodically. **Free, ongoing** |
| **5** | **Any Claude Code / Cursor / Codex add-on discloses >$1,000 MRR** | Q2's absence claim, which is the load-bearing one | Alerts on Indie Hackers + X for "MCP server MRR", "Claude Code plugin revenue". **Free, ongoing** |
| **6** | **echook passes ~1,000 stars** | Q1's threshold analysis and Q5's acquihire floor both move | Nothing to test — just watch. Currently 4 new stars/month and decelerating |

**Items 1 and 2 landing together overturn the verdict; either alone dents it. Items 4 and 5 landing together overturn it more durably** — a rail plus a proven revenue instance means the ecosystem changed underneath these base rates, and every "the absence is the finding" conclusion above expires on that date.

**Standing re-test date: 2027-02-04.**

---

## WHAT I COULD NOT VERIFY — the honest list

1. **X/Twitter build-in-public "$X MRR" disclosures.** X requires authentication; no accessible engine surfaced any. **The single largest gap** — if such disclosures exist, they most likely live there.
2. **Reddit primary sources** — fully blocked by three independent methods (WebFetch refuses; curl and r.jina.ai both 403). The SkillHQ and Agent37 seller threads were reachable only as snippets; **their actual numbers were never seen.**
3. **mcp.so** returned 403; could not check for paid listings. **Smithery's pricing page** 429'd (its docs contain no monetisation content, but an undocumented offering cannot be ruled out).
4. **Actual dollar amounts for any GitHub Sponsors profile.** GitHub does not expose sponsorship income publicly (`monthlyEstimatedSponsorsIncomeInDollars` does not exist on the public `User` type — tested). Every "$X/month from Sponsors" figure anywhere in this report is a maintainer's voluntary blog disclosure, never platform data.
5. **A blog-post income report from a maintainer stating both a dollar figure AND a sub-1,000-star count.** Searched repeatedly across every working engine; not found. The 87-star/29-sponsor case was found by **measurement**, not by anyone's disclosure.
6. **Wallaby/Quokka actual prices** — five fetch routes all return the literal string `"Calculating"`. Needs a browser. It is the best counterexample to Q3's dominant characteristic, so its price would genuinely calibrate the analysis.
7. **Rectangle Pro's price; Duet Display's current pricing** (/pricing/ 404s); **Growl's exact retirement date**; **Watson's sale and shutdown dates** (karelia.com refused connection).
8. **Microsoft's history of announcing-then-abandoning paid extensions.** The *end state* is nailed down at schema level; the *narrative* is not.
9. **Causation for CCometixLine / nilbuild dormancy** — timing correlates with the native percentage fields; no maintainer statement exists and none is claimed.
10. **Whether any MIT/local VS Code extension earns meaningful money, exhaustively.** Checked the five biggest nameable; all top out at a sponsor link. **A strong negative, not a proven one.**
11. **Any primary-source recruiter survey on GitHub profiles in hiring**; any Stack Overflow survey item linking OSS to hiring outcomes; BLS and Upwork rate pages (both HTTP 403).
12. **Any acquisition by Sourcegraph or Warp** — one search, null result, not proof of absence.
13. **echook's own install base** — unknowable by construction: no telemetry (by design), not on PyPI, no download counter. The owner cannot count his own users, which is why Q1's reachable-population figure is a floor built from stars rather than a measurement of usage.
