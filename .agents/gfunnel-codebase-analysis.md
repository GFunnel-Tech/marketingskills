# GFunnel: What We Actually Are (Read From the Code) + Competitor Map

*Prepared 2026-11-09. Source: code, schemas, integrations and pricing configs across the GFunnel-Tech repos — deliberately **not** our marketing copy.*

Repos analyzed: `platform` (live PHP/UNA v15), `gfunnel_com` (legacy source of truth), `gfunnel` (Next.js 15 + Supabase rebuild), `gfunnel-hub` (Service Hub), `gfunnel-services`, `Sales-hub`, `gfunnel-comms`, `security-spark-ads` (Application Hub), `industry-setup-flow`, `methodology`, `ampliphipartners`, `glide-marketing-hub`, `timber-ledger`, `energybillfixer`, `eco-craft-pulse`, `jenny-flow-grow`. (`Content-Machine` and `Ecosystem` are empty. This `marketingskills` repo is an unmodified fork of Corey Haines' skill library — useful tooling, not product.)

---

## 1. The honest one-paragraph answer

GFunnel is **a done-for-you marketing & operations services company with its own software platform wrapped around it.** The deepest, most-tested engineering in the whole org is the **Fulfillment system** (~18.5k lines: a three-party ledger of client ↔ agency/reseller ↔ vendor with separate cost and price, vendor bidding, a white-label/anonymity flag, a 14-service catalogue). The software layer is a **community/business-OS shell (UNA CMS) on top of GoHighLevel**: every business workspace is provisioned as a GHL sub-account under GFunnel's agency, and ~35 GHL screens (funnels, workflows, phone, calendars, Voice AI) are deep-linked into the workspace. Around that sits a **multi-level partner/reseller program** (30–70% commissions, three generations deep) and a **dev shop** that builds client apps in Lovable/Supabase (Glide Media's Meta-ads agency platform, UpSmith/AskJenny, Energy Bill Fixer, KORR, NFT-Trees).

In other words, the code says we are four businesses at once:

| # | Business | Evidence in code | Maturity | Revenue today |
|---|---|---|---|---|
| 1 | **Productized DFY services** (ads, social, funnels, copy, VSL, automation, "AI Employee", admin) | `platform/modules/gfunnel/fulfillment`, `gf_bidding.php`, `gfunnel-hub/src/lib/servicePricing.ts`, retainers in `gfunnel/src/config/plans.ts` | **Deepest** | **Yes** — first named paying client (Rive Creative, Oct 2026) |
| 2 | **All-in-one "business OS" SaaS** (workspaces, app hub, Sales Hub, Organizer, Projects, community, courses, AI agents) | `platform` gf_* modules + GHL sub-account provisioning; `gfunnel` Next.js rebuild | Broad but uneven; GHL auto-provisioning "never run against a live agency" | Gated at $97/$297, unproven |
| 3 | **Partner / reseller network** (ranks, MLM matrix, MRR licences, Business-in-a-Box, industry modules) | `aqb/affiliate`, `inc/gf_partner_blocks`, `Sales-hub`, `ampliphipartners`, `gf_mrr_licence*` | Front-ends real; reseller billing & MRR payouts still spec | Not yet |
| 4 | **Custom build / venture studio** (Lovable + Supabase + n8n + GHL) | glide-marketing-hub, timber-ledger, energybillfixer, jenny-flow-grow, eco-craft-pulse | High delivery speed, several mature builds | Yes (billable hours, e.g. 59.75h AskJenny) |

**The core marketing problem is not wording — it's that we are selling four things to six personas with three price sheets.** Messaging can't fix that until we choose what leads.

---

## 2. Infrastructure & third parties (what the product is really built on)

