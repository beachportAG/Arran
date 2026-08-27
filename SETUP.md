# Arran Buys Homes — Setup Guide

Everything here is static HTML. No WordPress, no plugins, no monthly platform fee.

**Total running cost: the domain only.** Roughly $10 to $25 a year.

---

## What's in this folder

```
index.html              Homepage — seller landing page
projects/index.html     Before/after gallery (the differentiator)
about/index.html        Arran's story
agents/index.html       Partner page for real estate agents
wholesalers/index.html  Partner page for wholesalers
styles.css              Shared design system — edit once, all pages change
images/                 Where photos go (see images/README.txt)
404.html                Not-found page
robots.txt              Search engine instructions
sitemap.xml             Page list for Google
```

The agent and wholesaler pages are intentionally **not** in the main navigation. They're linked only from the footer, so Arran hands out `arranbuyshomes.com/agents` directly to brokerages without cluttering the seller experience.

---

## Contact info — already done

These are live across every page. No action needed.

| Item | Value |
|------|-------|
| Phone (displayed) | `(321) 604-8481` |
| Phone (`tel:` links) | `3216048481` |
| Email | `arranbuyshouses@gmail.com` |
| Location shown | Orlando, FL — **no street address anywhere** |

The structured data declares Orlando/FL as the locality with no street address, which is the correct pattern for a business that doesn't publish a physical location. Google accepts this.

## Also done

| Item | Value |
|------|-------|
| Domain | `arranbuyshomes.com` — live on GitHub Pages with HTTPS |
| Formspree endpoint | `https://formspree.io/f/mwlkebwg` (10 forms) |
| Spam honeypot | `_gotcha` hidden field on every form |

Nothing left to find-and-replace. The remaining work is photos and real project numbers.

> **Heads up on the name.** The email is `arranbuys**houses**@gmail.com` but the site is branded `Arran Buys **Homes**`. Pick one before buying the domain — mismatched brand and email costs you credibility on every lead. If he'd rather be "Arran Buys Houses," say the word and I'll swap it site-wide in one pass.

---

## Step 1 — Buy the domain

Any registrar works. They differ only on price.

- **Cloudflare Registrar** — ~$10/yr, sold at cost, no upsells. Cheapest.
- **Porkbun** — ~$11/yr, free WHOIS privacy.
- **GoDaddy** — ~$20 to $25/yr after the first-year promo. Fine, just pricier and heavy on upsells.

Make sure **WHOIS privacy** is on. Without it, Arran's name, address, phone, and email are published in a public database that gets scraped by spammers constantly. Cloudflare and Porkbun include it free. GoDaddy charges for it.

---

## Step 2 — Put the files on GitHub

