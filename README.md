# vps provider: How to Choose Without Overpaying — Real Entry Prices, IPv6-Only Gotchas and Renewal Traps Compared

Most people typing "vps provider" into a search bar already know what a VPS is. They want to know who deserves their money this month, what a usable server actually costs, and which fine print bites later. So here are the short answers up front. A shared-CPU cloud server starts at **$2.50/month at Vultr** (IPv6-only; $3.50 with an IPv4 address), DigitalOcean's entry Droplet is $4, and Hetzner's regular cloud line runs about €5.49 for 2 vCPU and 4 GB of RAM. The complication: this has been a rough year for hosting prices, so any comparison table you bookmarked a while ago is probably lying to you.

This guide walks through what actually changed, Vultr's full shared-CPU price ladder, the one detail about that $2.50 plan almost nobody explains, and how the usual suspects compare on the things that decide real-world cost: renewals, management, and what an entry spec can honestly handle.

> **In a hurry?** For a cheap server you control over SSH, Vultr's Cloud Compute line is the most direct route: **$2.50/mo** IPv6-only, **$3.50/mo** with IPv4 — 👉 [check Vultr's current plans and prices](https://www.vultr.com/pricing/?ref=7268283). If you'd rather have 4 GB of RAM plus a control panel at the entry tier, Hostinger's KVM plan (~$6.49 intro) is built for that. If you want nothing to do with server admin at all, ScalaHosting's managed plans start at $14.95/mo.

## What changed about VPS pricing this year

Answer first: budget 20–40% more than older comparison tables told you, and put extra weight on providers whose prices don't jump between year one and year two.

Two things moved the market. The first is hardware. DRAM and NAND flash prices climbed sharply as AI infrastructure absorbed the supply, and smaller European hosts felt it first because they buy the same chips without the purchasing leverage of the hyperscalers. The clearest example is Hetzner, long the price floor of the whole market: it raised cloud server prices on June 15, 2026, with its US CPX11 plan going from €5.99 to €17.49 per month and the CCX13 dedicated-vCPU plan from €15.99 to €42.99. Some US plans nearly tripled.

The second change is billing granularity. DigitalOcean moved CPU Droplets to per-second billing on January 1, 2026, with a sixty-second minimum and a monthly cap. For short-lived test boxes and CI runners, that quietly changed the math in your favor.

The blunt version: the era of the €3.79 production server is over. When you compare providers below, treat price stability as a feature, because two of the traditional cheap picks repriced this year.

## Vultr's plans and prices: the full shared-CPU ladder

The line most people should look at is **Cloud Compute – Regular Performance**: shared CPU, monthly pricing, and sizes that step up gently instead of doubling your bill. Here is the current ladder:

| Size | Monthly price | vCPU / RAM | Storage | Transfer | Buy |
| --- | --- | --- | --- | --- | --- |
| IPv6-only starter | $2.50 | 1 vCPU / 512 MB | 10 GB SSD | 0.5 TB | [ Get the $2.50 plan](https://www.vultr.com/pricing/?ref=7268283) |
| IPv4 starter | $3.50 | 1 vCPU / 512 MB | 10 GB SSD | 0.5 TB | [ Get the $3.50 plan](https://www.vultr.com/pricing/?ref=7268283) |
| 1 GB | $5 | 1 vCPU / 1 GB | 25 GB SSD | 1 TB | [ Get the $5 plan](https://www.vultr.com/pricing/?ref=7268283) |
| 2 GB | $10 | 1 vCPU / 2 GB | 55 GB SSD | 2 TB | [ Get the $10 plan](https://www.vultr.com/pricing/?ref=7268283) |
| 4 GB | $20 | 2 vCPU / 4 GB | 80 GB SSD | 3 TB | [ Get the $20 plan](https://www.vultr.com/pricing/?ref=7268283) |
| 8 GB | $40 | 2 vCPU / 8 GB | 160 GB SSD | 4 TB | [ Get the $40 plan](https://www.vultr.com/pricing/?ref=7268283) |
| 16 GB | $80 | 4 vCPU / 16 GB | 320 GB SSD | 5 TB | [ Get the $80 plan](https://www.vultr.com/pricing/?ref=7268283) |
| 32 GB | $160 | 8 vCPU / 32 GB | 640 GB SSD | 6 TB | [ Get the $160 plan](https://www.vultr.com/pricing/?ref=7268283) |
| 64 GB | $320 | 16 vCPU / 64 GB | 1280 GB SSD | 7 TB | [ Get the $320 plan](https://www.vultr.com/pricing/?ref=7268283) |

Two notes on that table. The $2.50 and $3.50 rows are the same hardware; the only difference is the IPv4 address. And the pricing page shows no intro-versus-renewal split on these shared-CPU plans — the listed number is the ongoing rate, which is not how every VPS brand structures its headlines.

If shared CPU isn't enough, the same platform carries other lines:

- **High Performance (AMD / Intel)** — the same size ladder on newer hardware with NVMe storage, priced above the Regular line
- **Optimized Cloud Compute** — dedicated vCPUs in General Purpose, CPU-Optimized, Memory-Optimized and Storage-Optimized flavors, for workloads that need sustained CPU rather than bursty shared capacity
- **Cloud GPU and Bare Metal** — for inference workloads and fully physical servers

Deploying one takes about a minute in the current panel: Products → Compute → Deploy → Shared CPU, pick a region and size, choose an OS or application image under Configure Software, then hit Deploy.

## The $2.50 tier is IPv6-only. Read this before ordering.

The cheapest Vultr plan has no IPv4 address, so it's reachable over IPv6 only. Most comparison tables print "$2.50" and move on, which is how people end up with a server they can't SSH into from their own laptop.

Here's what IPv6-only means in practice. If your home or office network hands out IPv4 addresses only — still very common on fixed-line connections — you won't reach the box directly. You'd need to hop through something dual-stack (another server, a tunnel, a jump host) to administer it. Hosting a public site works only for visitors on IPv6-capable networks, which describes most mobile carriers but far from all broadband.

Who the $2.50 tier actually suits: backend services talking to other IPv6-reachable servers, throwaway test boxes you access through a tunnel, and anyone experimenting. For almost everyone else, the **$3.50 tier**, which is identical hardware plus an IPv4 address, is the real entry point. One dollar a month is cheap insurance against an evening of network debugging.

👉 [See Vultr's $2.50 and $3.50 entry tiers](https://www.vultr.com/products/cloud-compute/?ref=7268283)

## How Vultr compares with the other usual suspects

On raw entry price Vultr sits at or near the floor. On RAM per dollar at the entry tier, it doesn't, and that's the number some competitors engineer their headlines around. Printed entry prices aren't comparable until you look at specs:

| Provider | Entry price | What entry actually includes | Known for | Watch out for |
| --- | --- | --- | --- | --- |
| Vultr | $2.50/mo | 1 vCPU, 512 MB, 10 GB SSD, IPv6 only | Region spread, small price steps | IPv6-only entry; IPv4 costs $1 more |
| DigitalOcean | $4/mo | 1 vCPU, 512 MB, 10 GB SSD | Docs, API, per-second billing since Jan 1 | Powering off doesn't stop billing; backups cost extra |
| Hetzner Cloud | from ~€5.49/mo | 2 vCPU, 4 GB, 40 GB NVMe | Price-to-performance in Europe | US prices jumped June 15 — CPX11 now €17.49 |
| Hostinger | ~$6.49/mo intro | 1 vCPU, 4 GB, 50 GB NVMe | Most RAM per dollar at entry, panel included | Renewal runs higher than the intro rate |
| Akamai Cloud (Linode) | ~$5/mo | 1 vCPU, 1 GB (Nanode) | Multi-region footprint, flat renewal pricing | Entry spec is modest for the price |
| OVHcloud | $4.54/mo | 2 vCPU, 4 GB, daily backup | Included traffic and DDoS protection | — |
| IONOS | $2/mo first 3 months | 1 vCore, 2 GB, 60 GB NVMe | Aggressive teaser pricing | $6/mo after the promo, on a 1-year term |
| Contabo | from ~€5.50/mo | High-resource budget configs | Raw resources per euro | Entry price shown as a 24-month effective rate |
| Kamatera | from $4/mo | Fully custom configurations | Pick exact cores and RAM | — |

Read that table by matching rows, not columns. Vultr's $2.50 entry is a 512 MB box. Hostinger's $6.49 entry is a 4 GB box. Hetzner's ~€5.49 regular plan is also 4 GB. "Cheapest" means nothing until the RAM column lines up.

Pricing structure matters as much as the numbers. Vultr lists one ongoing rate on these plans. Hostinger and IONOS both lead with teaser rates that step up later (Hostinger's KVM 1 renews higher than its $6.49 intro; IONOS's VPS S+ goes from $2 to $6 after three months, tied to a one-year term). Akamai is positioned explicitly around never seeing a renewal increase. Which structure suits you depends on lifespan: for a three-month project the teasers are genuinely cheap, but for a server that will still exist next year, the flat price wins.

## Managed or unmanaged: the bill nobody puts in the table

Vultr hands you a root password and walks away, which makes it an unmanaged provider. Same for DigitalOcean, Hetzner, OVHcloud, Contabo and Kamatera. That's fine if you live in a terminal; it's a hidden tax if you don't.

The market splits three ways:

| Type | What you handle | Typical cost |
| --- | --- | --- |
| Unmanaged VPS | OS updates, web server, backups, security, uptime | $4–15/mo |
| Self-managed with a panel | Site setup and updates through a GUI | $6–30/mo |
| Fully managed | Your code, that's about it | $30–100+/mo |

Here's the comparison almost every review skips: a $5 unmanaged server isn't cheaper than a $35 managed one if server admin eats six hours of your month. Price your own hours honestly before picking "cheap."

If you land on managed, the reference points are ScalaHosting at $14.95/mo (SPanel and SShield security included rather than billed separately), Cloudways from $11/mo, and Liquid Web, which runs around $4.25/mo self-managed with optional management add-ons and phone support. Vultr deliberately doesn't play in that space; its value is the raw server at a low, stable price.

## Who a Vultr server fits — and who should look elsewhere

Vultr is the right pick when region choice and small price steps matter more than hand-holding. Its shared-CPU Cloud Compute instances suit bursty websites, CMS installs, test environments and small databases, and the location list is broad enough that "deploy close to your users" is a realistic instruction rather than marketing copy. The ladder also steps gently ($2.50, $3.50, $5, $10), so going from a test box to a production instance doesn't force you to double the bill.

It's the wrong pick in three cases. If you want 4 GB of RAM and a beginner-friendly panel at entry level, Hostinger's KVM plan delivers more hardware for a couple of dollars more. If most of your audience is in Europe and you're comfortable with Linux, Hetzner's regular line gives you 4 GB for about €5.49, though you should re-check current numbers given the June increases. And if you genuinely want a managed server, Vultr isn't offering one; ScalaHosting or Liquid Web fit better.

One practical check for any provider: if you specifically need a Windows image, confirm it's available for the exact plan before ordering, because image support varies by product line.

👉 [Browse Vultr's deployment locations](https://www.vultr.com/locations/?ref=7268283)

## Quick answers before you order

### Is the $2.50 plan enough for a real website?

For a lightweight static site or a small personal app, yes. It's a full Linux server, just a small one. For a CMS with a database doing real traffic, the $5 tier (1 GB) is the realistic floor, and the 4 GB tier at $20 is where small production sites stop thinking about memory.

### Do I keep paying if I just shut the server down?

On DigitalOcean, explicitly yes: after the per-second billing change, a powered-off Droplet still bills because the resources stay reserved until you destroy it. Paying for reserved capacity is standard across cloud providers, so the safe habit everywhere is to destroy test servers when you're done instead of just stopping them.

### Why did Hetzner get expensive all of a sudden?

Memory and flash costs rose through the first half of the year as AI infrastructure absorbed supply, and Hetzner passed that on with its June 15 price adjustment. US plans took the worst of it: CPX11 went from €5.99 to €17.49, CCX13 from €15.99 to €42.99. European locations were hit far less, which is worth knowing before you write the whole provider off.

### Do these entry plans include backups?

Not uniformly. DigitalOcean charges extra (percentage-based options run 20% weekly or 30% daily of the server cost; usage-based ones start at $0.01 per GiB-month). OVHcloud's VPS-1 includes daily backups. Check where backups sit in the pricing before comparing headline numbers, because a $4 server with paid backups can end up costing more than a $5 one with them included.

## A ten-second decision guide

- Cheapest possible test box, and you're comfortable over IPv6 → Vultr's $2.50 tier. Add a dollar for IPv4 and it becomes reachable from anywhere — 👉 [create a Vultr account and deploy your first instance](https://www.vultr.com/register/?ref=7268283)
- Entry tier with 4 GB and a panel → Hostinger's KVM plan (~$6.49 intro, higher renewal)
- European audience, comfortable in a terminal → Hetzner's regular cloud line, 4 GB at ~€5.49
- Zero sysadmin work → ScalaHosting ($14.95, managed) or Liquid Web

Before clicking buy on any of them, check two things: whether the region list actually covers where your users are, and whether the price on screen is an intro rate or the ongoing one. The second number is the only one that matters after month twelve.
