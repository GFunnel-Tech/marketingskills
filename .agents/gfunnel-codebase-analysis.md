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
| CRM, funnels, phone, SMS, email, calendars, Voice/Conversation AI, invoices | **GoHighLevel / LeadConnector** (agency OAuth, auto sub-accounts on SaaS plan, snapshots, Sales Hub push, platform CRM) | GHL is **one of the apps inside a GFunnel workspace**, not the product itself. Message it that way ("GoHighLevel is included in your workspace"), never "GFunnel is GHL". |
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

✅ **The software offer (owner-confirmed): $97/mo = the GFunnel workspace with GoHighLevel AND every other app included.** This turns the price match into the headline: GoHighLevel's own entry plan is $97/mo by itself (Starter, third-party sources). With GFunnel, the same $97 includes GHL **plus** the App Hub, Sales Hub, Organizer, Projects, community, courses and AI agents. Lead with it: *"Everything your business runs on, GoHighLevel included, for $97 a month."*
- Make $97 the ONE software price everywhere. Today the code shows Single $97 / Unlimited $297 / Free/Pro/Agency / Office/Business. Collapse these so the $97 story isn't diluted. $297 Unlimited can stay as the multi-workspace (agency) tier.
- Before quoting it, confirm what GHL plan each $97 workspace actually gets. The code provisions sub-accounts on a **$0 "free SaaS plan" with GHL-enforced limits** (`prod_VZJVwqZgreS4d2`), so the copy must not promise full GHL Starter features unless the plan is changed. **[CONFIRM]**

---

### 3.1 GoHighLevel's Minimum Advertised Price (MAP) policy: bundling does NOT remove it

The goal was to bundle GHL inside GFunnel so the $97 MAP floor stops applying. HighLevel's own MAP FAQ (Aug 2024) addresses bundles directly:
- **"The entire bundle that includes access to our Core Platform must be priced at or above $97."**
- "Core Platform" means **any 2+ of**: funnel/website builder, forms, surveys, CRM, email builder, calendar, automation workflows.
- Offering a standalone feature below $97 is prohibited "if you are bundling the standalone product with other 'free' platform features."

What IS allowed:
- **A single GHL feature sold as a true standalone product** (e.g. CRM only, or calendar only) is outside MAP.
- **Charging less than $97 privately.** MAP covers advertised prices only. A lower actual price is allowed if it "is not offered publicly and cannot be discovered through publicly-available or searchable forums": an add-to-cart reveal, private checkout codes, or sales-call pricing.
- In the EU/UK, discounts may be communicated.

Enforcement: HighLevel may "suspend or terminate your ability to resell access." GFunnel provisions every workspace as a GHL sub-account, so that is an **existential** risk, not a fine. HighLevel says it is currently not granting MAP exceptions.

