# n8n VPS: How Much RAM You Need, What Self-Hosting Really Costs, and Which Plan to Pick (AVA Hosting n8n Plans From €5/mo)

Self-hosting n8n on a VPS turns your automation bill into a flat monthly charge, and on AVA Hosting that charge starts at €5/mo for a plan with n8n and PostgreSQL already deployed. Whether €5 covers you depends on how many workflows execute simultaneously, not on how many times they fire. One workflow on a five-minute trigger produces 8,640 executions a month (30 days × 24 hours × 12 runs), which is close to the entire monthly allowance of an entry n8n Cloud tier that third-party host pages quote at $20–$24/mo.

Below: the full plan list with prices and specs, the RAM thresholds that actually decide performance, what “pre-installed” covers on five different hosts, and four things to confirm before you pay.

> **Most readers should take the €5/mo plan.** 1 vCPU, 2 GB RAM, 25 GB NVMe, with n8n and PostgreSQL provisioned in one click, automatic n8n updates, scheduled backups, custom domain support and automated HTTPS included. Move to €10 (2 vCPU, 4 GB) when several workflows run concurrently or payloads grow; €20 (4 vCPU, 8 GB) is the tier where AI agent chains and vector-store lookups stop competing for memory.
> 👉 [Check the current n8n plan and price](https://my.ava.hosting/aff.php?aff=15562)

## AVA Hosting n8n and app plans, in full

The software itself is free. n8n's Community Edition has no licence fee, so the only recurring cost is the server underneath it. AVA Hosting sells two relevant product lines: self-hosted application plans, where n8n arrives pre-deployed with PostgreSQL, and raw VPS plans with root access.

Prices are the “starting from” figures shown on AVA Hosting's store pages, in euros, monthly billing unless marked annually, before VAT. Checkout shows the final amount for the term you choose.

| Plan | vCPU · RAM · NVMe | Price (EUR) | Best for | Order |
| --- | --- | --- | --- | --- |
| Start | 1 · 1 GB · 15 GB | €2.00/mo | A single light workflow, testing | View plan |
| Mini | 1 · 2 GB · 25 GB | €5.00/mo | The n8n default: a few workflows, one or two people | View plan |
| Basic | 2 · 4 GB · 50 GB | €10.00/mo | Concurrent workflows, larger payloads | View plan |
| Pro | 4 · 8 GB · 100 GB | €20.00/mo | AI agents, RAG pipelines, queue mode | View plan |
| Business | 6 · 12 GB · 150 GB | €30.00/mo | Heavy multi-worker setups | View plan |
| Power | 8 · 16 GB · 200 GB | €40.00/mo | Local models alongside production automation | View plan |

Unlimited transfer is included on every tier. The €2 Start plan is listed with a “Free Trial” label, but the page doesn't state how long the trial runs, so confirm that at checkout. At 1 GB of RAM it sits below the floor most hosts recommend for n8n; treat it as a sandbox rather than a place to run business workflows.

The VPS line is the other option, and it's the one to take if you want root, custom npm packages, or your own Docker Compose stack.

| Plan | vCPU · RAM · NVMe | Price (EUR) | Best for | Order |
| --- | --- | --- | --- | --- |
| VPS Nano | 1 · 512 MB · 20 GB | €11.00/yr | Nothing n8n-related; shown as 0 available | View plan |
| VPS One | 1 · 2 GB · 25 GB | €5.00/mo | Same size as Mini, but self-managed | View plan |
| VPS Basic | 2 · 4 GB · 50 GB | €10.00/mo | Self-managed production start | View plan |
| VPS Lucky | 2 · 6 GB · 70 GB | €15.00/mo | More RAM without more cores | View plan |
| VPS Power | 4 · 8 GB · 90 GB | €20.00/mo | Queue mode, multiple workers | View plan |
| VPS Extra | 6 · 12 GB · 120 GB | €30.00/mo | Concurrency plus retained history | View plan |
| VPS Ultra | 8 · 16 GB · 160 GB | €40.00/mo | Local models, heavy data transforms | View plan |

Every VPS plan lists full root access, weekly backups, DDoS protection, a 99.9% uptime SLA, unlimited bandwidth and a 1 Gbps port (the Nano is 100 Mbps). One detail that bites people: outbound port 25 is closed across the VPS line, so n8n can't deliver mail directly. Point the Send Email node at an SMTP relay instead.

## How much RAM does n8n actually need?

Guidance published by three different hosts converges on the same numbers. 2 GB is the working floor, 4 GB is a normal production size, and 8 GB is where AI work stops being cramped.

AVA Hosting maps n8n to its 2 GB plan at €5. OBHost's n8n page recommends 2 GB for personal use or small teams, and 4–8 GB for production environments with many concurrent workflows or AI agent pipelines. Hostinger's published minimum, as surfaced in search results, is 1 vCPU / 2 GB with 2+ vCPU / 4 GB recommended. Treat the Hostinger figure as a weaker source, but it lines up with the other two.

AVA Hosting's own caveat is worth quoting in substance: busy webhook endpoints, large files, or concurrent long-running workflows may require a larger plan.

One thing the marketing pages usually skip. PostgreSQL stores workflow definitions, users, credential metadata and every execution record, so the database grows with your history and the whole stack needs more headroom than an application-only RAM figure suggests. If you keep 30 days of execution history on a busy instance, budget one tier above what the workflow count implies, or trim retention.

one.com's tiering shows the same boundaries from a different angle: 2 vCPU / 4 GB for light workflows, 4 vCPU / 8 GB for moderate ones, 8 vCPU / 16 GB and above for heavy production.

👉 [See which AVA Hosting plan matches your RAM target](https://my.ava.hosting/aff.php?aff=15562)

## The execution math that decides whether self-hosting pays

A five-minute schedule is not an aggressive interval. It's the default for polling a CRM, checking an inbox, or syncing a sheet. Run the arithmetic and one such workflow lands at 8,640 executions per month. Two of them put you at 17,280.

Compare that with the n8n Cloud tiers quoted on hosting comparison pages: a Starter tier around $20–$24/mo capped near 2,500 executions, and a Pro tier at $60/mo capped at 10,000. Those figures come from third-party host pages rather than n8n's own pricing page, so treat them as an order of magnitude rather than a quote. The direction is unambiguous either way. A single five-minute workflow already exceeds the Starter allowance by a factor of three, and two of them exceed Pro.

Self-hosted plans don't meter executions at all. AVA Hosting charges €5 to €40/mo depending on the machine, and the workflow count doesn't enter the bill.

That flat fee buys resources, not infinite capacity. Your real ceiling is CPU, RAM and disk, which is why the “unlimited executions” line on every host's n8n page should be read as “no billing cap” rather than “no performance limit”. A 2 GB box will choke on twelve concurrent executions long before any invoice changes.

The trade is time. Cloud plans include hosting, upgrades and backups in the price. On a VPS you take on updates, monitoring, TLS renewal and error handling. AVA Hosting applies n8n updates automatically and includes scheduled backups, which removes part of that load, but nobody will test your workflows after a major version bump except you.

## What “pre-installed” covers on each host

Pre-installed ranges from “n8n is running, good luck with the rest” to “Docker and PostgreSQL are configured, log in and build”. The differences decide how much of your first weekend disappears.

- **AVA Hosting:** one-click deployment provisions n8n and PostgreSQL together, with automatic n8n updates, scheduled backups, custom domain support and automated HTTPS. The database ships unmanaged, so persistent data and database records are your responsibility to review before upgrades.
- **IONOS:** n8n, Docker and the web UI are pre-installed on VPS+ and dedicated servers. You reach the instance at the server IP on port 5678, and you have to open 5678 in the firewall panel yourself. The web interface is protected by HTTP Basic Auth with the username `admin` and your server's root password, which you can disable over SSH. Production use needs a domain and an SSL certificate you configure.
- **one.com:** n8n arrives with Docker and PostgreSQL preconfigured, advertised as no command line required, and plan upgrades apply from the control panel within minutes without a reinstall.
- **OVHcloud:** n8n is pre-installed on many VPS plans, and the page is explicit that OVHcloud covers hardware, network and virtualisation while you own OS updates, firewall rules, strong credentials, HTTPS and user permissions.
- **Bluehost:** a one-click n8n template at checkout, with support at the infrastructure layer only.

Four questions worth settling before you pay anywhere:

1. Is a domain and SSL configured, or do I get an IP address and port 5678 with Basic Auth?
2. Are backups included, how often do they run, and can I restore one myself?
3. Who applies n8n updates, and can I pin a version when a release breaks a node?
4. Is the database SQLite or PostgreSQL, and who manages it?

On AVA Hosting, questions 1, 2 and 3 are answered on the product page: HTTPS and custom domains are automated, backups are scheduled, and n8n updates are applied for you. Question 4 is the one to raise with support, because PostgreSQL is explicitly unmanaged.

## Where your data actually sits

Self-hosting keeps your workflows, credentials and execution history on your own disk. It does not keep everything in the building. Any workflow that calls OpenAI, Anthropic or Gemini sends prompts and payloads to that provider's cloud, and IONOS says so plainly on its own n8n page.

If data can't leave your infrastructure, you need local models through Ollama or a similar runtime, and that changes the spec. IONOS positions local Llama-class models as a dedicated-server workload; one.com points at its larger tiers for the same reason. On AVA Hosting's line, 8 GB (€20/mo) is the realistic entry point for a small local model running beside production automation, and 16 GB (€40/mo) leaves room to breathe.

Ask where the datacenter is before ordering if residency is a compliance requirement. Currency and pricing don't tell you that.

## How AVA Hosting compares on price

All figures below are as shown on each provider's page at the time of checking. Bluehost and OVHcloud list in USD, OBHost's page displays AUD, and one.com and IONOS didn't show prices in the pages reviewed. Convert before comparing.

| Provider | Example plan | vCPU · RAM · Storage | Price shown | Notes |
| --- | --- | --- | --- | --- |
| Bluehost | n8n VPS Standard | 2 · 4 GB · 80 GB SSD | $4.69–$25.99/mo across the range | One-click n8n template, 5 datacenter regions |
| OVHcloud | VPS-3 | 6 · 12 GB · 100 GB NVMe | from $12.32/mo | Pre-installed, OS security on you, anti-DDoS |
| OVHcloud | VPS-4 | 8 · 24 GB · 200 GB NVMe | from $23.37/mo | Same terms, 2 Gbps port |
| one.com | Cloud server S / M / L | 2·4 GB / 4·8 GB / 8·16 GB | Not shown on page | Docker + PostgreSQL preconfigured, EU data |
| IONOS | VPS+ | Varies by tier | Not shown on page | n8n, Docker, web UI pre-installed, port 5678 |
| OBHost | n8n VPS | From 2 GB RAM | from $6.89/mo (AUD) | 14-day money-back, 9 locations, KVM |

AVA Hosting's €5 for 2 GB and €10 for 4 GB sit in the same bracket as OVHcloud's entry pricing, with two practical differences: n8n updates and HTTPS are handled for you, and the VPS line includes weekly backups as standard. OVHcloud hands you OS patching and n8n upgrades, and gives you far more RAM per euro at the top of its range.

## Which plan to buy

Running a handful of webhooks and cron jobs for yourself or a two-person team: Mini at €5/mo. It matches the 2 GB floor every host recommends, and it's the plan AVA Hosting itself maps n8n to.

Several workflows firing at once, larger JSON payloads, or a month of retained execution history: Basic at €10/mo for the extra core and the doubled RAM. This is the tier most small teams end up on within a quarter.

AI agent chains, RAG with a vector store, queue mode with workers, or a local model: Pro at €20/mo, and Business at €30/mo if concurrency and history both grow.

Need root, custom npm packages, or your own Compose stack: the VPS line, starting at VPS One for €5/mo. Same size as Mini, but you build and secure everything, and you'll need an external SMTP relay because port 25 is closed.

Two things to confirm at checkout, since the store pages show starting prices: the renewal cost for the term you select, and the refund window. AVA Hosting's VPS listings include weekly backups and a 99.9% SLA, but the pages reviewed don't state a money-back period, so ask before paying rather than assuming one.

👉 [Compare AVA Hosting's n8n plans and current pricing](https://my.ava.hosting/aff.php?aff=15562)