| Layer | Tools | What it means for positioning |
|---|---|---|
| CRM, funnels, phone, SMS, email, calendars, Voice/Conversation AI, invoices | **GoHighLevel / LeadConnector** (agency OAuth, auto sub-accounts on SaaS plan, snapshots, Sales Hub push, platform CRM) | Our software *is* a GHL white-label underneath. Any buyer who knows GHL will price-compare us to GHL directly. |
| Community, courses, social, marketplace, directory, jobs | **UNA CMS v15** + licensed modules (modzzz listing/jobs, aqb affiliate/SEO, fansonly) | "Community + business OS" is genuinely ours to say, but it's a Skool/Mighty-style category. |
| Automation backbone | **Self-hosted n8n** (`apihub.gfunnel.com`) | Strong fulfillment capability (automation & integration services). |
| AI | NeuronAI agents runtime (DeepSeek default, Anthropic, OpenAI, Gemini, Mistral, Ollama); Anthropic SDK in Next.js; Lovable AI Gateway; ElevenLabs, Higgsfield, PlayAI | "AI Employee" service is credible; AI-agent *software* is built but unproven in production. |
| Payments | Stripe / Stripe Connect, PayPal, Chargebee SDKs, UNA credits wallet | Fulfillment payments are recorded manually, not charged — fix before scaling. |
| Ads | Meta Graph API + CAPI (Glide platform, ~25 meta-* functions) | Paid-ads management is our most productized, highest-ticket service. |
| Messaging / infra | Twilio, Resend, Pusher/Soketi, OneSignal, Mux, Jitsi, Vercel, Upstash, Cloudflare, AWS S3 | Commodity. |
| Build tooling | Lovable, HighLevel AI Studio, Claude Code | We ship fast and cheaply — this is a delivery advantage for services, not a customer-facing feature. |

---

## 3. Pricing found in code (it conflicts — fix before selling)

| Surface | Plans |
|---|---|
| `platform/gf_pricing.php` (public) | Free / Pro "upgrade in-app" / Agency "custom" — **no numbers** |
| `platform/inc/gf_upgrade.inc.php` (actual gate) | Single **$97/mo**, Unlimited **$297/mo**, Done-with-you **from $497/mo** |
| `gfunnel/src/config/plans.ts` | Free, Starter $97, Growth $297, Pro $497, Agency $497, Enterprise |
| `security-spark-ads` | Office $97 / Business $297 (+ "Elite"), $1 for 90 days |
| Service retainers (`gfunnel`) | Starter $1,497 · Pro $2,497 · Scale $3,997 /mo (3-mo min, $83/hr overage) |
| À-la-carte menu (`gfunnel-hub`) | 14 services, $97 → $3,500/mo (Paid Ads Launch $497 / Scale $997 / Growth Partner $3,500 + perf fee) |
| Paid-ads funnel (`gf_paid_ads.php`) | $997/mo core, +$500 expansions, $1,500 build team, $3,000 fractional CSO |
| Business Build (`gf_playbook.php`) | $297 setup + $97/mo, $37 downsell |
| Partner modules (`Sales-hub`) | Foundation $297, Industry $997, Business-in-a-Box |

⚠️ **Our software tiers ($97 / $297 / $497) are identical to GoHighLevel's own tiers ($97 Starter / $297 Unlimited / $497 Agency Pro).** Since we resell GHL underneath, a GHL-savvy buyer sees us as "GHL at GHL's price, plus extras." Either price the software as *included with services* or justify the premium explicitly.

---

## 4. Who the code is built for

- **Agencies** — the strongest fit by engineering: cost/price separation that hides vendor cost from the end client, white-label vendor bidding, GHL sub-account provisioning, the Glide agency OS, partner payouts.
- **Local / SMB owners** — 52 SEO industry hubs (`gfunnel/src/data/industries.ts`): home services (HVAC, plumbing, roofing…), health (dental, chiro, med spa), professional services (legal, accounting, insurance, mortgage, real estate), coaches, restaurants, salons, gyms. Nine-department "BEAS" business score.
- **Individuals / creators / "connectors"** — free personal workspace, courses, communities, partner program.

Client work clusters in: **mortgage/real-estate lead gen, home-services contractors, insurance (Lead System vertical), energy/utility savings.**

---

## 5. Competitor map

There is no single competitor because we span categories. Grouped by the "shelf" a buyer would put us on:

### A. Same chassis — GHL and its white-label resellers (most dangerous)
| Competitor | Why they compete | Where we can win |
|---|---|---|
| **GoHighLevel** (direct) | It *is* our CRM layer, at the same $97/$297/$497 prices | Services + community + methodology on top; we do the work, GHL doesn't |
| **Thousands of GHL "SaaS mode" agencies** & vertical GHL SaaS (e.g. Agent CRM for insurance) | Same product, niche branding, often cheaper | Breadth of fulfillment + vendor network |
| **Extendly** | White-label GHL support, snapshots, fulfillment for GHL agencies | Broader service menu beyond GHL setup |

