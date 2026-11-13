# Cheap NVMe VPS: How Low the Prices Go, Which Plan Your Workload Needs, and What the Sticker Price Leaves Out (JustHost Plans Compared)

Cheap NVMe VPS hosting currently starts at roughly $3 to $6 a month from established providers. Arct Cloud lists $3.89/mo for 1 vCPU, 1 GB RAM and 15 GB NVMe; OVHcloud starts at $4.54/mo for 2 vCores, 4 GB and 40 GB; BuyVPS prices its shared-CPU Standard tier from $5.94/mo. JustHost goes lower still: its VPS Promo plan is $1.99/mo for 1 core, 512 MB RAM and 5 GB NVMe, and the first genuinely usable tier, Sirius, is $4.85/mo.

The tier you pick matters more than the logo on the invoice. Published benchmarks put entry-level boxes around 16,000–20,000 random 4K IOPS, while a fixed-core plan on the same NVMe technology clears 120,000. Below: what each JustHost plan actually contains, where the IOPS ceiling sits, which workloads gain from NVMe and which are wasting money on it, and the four numbers that change the real monthly cost.

## Quick pick

> **A single small site, a bot, a VPN endpoint, a staging box:** JustHost **Sirius** — 1 core, 1 GB RAM, 20 GB NVMe, 300 Mbps fair-share port — at **$4.85/mo**, or **$3.88/mo** when you pay for 12 months. It costs a dollar more than New Star and doubles the disk while tripling the port speed.
> **Postgres/MySQL, Docker, a CI runner, anything with a search index:** **Vega** — 2 cores, 4 GB RAM, 80 GB NVMe, 500 Mbps — at **$13.44/mo**, **$10.75/mo** annual.
> 👉 [See the Sirius plan and its current price](https://justhost.asia/en/services/vps/tariffs/sirius?ref=196392)

## All JustHost NVMe plans on the tariff page

Prices are as displayed on JustHost's full tariff page. The 12-month column is the discounted rate the page shows when you commit to a year; three of the promotional tiers require a minimum three-month order to qualify.

| Plan | vCPU / RAM / NVMe | Port (fair-share) | Monthly | 12-month | Order |
| --- | --- | --- | --- | --- | --- |
| VPS Promo | 1 core / 512 MB / 5 GB | 10 Mbps (~4 TB) | $1.99 | — | [Promo](https://justhost.asia/en/services/vps/tariffs/promo-c1r512nvme?ref=196392) |
| New Star | 1 core / 1 GB / 10 GB | 100 Mbps (~31 TB) | $3.81 | $3.05 | [New Star](https://justhost.asia/en/services/vps/tariffs/new-star-c1r1024nvme?ref=196392) |
| Sirius | 1 core / 1 GB / 20 GB | 300 Mbps (~93 TB) | $4.85 | $3.88 | [Sirius](https://justhost.asia/en/services/vps/tariffs/sirius?ref=196392) |
| Arcturus | 1 core / 2 GB / 30 GB | 300 Mbps (~93 TB) | $6.92 | $5.53 | [Arcturus](https://justhost.asia/en/services/vps/tariffs/arcturus?ref=196392) |
| Double Star | 2 cores / 2 GB / 20 GB | 200 Mbps (~62 TB) | $7.08 | $5.67 | [Double Star](https://justhost.asia/en/services/vps/tariffs/double-star-c2r2048nvme?ref=196392) |
| Alpha Centauri | 2 cores / 2 GB / 40 GB | 400 Mbps (~124 TB) | $8.99 | $7.19 | [Alpha Centauri](https://justhost.asia/en/services/vps/tariffs/alpha_centauri?ref=196392) |
| Bright Star | 4 cores / 4 GB / 30 GB | 300 Mbps (~93 TB) | $9.80 | $7.84 | [Bright Star](https://justhost.asia/en/services/vps/tariffs/bright-star-c4r4096nvme?ref=196392) |
| Vega | 2 cores / 4 GB / 80 GB | 500 Mbps (~155 TB) | $13.44 | $10.75 | [Vega](https://justhost.asia/en/services/vps/tariffs/vega?ref=196392) |
| Capella | 4 cores / 4 GB / 120 GB | 750 Mbps (~232 TB) | $18.30 | $14.64 | [Capella](https://justhost.asia/en/services/vps/tariffs/capella?ref=196392) |

Two things the table does not show. Larger configurations exist above Capella — 8 GB RAM with 200 GB NVMe, then 12 GB and 24 GB tiers — on the same structure and with the same storage type. And JustHost's VPS landing page currently advertises "Special" versions of several of the same plans at noticeably lower headline rates: Sirius at $2.81/mo ($2.25/mo annual) against $4.85 on the tariff page, Arcturus at $4.01 against $6.92, Vega at $7.79 against $13.44. The configurations are identical. Which SKU you land on depends on the page you entered from, so read the plan name and the total on the checkout screen rather than the banner price.

Every plan is KVM, ships with one IPv4 and one IPv6 address, and sits behind DDoS filtering. Payment options include cards, PayPal, Alipay, UnionPay and several cryptocurrencies.

## Where the speed comes from, and where it stops

NVMe talks to the CPU over PCIe instead of the SATA bus. SATA III caps out around 550–600 MB/s and a spinning disk around 160 MB/s, while an NVMe drive can push multiple GB/s and handle far more small random reads per second. That is a statement about the interface, not about your server. Arct Cloud says so on its own page: those figures "compare storage interfaces; they are not VPS performance guarantees."

The gap between the marketing number and the delivered number is the thing worth understanding before you buy. BuyVPS publishes fio results for its 4-core EPYC Genoa plan with 8 GB RAM and NVMe RAID10, run at queue depth 32 with direct I/O and a 4K block size, median of five passes: **122,959 IOPS for 4K random reads**, **87,730 for 4K random writes**, and **693.84 MB/s on a 50/50 mixed 4K load**. The same vendor states that an NVMe drive can exceed 500,000 IOPS on its own, and that "the IOPS ceiling for each VPS is set by the plan and vCPU count" — lower tiers sit under a lower ceiling. Both statements are true at once: 500k is a whole drive, 120k is what one virtual machine was allocated.

Third-party benchmarks of JustHost's own boxes land further down the scale. Tests published for a Hong Kong VPS on E5-2690 v4 hardware recorded 4K read/write around 78 MB/s, roughly 19.6K IOPS, with sequential I/O near 460 MB/s. A UAE (Fujairah) box on Xeon Gold 6148 measured about 64 MB/s on the same 4K test, around 16.1K IOPS, with 603 MB/s sequential. Those are single test sets on entry-level configurations, not a verdict on the whole range, but they set a realistic expectation: an inexpensive 1-core VPS delivers tens of thousands of random IOPS, not hundreds of thousands.

That is still a large jump over SATA for the right workload, because the workloads that care about NVMe are the ones doing many small random reads:

- **OLTP databases** — PostgreSQL, MySQL, MariaDB, where index lookups hit disk constantly.
- **Document stores and search** — MongoDB, Elasticsearch, OpenSearch, Meilisearch.
- **Build and CI pipelines** — `git clone`, `npm install`, `pip install`, `cargo build` all spend their time on filesystem metadata and small reads.
- **Container hosts** — pulling and unpacking image layers under Docker or k3s.
- **Busy web apps with sessions, logs and caching that spill to disk.**

If your plan is to run one of those on a 1-core, 1 GB box, the ceiling in the benchmarks above is what you will hit. 👉 [Compare the tiers that raise the IOPS ceiling](https://justhost.asia/en/services/vps/tariffs-all?ref=196392)

## Who should not pay for NVMe

Plenty of buyers searching for a cheap NVMe VPS do not need NVMe. A static site served from a CDN, a low-traffic blog with page caching, a WireGuard endpoint, a cron-job box — these touch storage so rarely that a SATA SSD would perform identically. Arct Cloud makes the same point from the other direction: CPU-bound applications may benefit more from a faster processor tier than from faster storage. If your workload is compiling code, transcoding video or running a game server tick loop, spend the money on cores, not on a bigger disk.

The tier logic on JustHost's own ladder follows this. Bright Star gives you 4 cores for $9.80 but only 30 GB of disk; Vega gives you 2 cores for $13.44 with 80 GB. A build server wants Bright Star. A database wants Vega. Paying for both at once means jumping to Capella at $18.30.

## The four numbers that decide the real monthly cost

**1. The billing term sets the unit price.** Every discounted rate in the table above is contingent on paying for 12 months. New Star, Double Star and Bright Star additionally require a three-month minimum order before the discount applies at all. Monthly billing on Sirius is $4.85; annual is $3.88. That is a 20% difference in exchange for prepaying a year.

**2. Which page you land on sets the headline price.** As noted, JustHost currently shows two price levels for the same configurations depending on whether you arrive via the tariff list or the VPS landing page. Neither is fake, but only one will appear on your invoice. Confirm the plan name at checkout.

**3. The port is the traffic allowance.** JustHost sells "unmetered" ports at a stated speed on a fair-share basis, and converts that into a monthly TB figure. The arithmetic is transparent: a 10 Mbps port running at capacity moves about 3.2 TB in 30 days, and JustHost's own numbers (100 Mbps → 31 TB, 300 Mbps → 93 TB) assume roughly 90% efficiency. The Promo plan's "4+ TB" is not a bucket you can exceed by burst; it is the width of the pipe, and 10 Mbps is narrow enough that a single large backup or a video pull will saturate it for hours. If outbound throughput matters, the 100 Mbps floor on New Star is the practical minimum.

**4. Datacenter location changes what you get for the same money, elsewhere in the market.** This one is worth watching across providers rather than within JustHost. OVHcloud sells "unlimited traffic" on its VPS range but excludes the Asia-Pacific region in a footnote: Mumbai, Singapore and Sydney carry monthly quotas of 500 GB on VPS-1, 1 TB on VPS-2 and VPS-3, and 3 TB on VPS-4, after which bandwidth is throttled to 10 Mbps. Exabytes in Singapore goes further — its advertised rates are for the lowest available billing cycle, which is a three-year term, the promotional price applies to new registrations only with renewals reverting to list price, and the "3-minute deployment" covers the base OS without control panel, antivirus, DDoS protection or backup.

## How JustHost compares on paper

| Provider | Entry NVMe configuration | Entry price | Worth knowing |
| --- | --- | --- | --- |
| JustHost | 1 core / 512 MB / 5 GB, 10 Mbps | $1.99/mo | First usable tier is $4.85 (1 GB / 20 GB / 300 Mbps) |
| Arct Cloud | 1 vCPU / 1 GB / 15 GB | $3.89/mo | Every plan NVMe; Linux images under 30 seconds |
| OVHcloud | 2 vCores / 4 GB / 40 GB | from $4.54/mo | Daily backup of previous 24h; APAC traffic quotas |
| BuyVPS | Shared 1:4 vCPU, Standard tier | from $5.94/mo | Publishes fio medians; NVMe RAID10 on all tiers |
| WhaleVPS (Finland) | 2 cores / 4 GB / 40 GB, 20 TB | $19.00/mo | Unmanaged, dedicated CPU/RAM allocation |
| Exabytes (Singapore) | NVMe tiers from C2 upward | SGD pricing, three-year term | Promo rates for new signups only; 80/20 local/international bandwidth split |

Read the JustHost row against the others carefully. It wins on the entry price and loses on the entry configuration — 512 MB and a 10 Mbps port is a different product from OVHcloud's 4 GB and 40 GB, and the comparison only becomes fair at Sirius ($4.85, 1 GB / 20 GB / 300 Mbps) or Arcturus ($6.92, 2 GB / 30 GB).

## FAQ

**Can a 1 GB NVMe VPS run MySQL or PostgreSQL?**
Yes, for a small dataset and low concurrency. The constraint is memory before it is storage: at 1 GB total, the database buffer pool and the OS compete for the same RAM, so once your working set exceeds a few hundred MB you will see disk reads on every query. Arcturus at $6.92 doubles RAM to 2 GB for $2 more, which is the cheaper fix than upgrading the whole plan later.

**Is NVMe actually faster than SATA SSD for a small website?**
For a cached site with mostly static pages, barely. The difference shows up when PHP sessions, logs, database queries and file uploads all hit disk — the small random I/O pattern where PCIe latency beats the SATA interface. If your site is behind Cloudflare and mostly serves HTML, buy the cheaper storage and more RAM instead.

**Should I pay monthly or annually?**
Annual billing cuts roughly 20% off JustHost's rates, so a year of Sirius is $46.56 instead of $58.20. That is worth taking once you have run the plan for a month and know it fits. Start monthly, measure, then commit.

**What does "fair-share" mean on the port?**
The stated speed is a ceiling, not a guarantee, and it is shared with other customers on the same host. In practice a 300 Mbps port will not sustain 300 Mbps around the clock. Size the port for your peak, not for the TB number in the marketing copy.

**How many cores do I actually need?**
One core handles a single small site or a lightweight daemon. Two cores is the comfortable floor once a database and a web server share the box. Four cores is for build pipelines, container hosts running several services, or anything with concurrent workers — and at that point Bright Star ($9.80) is better value than climbing the single-core ladder.

## What to pick

A bot, a tunnel, a throwaway test box: **VPS Promo at $1.99**, accepting the 10 Mbps port and 512 MB as the price of admission. One real website or a small app: **Sirius at $4.85/$3.88**, the point where disk, RAM and port stop being compromises. A database, Docker with a few containers, or a CI runner: **Vega at $13.44/$10.75**, where 4 GB RAM and 80 GB of NVMe keep the buffer pool and the image layers off each other's toes. CPU-heavy work with modest storage: **Bright Star at $9.80/$7.84**.

Three things to confirm on the checkout screen before you pay: the plan name matches the configuration you chose, the total reflects the billing term you intended, and the datacenter is the one you want traffic routed through.

👉 [Open JustHost's full VPS price list and pick your tier](https://justhost.asia/en/services/vps/tariffs-all?ref=196392)