1. Create a free account at [github.com](https://github.com).
2. Click **New repository**. Name it `arranbuyshomes`. Set it to **Public** (Pages requires public on the free plan). Don't add a README.
3. On the empty repo page, click **uploading an existing file**.
4. Drag in everything from this folder. Folders and all.
5. Click **Commit changes**.

### Turn on hosting

1. In the repo, go to **Settings → Pages**.
2. Under *Source*, pick **Deploy from a branch**.
3. Branch: `main`, folder: `/ (root)`. Click **Save**.
4. Wait 1 to 2 minutes, then reload the Settings → Pages screen. The live URL appears in a green banner at the top.

For the current repo (`beachportAG/Arran`) that URL is:

**https://beachportag.github.io/Arran/**

GitHub lowercases the username but preserves the repo name's capitalization, so the `/Arran/` part is case-sensitive.

> **All links are relative**, not root-relative. That means the site works identically at a GitHub subfolder URL, at a custom domain root, and when you just double-click `index.html` on your desktop. Don't change `href="styles.css"` to `href="/styles.css"` — that breaks the subfolder URL.

### Point the domain at it

Still in **Settings → Pages**, enter the domain under *Custom domain* and save. GitHub creates a `CNAME` file automatically.

Then at the registrar's DNS panel, add these five records:

| Type | Name | Value |
|------|------|-------|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `<username>.github.io` |

DNS takes anywhere from 10 minutes to a few hours. Once it resolves, go back to **Settings → Pages** and tick **Enforce HTTPS**. The certificate is free and auto-renews.

---

## Step 3 — Wire up the forms

Static hosting can't process a form on its own, so a free relay handles it.

1. Sign up at [formspree.io](https://formspree.io) — free tier is **50 submissions/month**.
2. Create a form. Point the notification email at Arran's inbox.
3. Copy the form ID from the endpoint (`https://formspree.io/f/**xyzabcd**`).
4. Replace all 9 instances of `YOUR_FORM_ID` with it.
5. **Submit a real test from your phone** before announcing the site. Confirm it lands in his inbox and isn't in spam.

All three audiences post to the same endpoint but tag themselves, so his inbox sorts cleanly:

- Sellers → subject `Cash Offer Request`
- Agents → subject `AGENT Submission`
- Wholesalers → subject `WHOLESALER Deal`

If he outgrows 50/month, [Web3Forms](https://web3forms.com) is free at 250/month and swaps in the same way.

---

## Step 4 — Add the photos

This is the part that makes the site actually work. The gallery is the whole credibility argument.

**Optimize first.** Phone photos are 4 to 8 MB each and will make the page crawl. Run them through [squoosh.app](https://squoosh.app): set *Resize* width to **1600**, format to **WebP** or **JPEG quality 75**. That gets each file under 300KB with no visible loss.

Name them to match what's already in the HTML:

```
images/hero.jpg                      wide exterior shot, 1920x1080
images/arran.jpg                     portrait of Arran, 600x740
images/projects/pine-hills-before.jpg
images/projects/pine-hills-after.jpg
images/projects/mount-dora.jpg       finished-only, no before shot
```

Then in each page, swap the placeholder `src="data:image/svg+xml..."` for the real path, e.g. `src="/images/projects/pine-hills-after.jpg"`.

**Before/after pairs must be shot from roughly the same spot at the same aspect ratio**, or the drag slider looks broken. Tell Arran this now so he starts shooting that way on the next job. Standing in the doorway of each room before demo takes ninety seconds and is worth a lot on this page.

To add photos later, Arran drags files into the GitHub web interface. No git, no command line.

---

## Step 5 — Google Business Profile

This matters more than the website for local search.

Register at [business.google.com](https://business.google.com) and choose **service-area business** when it asks about a storefront. Google then lets him list the cities he serves while keeping the address hidden from the public listing.

Google does require an address during verification, but with a service-area business it is used only to confirm he's real and is never displayed. That's how he stays consistent with the site, which shows Orlando, FL and nothing more specific.

If he later wants a mailing address that isn't his house, a virtual mailbox runs $10 to $30/month. Not necessary to launch.

---

## Editing later

- **Change a color, font, or spacing** → edit `styles.css` once. Every page updates.
- **Change wording on one page** → edit that page's `.html`.
- **Change the phone number** → find-and-replace across all files (both formats).
- **Add a project** → copy an existing `<article class="pj">` block in `projects/index.html` and swap the text and image paths.

Edits can be made right in GitHub's web editor (click any file, then the pencil icon). Changes go live about a minute after committing.

---

## Real content still needed from Arran

The copy is written and structurally complete, but these are placeholders standing in for facts only he has:

- **The stats on the projects page** — currently `40+ homes`, `14 avg days to close`, `6 counties`. Use his real numbers. If he's done 12 houses, say 12. An inflated number that a seller can sense is worse than a modest true one.
- **The six project write-ups** — the situations are realistic but invented. Replace them with actual deals, keeping addresses partial (`2*** Kinnon Dr`) the way the competitor does.
- **Whether "40+" and "14 days" are defensible** — if he ever advertises these, they should be true.

---

## Growing it later

The single highest-value addition is **city landing pages**: `/orlando/`, `/kissimmee/`, `/lakeland/`, `/sanford/`. That's the entire SEO strategy behind the competitor site you sent. Each one is this homepage with the city name swapped into the title, H1, and copy. Once the main site is live and converting, that's the next move.
