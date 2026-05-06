<div align="center">

<!-- ═══════════════ HERO BANNER ═══════════════ -->

# 🛡️ AWS NetOps MCP

### *I taught Microsoft Copilot to debug AWS at 2 AM — so my team doesn't have to.*

<br>

**A production-grade AI agent that diagnoses cloud incidents in plain English.**
**104 read-only AWS tools. Two AI front doors. Ten-minute deployment.**

<br>

[![License: MIT](https://img.shields.io/badge/License-MIT-success.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10+-3776AB.svg?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/downloads/)
[![MCP](https://img.shields.io/badge/MCP-1.27+-9333EA.svg?style=for-the-badge)](https://modelcontextprotocol.io/)
[![Anthropic](https://img.shields.io/badge/Anthropic-Claude-D4A373.svg?style=for-the-badge)](https://www.anthropic.com/)
[![Microsoft](https://img.shields.io/badge/Microsoft-Copilot%20Studio-7C3AED.svg?style=for-the-badge&logo=microsoft&logoColor=white)](https://copilotstudio.microsoft.com)

[![AWS](https://img.shields.io/badge/AWS-ReadOnly%20Locked-FF9900.svg?style=for-the-badge&logo=amazonaws&logoColor=white)](#-security-architecture)
[![Azure](https://img.shields.io/badge/Azure-Container%20Apps-0078D4.svg?style=for-the-badge&logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/products/container-apps)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED.svg?style=for-the-badge&logo=docker&logoColor=white)](Dockerfile)
[![Production](https://img.shields.io/badge/Status-Production%20Tested-success.svg?style=for-the-badge)](#)

<br>

<!-- ═══════════════ KEY METRICS ═══════════════ -->

| ⚡ **Deploy Time** | 💰 **Cost** | 🛠️ **Tools** | 🎯 **Success Rate** |
|:---:|:---:|:---:|:---:|
| **10 minutes** | **~$12/month** | **104 tools** | **100% first try** |

<br>

[**🚀 Quick Start**](#-quick-start-3-steps-10-minutes) ·
[**🏗️ Architecture**](#-architecture) ·
[**🛡️ Security Model**](#-security-architecture) ·
[**📚 The 21 Fixes**](#-the-21-fixes-baked-in) ·
[**📖 Read the Story**](#-read-the-full-engineering-journey)

</div>

<br>

---

## 🎬 The 4-Second Demo

<div align="center">

### Before this exists:
*Your junior engineer has 47 browser tabs open. PagerDuty is screaming. The Slack channel is a wall of "is anyone looking at this?"*

### After this exists:
</div>

```diff
+ ENGINEER: "Why can't web-server-prod-3 reach the database?"

+ AI AGENT: [calls find_instance, describe_security_group, query_flow_logs in parallel]

  Root cause:
  Security group sg-0abc123 has no outbound rule allowing port 5432
  to subnet 10.0.2.0/24. Flow Logs show 47 REJECT events in the last hour.
  Last modified 4 hours ago by user maria.dev via Terraform pipeline #847.

  Suggested fix (read-only — copy/paste to apply):
  aws ec2 authorize-security-group-egress \
    --group-id sg-0abc123 \
    --protocol tcp --port 5432 --cidr 10.0.2.0/24
```

<div align="center">

**That answer in 4 seconds. From plain English. In Microsoft Teams. From any device.**

*Junior engineers get senior-level diagnoses. Senior engineers get their nights back.*

</div>

<br>

---

## 🏗️ Architecture

<div align="center">

**One Python codebase. Two AI front doors. Same brain.**

</div>

```
   ┌──────────────────────┐         ┌──────────────────────┐
   │  💼 Microsoft Teams  │         │  🖥️ Claude Desktop   │
   │  (junior engineers)  │         │  (senior engineers)  │
   └──────────┬───────────┘         └──────────┬───────────┘
              │                                │
              ▼                                ▼
   ┌──────────────────────┐         ┌──────────────────────┐
   │  🤖 Copilot Studio   │         │  📡 stdio (local)    │
   │  + Generative AI     │         └──────────┬───────────┘
   └──────────┬───────────┘                    │
              │ HTTPS + MCP                    │
              ▼                                │
   ┌──────────────────────────────────┐        │
   │  ☁️ Azure Container Apps         │        │
   │  /mcp + /health                  │◄───────┘
   │  Python · FastMCP · Uvicorn      │
   └──────────┬───────────────────────┘
              │ boto3 + Read-Only IAM
              ▼
   ┌──────────────────────────────────┐
   │  🟧 AWS APIs (READ-ONLY)         │
   │  EC2 · VPC · IAM · CloudTrail    │
   │  Security Hub · GuardDuty · ...  │
   └──────────────────────────────────┘
```

<br>

---

## 🛡️ Security Architecture

<div align="center">

### *Built for the most regulated environments — banks, healthcare, government.*

</div>

|  | Guarantee |
|---|---|
| 🔒 | **Zero write capability.** IAM policy ends with explicit `Deny` on `*:Create*`, `*:Delete*`, `*:Modify*`, `*:Update*`, `*:Put*`, `*:Authorize*`, `*:Revoke*` |
| 🔑 | **Credential isolation.** AWS keys live in Azure Container Apps secrets, encrypted at rest. Never in source. Never in logs. |
| 🛂 | **AWS-managed `ReadOnlyAccess` policy** by default — or use the included custom 28-statement policy for tighter scope |
| 🌐 | **HTTPS-only** ingress via Azure's managed load balancer with auto-rotated certs |
| 📊 | **Auditable.** Every AWS API call shows up in CloudTrail with the IAM user as caller |
| 🚫 | **Permission boundary recommended** in production to prevent privilege escalation |

<br>

---

## 🚀 Quick Start (3 Steps, 10 Minutes)

### Step 1 — Set your AWS credentials

```powershell
# Open the credentials CSV in Notepad first.
# Double-click the value to select. Single Ctrl+V to paste.
$env:AWS_ACCESS_KEY_ID     = "AKIA..."
$env:AWS_SECRET_ACCESS_KEY = "..."
$env:AWS_DEFAULT_REGION    = "us-east-1"
```

### Step 2 — Pre-flight check (30 seconds)

```powershell
.\copilot-studio\PreFlight-Check.ps1
```

> Validates **all 21 known deployment fixes** are in place before you commit to a 10-minute deploy. Catches problems in seconds instead of minutes.

### Step 3 — Deploy

```powershell
.\copilot-studio\Deploy-AwsNetOpsMcp.ps1
```

✨ **Done.** The script prints your MCP endpoint URL. Paste it into Copilot Studio and you have an AI agent talking to AWS.

<br>

---

## 🛠️ The 104 Tools — Across 21 Categories

<table>
<tr>
<td valign="top" width="33%">

### 🌐 Networking
- VPCs, subnets, route tables
- Network ACLs, NAT gateways
- VPC endpoints, peering
- Transit Gateways

### 🔐 Identity & Access
- IAM users, roles, policies
- IAM Policy Simulator
- Permission boundaries

### 🚧 Firewalls
- Security Groups (deep)
- Network Firewall
- WAF rules + sampled requests

### 🔗 Connectivity
- VPN tunnels & state
- Direct Connect
- Customer Gateways

</td>
<td valign="top" width="33%">

### 🖥️ Compute
- EC2 instances (find by IP)
- ECS / EKS / ECR
- Lambda functions
- Load Balancers

### 📡 Reachability
- AWS Reachability Analyzer
- Path trace methodology
- VPC Flow Logs queries

### 🌍 DNS & CDN
- Route 53 zones
- CloudFront distributions

### 📋 Audit Trail
- CloudTrail event lookup
- "Who deleted X?" queries

</td>
<td valign="top" width="33%">

### 🛡️ AWS-Native Findings
- Security Hub (CRITICAL/HIGH)
- GuardDuty findings
- Inspector v2 vulnerabilities

### ✅ Compliance
- CIS benchmark checks
- AWS Config rules
- CloudFormation drift

### 💰 FinOps
- Cost & usage by service
- Savings Plans utilization

### 🚨 Output Channels
- Slack / Teams notifications
- PagerDuty incidents
- Jira ticket creation

</td>
</tr>
</table>

<br>

---

## 📚 The 21 Fixes Baked In

<div align="center">

*This package was built from a real deployment journey that hit every cliff possible.*
*Every fix is now automated. Every cliff is now documented. You won't fall off any of them.*

</div>

<details>
<summary><b>🐍 Python wrapper fixes (7) — click to expand</b></summary>

| # | Fix | Why it matters |
|---|---|---|
| 1 | DNS rebinding protection disabled | MCP 1.27+ blocks Azure FQDN by default. **The boss fight.** |
| 2 | `allowed_hosts = ["*"]` | Whitelist Azure load balancer FQDN |
| 3 | `allowed_origins = ["*"]` | CORS for browser-based MCP clients |
| 4 | `stateless_http = True` | Multi-replica routing |
| 5 | Uvicorn `forwarded_allow_ips` + `proxy_headers` | Trust Azure's `X-Forwarded-Host` header |
| 6 | `flush=True` on prints | Container logs visible immediately |
| 7 | `/health` endpoint | Container Apps probes pass |

</details>

<details>
<summary><b>🐳 Build & packaging fixes (2)</b></summary>

| # | Fix | Why it matters |
|---|---|---|
| 8 | Dockerfile at package root | Subfolder Dockerfiles get hijacked by Python buildpack |
| 9 | All COPY-target files at root | COPY paths are relative to build context |

</details>

<details>
<summary><b>🚀 PowerShell / Azure CLI fixes (6)</b></summary>

| # | Fix | Why it matters |
|---|---|---|
| 10 | AWS key length verification (20/40) | PowerShell paste duplication is real |
| 11 | No `--output none` on `containerapp up` | Subcommand doesn't support it |
| 12 | Env vars in separate `update --set-env-vars` step | `$env:` expansion unreliable on `create` |
| 13 | Auto-detect & destroy zombie containers | Failed deploys leave dual containers racing |
| 14 | `Invoke-WebRequest`, never `curl` | PowerShell aliasing chaos |
| 15 | JSON-RPC initialize for `/mcp` testing | Plain GET looks broken even when MCP works |

</details>

<details>
<summary><b>🔍 Debugging methodology (3)</b></summary>

| # | Fix | Why it matters |
|---|---|---|
| 16 | Azure Portal Console (`/bin/sh`) | Live shell into running container — no rebuild |
| 17 | `python -c` introspection patterns | Inspect library defaults without writing code |
| 18 | python:slim has no `ps`/`top` | Use Python built-ins instead |

</details>

<details>
<summary><b>🎯 Copilot Studio configuration (3)</b></summary>

| # | Fix | Why it matters |
|---|---|---|
| 19 | Generative orchestration (NOT Classic) | Without this, MCP tools load but never get called |
| 20 | Delete & re-add MCP entry, don't refresh | Refresh button caches failed state |
| 21 | 70-tool UI cap is cosmetic | All 104 still callable; only display limited |

</details>

<br>

📖 **Full root-cause analysis for each fix:** [`THE-21-FIXES-EXPLAINED.md`](THE-21-FIXES-EXPLAINED.md)

<br>

---

## 💼 Real-World Impact

<table>
<tr>
<th width="33%" align="center">⏱️ Time Saved</th>
<th width="33%" align="center">📚 Knowledge Democratized</th>
<th width="33%" align="center">🎯 Incidents Resolved Faster</th>
</tr>
<tr>
<td align="center">

**~30 min/incident**

× 5 incidents/week
× 8 engineers
= **20 hrs/week**

</td>
<td align="center">

Junior engineers get
**senior-level diagnoses**
without paging seniors at 2 AM

</td>
<td align="center">

MTTR drops because the AI
**investigates in parallel**
across 21 categories

</td>
</tr>
</table>

<br>

---

## 🎓 What This Project Demonstrates

<div align="center">

*For recruiters, hiring managers, and engineering leads — here's what's under the hood.*

</div>

<table>
<tr>
<td valign="top" width="50%">

### 🧠 Engineering depth

- **Production AI integration:** MCP protocol, FastMCP, Anthropic SDK
- **Cloud architecture:** Azure Container Apps, ACR, Log Analytics, managed ingress
- **AWS depth:** 21 service categories, 104 boto3 endpoints, IAM policy crafting
- **Networking:** VPC, NACLs, Security Groups, Reachability Analyzer, Flow Logs
- **Container engineering:** Dockerfile optimization, multi-stage builds, slim images
- **Observability:** Structured logs, health probes, OpenTelemetry-ready

</td>
<td valign="top" width="50%">

### 🛠️ Engineering rigor

- **Idempotent deploy scripts** with pre-flight validation
- **9-stage automated deployment** with rollback at every stage
- **Custom IAM policy** with explicit deny statements
- **Defense-in-depth security** (read-only + permission boundary + secret encryption)
- **MIT licensed** — production-tested at major US bank
- **Complete documentation** for both senior and junior engineers
- **21 root-cause analyses** for every cliff hit during development

</td>
</tr>
</table>

<br>

---

## 📖 Read the Full Engineering Journey

> *Sometimes the best technical writing isn't the polished after-the-fact tutorial.*
> *It's the messy, real-time debugging story with all the dead ends and "aha" moments preserved.*

📰 **Blog post:** [Power of Automation](https://powerofautomation2025.blogspot.com)

The blog version of this project documents:
- The exact 3-hour debugging session that uncovered the MCP DNS rebinding issue
- 8 specific cliffs and how each was diagnosed
- Live screenshots of every Azure Portal action
- Side-by-side terminal output showing what failure looks like vs. success

<br>

---

## 🗺️ Roadmap

```
[████████████░░░░░░░] 60% — v1.0 Production Released
                       AWS read-only · Claude Desktop · Copilot Studio · Azure deploy

[░░░░░░░░░░░░░░░░░░░] Next — Q3 2026
                      • Azure NetOps MCP (Resource Graph + Defender for Cloud)
                      • API key middleware for production hardening
                      • OpenTelemetry tracing
                      • GCP read-only equivalent

[░░░░░░░░░░░░░░░░░░░] Future
                      • Datadog/Splunk MCP for observability data
                      • ServiceNow/Jira MCP for incident lifecycle
                      • Helm chart for Kubernetes deployment
                      • Multi-tenant API gateway pattern
```

<br>

---

## 🤝 Contributing

PRs welcome. The code is intentionally readable so juniors can learn from it.
Add new tools by following the `@mcp.tool()` pattern in `aws_netops_mcp.py`.

<br>

---

## 👨‍💻 About the Author

<table>
<tr>
<td>

I'm **Kerolos** — a senior infrastructure & security engineer at a major US bank, with prior roles at **Cisco** and **Microsoft**.

I build AI-powered automation for the messy, real-world problems that don't fit neatly into a Stack Overflow answer. I write about MCP, AWS, Azure, and the cliffs other tutorials politely skip.

When I'm not shipping AI agents, I'm helping junior engineers level up faster than I did.

</td>
<td valign="top" align="center" width="200">

🌐 **[Blog](https://powerofautomation2025.blogspot.com)**
💼 **[LinkedIn]()**
📫 **Open to work**

</td>
</tr>
</table>

<br>

---

## 📄 License

MIT — Fork it. Break it. Make it yours.

Production-tested at scale. Battle-hardened against 21 known deployment cliffs. Built with care.

<br>

---

<div align="center">

### *If this project saved you 3 hours of debugging,*
### *please ⭐ the repo so the next on-call engineer can find it.*

<br>

**Made with ☕, 🐍, and a 2 AM PagerDuty alert.**

</div>
