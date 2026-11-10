# GFunnel Homepage Spec: "The Entrepreneur's Social Operating System"

*2026-11-09. Based on the live page (gfunnel.com, screenshotted at 1440px), `platform/template/page_home.html`, `inc/gf_home_blocks.inc.php`, and the structural read in `gfunnel-codebase-analysis.md` §0.*

---

## 1. What the page says today vs. what GFunnel is

| | Today | What the architecture is |
|---|---|---|
| Category | "The Business Operating Hub" / "Funnel more than leads." (reads as a funnel builder) | **A social network where every profile is a business, with an operating system and an economy built in** |
| Hero action | AI prompt box → sign-up popup | The network's front door: search people, businesses, apps, communities |
| Social layer | Section 4 of 9 ("More than a workspace"), with mock avatars | The core of the product: profiles, feed, communities, messaging, Reels, events |
| Proof | Two real numbers (31,486 businesses, 5,000+ apps), one hard-coded "+12k members" | Real counts can be computed (`gfHomeHeroStats()` already exists) |
| Price | Not on the page | $97/mo, GoHighLevel and all apps included; free personal profile |

**Verdict:** the page sells a workspace and an AI builder. It never tells a visitor GFunnel is a *social* platform, which is the one thing no competitor has.

## 2. Fix before anything else (claims the code can't back)

| On the page | Problem | Fix |
|---|---|---|
| "Every VA and vendor is **verified** before it's listed" | Nothing in the code vets or verifies vendors (the vendor network explicitly has no verification) | Remove "verified". Say "Browse vendors" |
| "**+12k members**" (community visual) | Hard-coded in the mock-up, not measured | Replace with the real member count, or remove the number |
| "$50 first payout" | An earnings figure without an income disclosure (partner-network compliance risk) | Remove the figure |
| Trust bar: "GDPR Compliant · 99.9% Uptime · Unlimited seats" | Not measured anywhere in the code | Keep only what you can prove (SSL). Drop the rest until backed |
| "News is on the way" (empty) | An empty feed on the homepage says "not live yet" | Feed it from Articles/blog posts, or remove the column |
| Community feed shows posts from **July 2025** | 16 months old; reads as a dead network | Show the newest public posts; hide the section if there are none from the last 30 days |
| "Workspace" in 3 of 9 headlines | Repetitive, and "workspace" is the generic word every competitor uses | Use the category language below |

## 3. Recommended page, top to bottom

### 1. Hero: name the category, open the network
- **Eyebrow:** The Entrepreneur's Social Operating System
- **H1 (pick one to test):**
  - A. *Where entrepreneurs build, run and grow, together.*
  - B. *Your profile is your business.*
- **Subhead:** Connect with entrepreneurs, run every app your business uses (GoHighLevel included), and get the help to grow, all from one profile.
- **Primary action: a network search box** ("Search people, businesses, apps and communities…") that hits the existing directories. This puts the network first and is the cold-start loop: a visitor finds their business or app and claims it.
- **Primary CTA:** *Create your free profile* · **Secondary:** *Find & claim your business*
- Under the CTAs: *Free personal profile · $97/mo for your business, GoHighLevel included*
- Keep the AI prompt box, but move it to section 6.

### 2. Live network strip (proof it's alive)
Real counts only, computed on each render: **members · businesses · apps · communities · offers**. 31,486 businesses and 5,000+ apps are already real. Hide any count that is small rather than showing a weak number.

### 3. "Three layers. One profile." (what a Social OS is)
Three columns, each with a real screenshot:
| Social | Operating System | Economy |
|---|---|---|
| Profiles, feed, communities, messaging, Reels, events | Your apps (GoHighLevel included), Sales Hub, company records, projects, AI agents | Marketplace, partner network, done-for-you services, vendor bidding |

### 4. Start it · Run it · Scale it (the three audiences as one journey)
Replaces "For personal / business / agencies". Same three links (`/personal`, `/business`, `/agency`), reframed as the path the code already models:
- **Start it** (individuals): profile, community, courses, formation, your first offer.
- **Run it** (business owners): every app in one place, every department, a team to do the work.
- **Scale it** (agencies): a workspace per client, white-label fulfillment, your own GoHighLevel connected.

### 5. The network, live
A real feed preview: newest public posts, newest businesses, active communities, trending apps. Pull from the same sources as `/social` and the directories. This is what makes "social" believable. Never use mock-up avatars here.

### 6. Every app, one place, with help for each
App Directory visual (already built and good). Add: *bring your own app, or have one built*; each app has tutorials, help and a discussion. Move the AI prompt box here: *"Ask GFunnel to build it."*

### 7. Claim your page
Combine the Business Database and the app directory: *"Your business and your apps may already be here. Claim them."* Keep the claimable business cards (real, already built) and add claimable app cards.

### 8. Pricing teaser
- **Free:** personal profile, the network, communities.
- **$97/mo:** your business OS, GoHighLevel and every app included.
- **Done for you:** services from $497/mo.
Link to `/pricing`. Advertise $97 or more for anything that includes GoHighLevel (MAP policy, see analysis §3.1).

### 9. Get it done for you
Services and vendors: *"Do it yourself, hire a vendor, or have our team do it."* No "verified".

### 10. Earn with the network
Partner network: *"Share what you love: your products, ours, or other members'."* No earnings figures, no "passive income".