Code-level risks to review:
1. **Every personal profile gets a free GHL sub-account** on a $0 SaaS plan (`gf_ghl_personal`, default on) while the site says "everything personal is free." If that free plan exposes 2+ Core Platform features and is publicly advertised as free, it is the clearest MAP exposure on the platform. **[CHECK the $0 plan's feature set]**
2. **Public $97 software price is compliant.** Do not publish anything lower (no "$1 for 90 days" on a public page; that offer exists in `security-spark-ads`).
3. Lower prices must stay behind add-to-cart, private codes or sales calls.

*Not legal advice. Get HighLevel's written confirmation or a lawyer's read of the current ToS before launching any sub-$97 GHL offer. The FAQ and the June 2026 ToS may differ on the exact floor.* Sources: [HighLevel MAP FAQ](https://help.gohighlevel.com/support/solutions/articles/155000003083-minimum-advertised-pricing-policy-map-policy-faqs-august-2024), [HighLevel ToS](https://www.gohighlevel.com/terms-of-service).

## 4. Who the code is built for

- **Agencies** — the strongest fit by engineering: cost/price separation that hides vendor cost from the end client, white-label vendor bidding, GHL sub-account provisioning, the Glide agency OS, partner payouts.
- **Local / SMB owners** — 52 SEO industry hubs (`gfunnel/src/data/industries.ts`): home services (HVAC, plumbing, roofing…), health (dental, chiro, med spa), professional services (legal, accounting, insurance, mortgage, real estate), coaches, restaurants, salons, gyms. Nine-department "BEAS" business score.
- **Individuals / creators / "connectors"** — free personal workspace, courses, communities, partner program.

Client work clusters in: **mortgage/real-estate lead gen, home-services contractors, insurance (Lead System vertical), energy/utility savings.**

---

## 5. Competitor map

**Positioning note:** GoHighLevel is **not a competitor — it is one of the apps you access inside GFunnel.** The code agrees: GHL is provisioned per workspace and deep-linked from the App Hub alongside Google Drive, diagrams.net and the rest. GFunnel is the layer above the apps — the workspace, the methodology, the services and the people who do the work.

### A. Competitors by offer (buyers compare per offer, not per company)

A competitor is whatever the buyer would otherwise buy for the same job. GFunnel sells four things, so it has four competitor sets. The one that matters is set by **which offer leads**.

| Offer (from code) | Buyer | Who they'd otherwise buy | Most dangerous |
|---|---|---|---|
| **$97/mo software** (workspace, GHL and all apps included) | SMB owner | GHL "SaaS-mode" resellers (thousands, often $97–$297 with GHL under their own brand) · **Thryv** (SMB software + marketing services) · HubSpot Starter, Keap, systeme.io | **GHL SaaS resellers**: same engine, same price, niche branding |
| **DFY retainers** ($1,497–$3,997/mo hour blocks + à-la-carte menu) | SMB owner | **Marketing 360** (platform + "your marketing executive") · **Thryv / Hibu / Scorpion** (local-SMB marketing services) · local agencies · delegation services (**Magic, Belay, Wing**) | **Marketing 360** for marketing work; **Magic/Belay** for the hours-across-9-departments model |
| **White-label fulfillment for agencies** (cost/price ledger, vendor bidding) | Agency owner | **DashClicks** · **Vendasta** · Extendly · white-label SEO/PPC shops · Upwork/Fiverr (for the bidding side) | **DashClicks**: closest product shape |
| **Community / partner / courses** | Creators, would-be resellers | Skool, Mighty Networks, Kajabi · GHL's own affiliate program | **Skool** |

DashClicks and Vendasta compete only on the agency track. Marketing 360 competes only on the DFY retainer. Whether either is "main" depends on whether GFunnel leads with agencies or SMBs. **[DECIDE THE WEDGE]**

**What this means for messaging:** every serious competitor above sells either software OR marketing services, or both for marketing only. GFunnel's genuine differences, as backed by code:
1. **Whole business, not just marketing.** Nine departments, the Organizer (formation, compliance), Projects, Sales Hub, time tracking/invoicing — Marketing 360 and DashClicks stop at marketing.
2. **A diagnostic before a sale.** BEAS / the business assessment tells the owner what to fix first; none of the three leads with a methodology.
3. **Open, low entry price.** $97/mo software with GoHighLevel and every other app included, then published service tiers ($497 → $3,997/mo). Compare DashClicks (~$199/mo software), Vendasta (platform plus wholesale per product) and Marketing 360 (quote-only, services billed separately).
4. **Agency + SMB on one platform**, with a partner program as a sales channel (DashClicks/Vendasta are agency-first; Marketing 360 is SMB-direct only).

### B. Adjacent — same job, different shape
| Competitor | Notes |
|---|---|
| **GHL "SaaS mode" agencies / vertical GHL SaaS** (e.g. Agent CRM) | Sell GHL under their own brand. They compete for the same SMB wallet, but they are a **software** pitch; we are a **software + team** pitch. |
| **Extendly** | White-label GHL support/fulfillment for GHL agencies — overlaps our agency track only. |
| **White-label service shops** (white-label SEO/PPC providers) | Single-service, cheaper per unit; potential **vendors** in our network as much as competitors. |

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

**Where nobody else sits:** DashClicks, Vendasta and Marketing 360 all sell software + done-for-you *marketing*. GFunnel's gap in the market is *the whole business*: services + an app workspace (GoHighLevel included) + a business methodology (BEAS / Omni Process) + a partner economy, under one login. That bundle is the differentiator, but only if we lead with one wedge and let the rest support it.

---

## 6. Recommendation: what to lead with

**Lead with the services. Bundle the software. Use partners as the channel.**

1. **Primary wedge — "Your marketing & ops department, with the software included."** Sell productized DFY services (start with Paid Ads + Funnel/Website + Automation/AI Employee, the three we have the most proof and tooling for) to **one** vertical cluster first. Best candidates by existing proof: **home services** (UpSmith work, 7 industry hubs) or **mortgage / real estate / insurance** (Glide/EMM, Lead System plan).
2. **Software: one $97/mo plan with GoHighLevel and all apps included.** It's the low-friction entry offer and also comes bundled in every service retainer. GoHighLevel is shown as an included app, never as the thing being sold.
3. **Agency track as second offer.** Our Fulfillment ledger + vendor bidding + white-label flag is genuinely agency-grade. Pitch: "White-label fulfillment for agencies — you keep the client and the margin." Competes head-on with DashClicks and Vendasta.
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
- DashClicks: [Prospeo](https://prospeo.io/s/dashclicks-pricing-reviews-pros-and-cons), [Capterra](https://www.capterra.co.uk/reviews/179692/dashclicks), [getpulsesignal](https://getpulsesignal.com/pricing/dashclicks)
- Marketing 360: [Hackceleration](https://www.hackceleration.com/labs/marketing-360-pricing), [Capterra](https://www.capterra.com/p/148516/Marketing-360/pricing/), [Social Champ](https://www.socialchamp.com/blog/marketing-360-pricing/)
- GoHighLevel tiers: [getautomized.com](https://getautomized.com/gohighlevel-pricing/), [setsmart.io](https://setsmart.io/blog/gohighlevel-pricing), [ecosire.com](https://ecosire.com/blog/gohighlevel-pricing-worth-it-2026)
- Vendasta: [Capterra](https://www.capterra.com/p/168614/Vendasta-Platform/pricing), [G2](https://www.g2.com/products/vendasta-ai-platform/pricing), [SuiteDash comparison](https://suitedash.com/?p=63405)
- Skool / Mighty Networks: [schoolmaker.com](https://www.schoolmaker.com/blog/mighty-networks-pricing), [costbench.com](https://costbench.com/changelog/mighty-networks-plan-removed-2026-04/), [cartmango.com](https://cartmango.com/skool-vs-mighty-networks/)