### B. White-label fulfillment + agency software (closest to our deepest code)
| Competitor | Notes |
|---|---|
| **DashClicks** | White-label fulfillment marketplace + agency software + client dashboard. Closest single analogue to Fulfillment + Workspace. |
| **Vendasta** | White-label platform + marketplace of 250+ resellable products; tiers roughly $99–$1,150+/mo plus wholesale. Enterprise-grade, complex. |
| **White-label service shops** (white-label SEO/PPC providers, e.g. Boostability-type vendors) | Single-service, cheaper per unit. |

### C. Productized "unlimited / subscription" services (competes with retainers & à-la-carte menu)
**Design Pickle, ManyPixels, Penji** (design), **Superside** (creative at scale), **Belay / Wing Assistant** (admin/VA), plus **Fiverr Pro / Upwork** (indirect: buy freelancers yourself).

### D. All-in-one SMB marketing software (competes for the $97–$497 software buyer)
**HubSpot Starter, Keap, Thryv, Podium, ClickFunnels, systeme.io, Kajabi.**

### E. Community / course platforms (competes for creators, coaches, partner community)
**Skool** (~$9 Hobby / $99 Pro), **Mighty Networks** (~$79–$354/mo), **Circle, Kajabi.**

### F. AI employees / agents
**Sintra, Lindy, Relevance AI**, and GHL's own Voice AI / Conversation AI (bundled in our own stack).

### G. Indirect / status quo
A local marketing agency on retainer · hiring an in-house marketer ($55–75k/yr) · DIY with Canva + ChatGPT + a cheap CRM · doing nothing.

**Where nobody else sits:** *services + software + business methodology (BEAS / Omni Process) + a partner economy, under one login.* That bundle is the differentiator — but only if we lead with one wedge and let the rest support it.

---

## 6. Recommendation: what to lead with

**Lead with the services. Bundle the software. Use partners as the channel.**

1. **Primary wedge — "Your marketing & ops department, with the software included."** Sell productized DFY services (start with Paid Ads + Funnel/Website + Automation/AI Employee, the three we have the most proof and tooling for) to **one** vertical cluster first. Best candidates by existing proof: **home services** (UpSmith work, 7 industry hubs) or **mortgage / real estate / insurance** (Glide/EMM, Lead System plan).
2. **Software as retention, not the headline.** Include the workspace (GHL sub-account + Sales Hub + Organizer + community) in every retainer. Stop selling $97/$297 standalone against GoHighLevel at identical prices.
3. **Agency track as second offer.** Our Fulfillment ledger + vendor bidding + white-label flag is genuinely agency-grade. Pitch: "White-label fulfillment for agencies — you keep the client and the margin." Competes with DashClicks/Vendasta/Extendly.
4. **Partner program as distribution**, once reseller billing and payouts actually run.

### Fix before spending on marketing
- [ ] **One price sheet.** Reconcile Free/Pro/Agency vs Single/Unlimited vs Starter/Growth/Pro vs Office/Business.
- [ ] **Run GHL sub-account auto-provisioning against the live agency** (code says it never has). Decide what happens on workspace deletion.
- [ ] **Charge, don't record.** Wire Stripe checkout into Fulfillment orders.
- [ ] **Remove claims the code can't back:** white-label custom domains/rebranding, MRR resale, VR, AI personas, reseller revenue share — until built.
- [ ] **Pick one codebase to sell from** (live PHP `platform` vs Next.js `gfunnel`), so the demo matches what's promised.
- [ ] **Security P0:** Supabase anon key hardcoded in `platform` source; CSRF items on the old roadmap.

---

## Sources (competitor pricing, third-party, verify before quoting publicly)
- GoHighLevel tiers: [getautomized.com](https://getautomized.com/gohighlevel-pricing/), [setsmart.io](https://setsmart.io/blog/gohighlevel-pricing), [ecosire.com](https://ecosire.com/blog/gohighlevel-pricing-worth-it-2026)
- Vendasta: [Capterra](https://www.capterra.com/p/168614/Vendasta-Platform/pricing), [G2](https://www.g2.com/products/vendasta-ai-platform/pricing), [SuiteDash comparison](https://suitedash.com/?p=63405)
- Skool / Mighty Networks: [schoolmaker.com](https://www.schoolmaker.com/blog/mighty-networks-pricing), [costbench.com](https://costbench.com/changelog/mighty-networks-plan-removed-2026-04/), [cartmango.com](https://cartmango.com/skool-vs-mighty-networks/)