### 11. FAQ (also serves AI search)
- What is a social operating system?
- Is GoHighLevel included?
- Is it free?
- I run an agency. Can I connect my own GoHighLevel?
- How is GFunnel different from LinkedIn, Skool or GoHighLevel?

### 12. Final CTA
*Join the entrepreneurs building on GFunnel.* · **Create your free profile**

## 4. What to keep
- The visual design system (dark hero, light content, orange accent, Sora/DM Sans).
- The App Directory visual and the claimable business cards. Both are real data and on-message.
- The scroll-driven pillar section mechanics (re-point the panels to the three layers).
- The "day in the life" timeline (move it lower, or to `/business`).

## 5. SEO and metadata
- `<title>`: *GFunnel: The Entrepreneur's Social Operating System*
- Meta description: *The social network where your profile is your business. Connect with entrepreneurs, run every app (GoHighLevel included) and get help to grow. Free to join.*
- Options already exist: `gf_home_seo_title`, `gf_home_meta_description`. No code change needed.
- Add `Organization` + `FAQPage` schema.

## 6. Open decisions
- H1 option A or B (or test both).
- Whether to show member count now or wait until it's strong.
- Which industry the `/business` page leads with.

---

## 7. Reference: neilpatel.com (owner likes it) — what to borrow

**Why it works:**
1. **One free tool as the hero action.** "Enter your URL → Start my analysis." A visitor gets value in 10 seconds, and NP gets the lead.
2. **A founder's face**, repeated (hero, services tabs, contact form). People trust a person before a platform.
3. **Proof immediately after the hero:** press logos, a client-logo band, big result numbers, a testimonial.
4. **The page feels alive.** Six recent articles with authors, data studies, videos, the next live event. Most of the page is fresh content, which is authority and SEO at once.
5. **A clear DIY-or-DFY fork:** "Everything you need" (tools, services, thought leadership tabs), then "Would you rather hand it off to the experts?"
6. **One close:** "Let's talk about growing your business" + a short form.
7. **Design devices:** an announcement bar, dark hero, orange accent band, one underlined phrase per H2, white card grids. GFunnel's palette (dark + orange) is already compatible.

**GFunnel already has an equivalent for almost every block:**

| neilpatel.com block | GFunnel equivalent (exists in code) | Status |
|---|---|---|
| Announcement bar | Beta strip mechanism / any banner | Built |
| Hero: URL → free analysis | **Business search → "Claim your business + get your free business score"** (Business directory + BEAS detection) | Directory built; BEAS score built for workspaces, needs a public "preview" version |
| Founder face | Cameron Garlick (methodology author) | Needs photos |
| Press/client logos | None recorded | **Hold open. Never fake.** Ask clients (Rive Creative, Glide Media, KORR, UpSmith) for permission |
| Result numbers + testimonial | None measured | **Hold open.** Use real network counts instead (businesses, apps, members) until case studies exist |
| "Everything you need" tabs | Social · Operating System · Economy (the three layers) | Built |
| Blog grid | Articles + member blog posts (`/articles`) | Built; needs content |
| Data studies | — | Not built; later |
| Videos | Reels + videos modules | Built |
| Next live session | Events module (`bx_events`), live streaming | Built |
| Hand it off to experts | Fulfillment Center sectors: Get more customers · Build my business · Scale my operations | Built |
| Let's talk | `/contact-sales` | Built |

**The twist that makes it GFunnel, not a copy:** on Neil's page the content is *his*. On GFunnel's homepage the articles, videos, events and communities come **from the network's members**. The content blocks prove the "social" claim at the same time as they build authority.

**Do not copy:** his photos, wording, layout pixel-for-pixel, or any client logo/number we can't back.

## 8. Revised section order (Neil's skeleton, GFunnel's substance)

1. **Announcement bar:** e.g. *"New: claim your business page for free →"*
2. **Hero (dark, founder photo on the right):** eyebrow *The Entrepreneur's Social Operating System* · H1 *Your profile is your business.* · one input: *"Search your business name"* → **Find & claim it** (free) · under it: *Free profile · $97/mo for your business, GoHighLevel included.*
3. **Proof band (orange):** live counts (31,486 businesses · 5,000+ apps · members · communities). Client logos only once permitted.
4. **"Everything you need to <u>build, run and grow</u>":** three tabs (Social · Operating System · Economy) with screenshots and the founder.
5. **"From the <u>network</u>":** six newest articles/posts from members, with author avatars.
6. **"Watch and <u>learn</u>":** Reels/videos carousel + courses.
7. **"Join the next <u>live session</u>":** next event from the Events module.
8. **"Every app, <u>one place</u>":** App Directory visual + "bring your own or have one built".
9. **"Would you rather <u>hand it off</u>?":** three or four service cards from the Fulfillment sectors.
10. **Pricing teaser:** Free · $97/mo (GoHighLevel included) · Done for you from $497/mo.
11. **"Earn with the <u>network</u>":** partner program, compliant wording.
12. **"Let's talk about <u>growing your business</u>":** short form → `/contact-sales`, founder photo.
13. Footer with newsletter signup.

**Rule for every live block:** if there's no fresh content (nothing in the last 30 days), hide the block. An empty or stale block does more harm than no block.
