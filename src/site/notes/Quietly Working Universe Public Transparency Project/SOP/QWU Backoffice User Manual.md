---
{"dg-publish": true, "permalink": "/quietly-working-universe-public-transparency-project/sop/qwu-backoffice-user-manual/", "noteIcon": "", "tags": ["operations", "pkm", "automation", "azure", "docker", "calendar", "leads", "wisdom", "experts", "l4g", "content-calendar", "relationships"]}
---
> [!INFO] PUBLIC VERSION
> This is the public, redacted version of the QWU Backoffice User Manual. Sensitive data (IPs, credentials, project IDs, personal names) has been replaced with descriptive placeholders like `<VM_IP>` or `[Member Name]`. The structure and educational content are preserved for transparency and Missing Pixel student training.
>
> Generated: 2026-03-17 08:02 | Source version: 3.44

# QWU Backoffice User Manual

**Version: 3.44 | Started: 251223 | Updated: 260317**

A comprehensive guide to the QWU Backoffice agent workspace, covering architecture, daily operations, automation, and development workflows. These notes serve both as operational documentation and educational curriculum for Missing Pixel students.

---

## Table of Contents

1. [[#Environment Overview]]
2. [[#Getting Started]]
3. [[#Daily Operations]]
4. [[#One-Tap Mobile VM Control via n8n ⭐]]
5. [[#Running Agent Jobs]]
6. [[#Overnight/Long-Running Jobs]]
7. [[#Mobile Access via Termux (Android) ⭐]]
8. [[#Obsidian + GitHub Integration: Unified Workspace]]
9. [[#Sparse Checkout: Filtering Files on Azure VM]]
10. [[#Syncing Workflow]]
11. [[#Claude Code: Modes and Commands]]
12. [[#Quick Reference Sheets]]
13. [[#DOE Architecture & Skills System]]
14. [[#Morning Briefing System ⭐]]
15. [[#Daily Summary System ⭐]]
16. [[#Google Calendar Integration]]
17. [[#Google Docs Sync System]]
18. [[#Video Content Pipeline]]
19. [[#Voice Profiles]]
20. [[#Expert Intelligence System ⭐]]
21. [[#Wisdom Synthesis System ⭐]]
22. [[#Canonical Datetime System]]
23. [[#Azure Cost Tracking]]
24. [[#Lead Generation System]]
25. [[#Communications Architecture]]
26. [[#Data Architecture]]
27. [[#Project Organization]]
28. [[#YAML Frontmatter Standards]]
29. [[#Docker Fundamentals: Running Isolated Tasks]]
30. [[#Docker Sandbox Security]]
31. [[#Meeting Intelligence System ⭐]]
32. [[#Outlook Email Processing ⭐]]
33. [[#SuiteDash CRM Integration ⭐]]
34. [[#Transcript Extraction System (Planned)]]
35. [[#Ez/Ezer Mascot]]
36. [[#Ez Terminal (Scheduler) ⭐ NEW]]
37. [[#Troubleshooting]]
37. [[#Resources]]
38. [[#BNI Member Dossier System]]
39. [[#BNI Meeting Recap System ⭐ NEW]]
40. [[#System Architecture Audit ⭐ NEW]]
41. [[#EPIC Appointment Intelligence System v2.0 ⭐ NEW]]
42. [[#Ezer Aión Assistant System ⭐ NEW]]
43. [[#Strategic Goals Framework ⭐ NEW]]
44. [[#QWU Cosmic Style Guide ⭐ NEW]]
45. [[#Content Calendar System ⭐ NEW]]
46. [[#Daily Journal Command Center ⭐ NEW]]
47. [[#Supervisor Observability System (SOS) ⭐ NEW]]
48. [[#Relationship Intelligence Layer ⭐ NEW]]
49. [[#Parallel Execution System ⭐ NEW]]
50. [[#Ezer Universal Interface ⭐ NEW]]
51. [[#Project System Status Files ⭐ NEW]]
52. [[#Supervisor Architecture]]
53. [[#HQ Command Center ⭐ NEW]]
54. [[#QWR SEO Intelligence ⭐ NEW]]
55. [[#Customer System Safeguards ⭐ NEW]]
56. [[#GreenCal Command Center ⭐ NEW]]
57. [[#Pocket Ez Companion App ⭐ NEW]]
58. [[#Public Manual Generation System ⭐ NEW]]
59. [[#QWR Audience Intelligence System ⭐ NEW]]
60. [[#QKN Quietly Knocking ⭐ NEW]]
61. [[#QSP Quietly Spotting ⭐ NEW]]
62. [[#QNT Quietly Networking ⭐ NEW]]
63. [[#QWR Content Performance Intelligence ⭐ NEW]]
64. [[#QWR Press Release Service ⭐ NEW]]
65. [[#Cost Intelligence System ⭐ NEW]]
66. [[#QWR Reverse Benchmarking Intelligence ⭐ NEW]]
67. [[#QWR Content Strategy System ⭐ NEW]]
68. [[#QWR Preparation Workbook ⭐ NEW]]
69. [[#QWF Ecosystem Landing Section ⭐ NEW]]
70. [[#Auto-Remediation System ⭐ NEW]]
71. [[#QTR Quietly Tracking ⭐ NEW]]
72. [[#QWF Ecosystem Widget ⭐ NEW]]
73. [[#QWR Team Accounts System ⭐ NEW]]
74. [[#QWF Documentation Standard ⭐ NEW]]
75. [[#Weavy Creative Production System ⭐ NEW]]
76. [[#Session Log]]

---

## Environment Overview

### What is the QWU Backoffice?

The QWU Backoffice is an AI agent workspace running on Microsoft Azure, designed to automate operations for The Quietly Working Foundation. It provides a secure, sandboxed environment where Claude Code agents can execute tasks, process data, and manage workflows.

### Architecture: Azure VM + Docker + VS Code Remote

```
┌─────────────────────────────────────────────────────────────────┐
│  YOUR DEVICES                                                    │
├─────────────────────────────────────────────────────────────────┤
│  Windows PC          │  Android Phone       │  Any Browser      │
│  VS Code + SSH       │  Termux + SSH        │  Azure Portal     │
└──────────┬───────────┴──────────┬───────────┴─────────┬─────────┘
           │                      │                     │
           └──────────────────────┼─────────────────────┘
                                  │
                                  ▼
┌─────────────────────────────────────────────────────────────────┐
│  AZURE CLOUD                                                     │
├─────────────────────────────────────────────────────────────────┤
│  ┌─────────────────────────────────────────────────────────┐    │
│  │  Ubuntu VM (claude-dev-vm)                              │    │
│  │  ┌─────────────────┐  ┌─────────────────────────────┐   │    │
│  │  │  Docker         │  │  qwu_backOffice/            │   │    │
│  │  │  (isolated      │  │  ├── .claude/               │   │    │
│  │  │   containers)   │  │  ├── 005 Operations/        │   │    │
│  │  └─────────────────┘  │  │   ├── Directives/        │   │    │
│  │                       │  │   └── Execution/         │   │    │
│  │                       │  └── [obsidian vault]       │   │    │
│  │  ┌─────────────────┐  └─────────────────────────────┘   │    │
│  │  │  Claude Code    │                                    │    │
│  │  │  (AI agent)     │                                    │    │
│  │  └─────────────────┘                                    │    │
│  └─────────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────────┘
```

### VM Details

| Property | claude-dev-vm | qwu-n8n |
|----------|--------------|---------|
| Resource Group | <RESOURCE_GROUP> | <RESOURCE_GROUP> |
| Region | West US 2 | West US 2 |
| Size | Standard D4as_v6 (4 vCPUs, 16 GB RAM, 128 GiB NVMe) | Standard B2s (2 vCPUs, 4 GB RAM, ~$30/mo) |
| IP | <VM_IP_CLAUDE_DEV> (static) | <VM_IP_N8N> (static) |
| Image | Ubuntu Server 24.04 LTS | Ubuntu Server 24.04 LTS |
| Swap | 4 GB | 6 GB (2GB + 4GB added 2026-02-23) |
| Operation Mode | 24/7 always-on | 24/7 always-on |
| Purpose | Backoffice agent workspace | n8n workflow engine + Caddy + Postgres |

### Infrastructure Monitoring & Backups

The QWU infrastructure is monitored at three layers, all documented in `005 Operations/Directives/infrastructure_monitoring.md`.

**External Monitoring (Betterstack)**
- **Plan:** AppSumo lifetime deal (2 stacked codes) — 200 monitors, 10 status pages, 5 members
- **17 HTTP monitors** (updated 2026-03-11): 10 WPMU sites, 5 infrastructure services, QWR app, OCN supporter site
- **4 heartbeat monitors:** claude-dev, n8n, WPMU VM, OCN VM (all every 6 hours)
- Alerts: phone call + SMS + email + push notification
- Outgoing webhook (ID 80218) fires on incident events → triggers auto-remediation (see [[#Auto-Remediation System ⭐ NEW]])
- **Status page:** [status.quietlyworking.org](https://status.quietlyworking.org) — two sections: "[Supporter Organization]" (supporter, first position) and "QWU Infrastructure" (all QWF sites + apps + infra + heartbeats)
- WPMU and OCN Lightsail CPU alarms deleted (2026-03-11) — they flapped due to WP-Cron bursts and xmlrpc attacks; Betterstack uptime monitoring is more useful

**Internal Health Checks**
- `check_vm_health.py` runs every 6 hours via cron on both VMs
- Collects: disk, memory, load, Docker containers, n8n workflow failures
- Posts health embed to Discord `#system-status`
- Always pings Betterstack heartbeat regardless of health status (v1.1.0). The heartbeat proves "VM is alive and monitoring is running." Service-level issues are reported via Discord alerts separately. A missing heartbeat should only mean "VM is unreachable."
- Thresholds: 80% warning, 90% critical for disk/memory
- Systemd services monitored: `sms-webhook`, `digital-twin`, `qnt-webhook`, `caddy`

**Application Health Checks**
- `check_calendar_health.py` runs every 2 hours via cron on claude-dev
- Validates HQ Command Center's `google-calendar-events` Supabase edge function
- Auto-redeploys known-good source via Supabase CLI if broken
- Posts to Discord `#system-status` (healthy/healed/still-broken)

**Database Backups**
- Nightly at 3 AM UTC: `backup_n8n_postgres.sh` on n8n VM
- Local rotation: 7 daily + 4 weekly (~8MB compressed per backup)
- Offsite: uploaded to Azure Blob Storage (`<STORAGE_ACCOUNT>` account, `n8n-backups` container)
- Restore: `az storage blob download ... && gunzip -c restore.sql.gz | docker exec -i n8n-postgres psql -U n8n n8n`

---

## Getting Started

### Accessing the Workspace (VS Code Connection)

1. Start the VM (Azure Portal or one-tap mobile script)
2. Open VS Code
3. Click green button (bottom-left) → Connect to Host → `claude-dev`
4. You're in!

### First-Time Setup for New Team Members

1. Generate SSH key on your machine
2. Send public key to admin
3. Admin adds to VM's `~/.ssh/authorized_keys`
4. Configure SSH in `~/.ssh/config`:

```
Host claude-dev
    HostName <VM_IP_CLAUDE_DEV>
    User <VM_USER>
    IdentityFile ~/.ssh/your-key.pem
```

### Understanding the Dev Container

The `.devcontainer/` folder contains configuration for isolated development:
- `Dockerfile` - Container image definition
- `devcontainer.json` - VS Code settings
- `init-firewall.sh` - Network security rules

### "Reopen in Container" — When to Click vs Dismiss

When you connect via VS Code Remote SSH, you may see a popup asking to "Reopen in Container." Here's when to use each option:

**Click "Reopen in Container" when you want to:**
- Work inside the sandboxed Claude Code agent environment
- Develop/test in the isolated Docker container
- Run agent operations that need that specific secure environment

**Click "Don't Show Again" or dismiss when you want to:**
- Work directly on the VM itself
- Access the Obsidian vault, check logs, manage Docker containers from the host
- Run tmux sessions for overnight agent monitoring
- General system administration

**Typical daily workflow:** For most day-to-day work—checking on agents, syncing the vault, running n8n-triggered operations—you probably want to stay on the SSH connection to the VM host rather than reopening inside the container.

**Switching between them:**
- **To enter container:** Command Palette (`Ctrl+Shift+P`) → `Dev Containers: Reopen in Container`
- **To return to VM host:** Command Palette → `Remote-SSH: Connect to Host` → `claude-dev`

---

## Daily Operations

### Starting Your Work Day

**Option 1: One-Tap Mobile (Recommended)**
Tap `qwu-start.sh` widget on phone → auto-connects when ready

**Option 2: Manual Start**
1. Azure Portal → Find `claude-dev-vm`
2. Click **Start**
3. Wait ~60 seconds
4. VS Code → Connect to `claude-dev`

### Stopping the VM When Done

**Option 1: One-Tap Mobile**
Tap `qwu-stop.sh` widget

**Option 2: From VS Code Terminal**
```bash
sudo shutdown now
```

**Option 3: Let Auto-Shutdown Handle It**
VM stops at 7 PM Pacific automatically.

### Checking Costs in Azure Portal

1. Azure Portal → Cost Management
2. Filter by resource group: `<RESOURCE_GROUP>`
3. Review daily/monthly spend

---

## One-Tap Mobile VM Control via n8n ⭐

Start and stop your Azure VM from your phone with a single tap... no Azure Portal needed.

### Architecture

```
Phone (Termux Widget)
    → n8n Webhook (cloud, always on)
    → Azure API (start/stop/status)
    → VM responds
    → Termux polls for SSH
    → Auto-connects when ready
```

### Components

| Component | Purpose |
|-----------|---------|
| Azure Service Principal | Scoped credentials for VM control only |
| n8n Workflow | Handles Azure auth + VM commands |
| Termux Scripts | One-tap triggers + SSH connection |
| Global Variable | Single location for secret rotation |

### Azure Service Principal Details

Created via Azure Cloud Shell:

```bash
az ad sp create-for-rbac \
  --name "n8n-vm-automation" \
  --role "Virtual Machine Contributor" \
  --scopes "/subscriptions/{sub-id}/resourceGroups/<RESOURCE_GROUP>/providers/Microsoft.Compute/virtualMachines/claude-dev-vm"
```

| Field | Value |
|-------|-------|
| Client ID | `<AZURE_CLIENT_ID>` |
| Client Secret | Stored in n8n Variables |
| Tenant ID | `<AZURE_TENANT_ID>` |
| Subscription ID | `<AZURE_SUBSCRIPTION_ID>` |
| Resource Group | `<RESOURCE_GROUP>` |
| VM Name | `claude-dev-vm` |

### n8n Webhook Endpoints

| Action | URL |
|--------|-----|
| Start | `https://n8n.quietlyworking.org/webhook/vm-control?action=start` |
| Stop | `https://n8n.quietlyworking.org/webhook/vm-control?action=stop` |
| Status | `https://n8n.quietlyworking.org/webhook/vm-control?action=status` |

### Termux Scripts

**~/.shortcuts/qwu-start.sh** - Start VM + wait + connect:

```bash
#!/data/data/com.termux/files/usr/bin/bash
# Version: 1.0.0
# QWU Start + Connect

WEBHOOK_URL="https://n8n.quietlyworking.org/webhook/vm-control?action=start"
VM_IP="<VM_IP_CLAUDE_DEV>"
MAX_ATTEMPTS=24

echo "🚀 Starting QWU Backoffice..."
curl -s "$WEBHOOK_URL"

echo "⏳ Waiting for VM..."
ATTEMPTS=0
until nc -z -w 5 $VM_IP 22 2>/dev/null; do
    ATTEMPTS=$((ATTEMPTS + 1))
    if [ $ATTEMPTS -ge $MAX_ATTEMPTS ]; then
        echo "❌ VM didn't respond in time"
        exit 1
    fi
    echo "   Attempt $ATTEMPTS/$MAX_ATTEMPTS..."
    sleep 5
done

echo "✅ Connecting..."
ssh qwu
```

**~/.shortcuts/qwu-stop.sh** - Deallocate VM (saves money):

```bash
#!/data/data/com.termux/files/usr/bin/bash
# Version: 1.0.0
# QWU Stop

WEBHOOK_URL="https://n8n.quietlyworking.org/webhook/vm-control?action=stop"

echo "🛑 Stopping QWU Backoffice..."
curl -s "$WEBHOOK_URL"
echo "✅ Shutdown initiated"
```

### Setup in Termux

```bash
# Create shortcuts directory
mkdir -p ~/.shortcuts

# Create and edit scripts
nano ~/.shortcuts/qwu-start.sh
nano ~/.shortcuts/qwu-stop.sh

# Make executable
chmod +x ~/.shortcuts/qwu-start.sh
chmod +x ~/.shortcuts/qwu-stop.sh

# Install netcat if needed
pkg install netcat-openbsd
```

Then add Termux:Widget to your home screen.

### Credential Rotation

The Azure client secret expires after 12 months. To rotate:

1. Azure Portal → Microsoft Entra ID → App registrations → n8n-vm-automation
2. Certificates & secrets → New client secret (12 months)
3. Copy the new secret value
4. n8n → Variables → Update `azure_client_secret`
5. Delete the old secret in Azure

**Calendar reminder set for 2 weeks before expiration (December 2026).**

### Self-Hosted n8n Instance (n8n.quietlyworking.org) ⭐ NEW

As of January 2026, we migrated from n8n Cloud to a self-hosted instance to reduce costs.

| Property | Value |
|----------|-------|
| **URL** | https://n8n.quietlyworking.org |
| **VM** | qwu-n8n (Azure B1ms, Ubuntu 22.04) |
| **API Endpoint** | https://n8n.quietlyworking.org/api/v1 |

**Environment Variables** (in `.env`):
```bash
N8N_API_URL=https://n8n.quietlyworking.org/api/v1
N8N_API_KEY=<API_KEY>  # Full key in .env
```

**API Usage** (from QWU Backoffice VM):
```bash
# List all workflows
curl -s "$N8N_API_URL/workflows" -H "X-N8N-API-KEY: $N8N_API_KEY" | jq '.data[] | {name, id, active}'

# Import a workflow
cat workflow.json | jq '{name, nodes, connections, settings}' | \
  curl -s -X POST "$N8N_API_URL/workflows" \
  -H "X-N8N-API-KEY: $N8N_API_KEY" \
  -H "Content-Type: application/json" -d @-

# Activate a workflow
curl -s -X POST "$N8N_API_URL/workflows/{workflow_id}/activate" \
  -H "X-N8N-API-KEY: $N8N_API_KEY"
```

**Naming Convention for .env:**
- API keys should follow: `SERVICE_API_KEY` format (e.g., `N8N_API_KEY`, `SUITEDASH_SECRET_KEY`)
- Use UPPERCASE_WITH_UNDERSCORES, not lowercase-with-hyphens
- Include a comment above explaining the key's purpose

**SSH Access to n8n VM** (from QWU Backoffice):
```bash
ssh qwu-n8n                    # Connect to n8n VM
ssh qwu-n8n "docker ps"        # Run single command
```

**Managing n8n Environment Variables:**

The self-hosted Community Edition uses server environment variables (`$env.VARIABLE_NAME`) instead of the Cloud Pro Variables UI (`$vars`).

```bash
# View current variables
ssh qwu-n8n "cat ~/n8n/.env"

# Add new variable (example)
ssh qwu-n8n "echo 'NEW_VAR=value' >> ~/n8n/.env"

# Also add to docker-compose.yml environment section, then restart:
ssh qwu-n8n "cd ~/n8n && docker compose up -d"
```

**Available Discord Webhook Variables:**
| Variable | Purpose |
|----------|---------|
| `DISCORD_WEBHOOK_AGENT_LOG` | #agent-log notifications |
| `DISCORD_WEBHOOK_INBOX_ALERTS` | #inbox-alerts for errors |
| `DISCORD_WEBHOOK_DAILY_DIGEST` | Daily summaries |
| `DISCORD_WEBHOOK_L4G_LEADS` | Lead generation alerts |
| `DISCORD_WEBHOOK_SYSTEM_STATUS` | System status updates |
| `DISCORD_WEBHOOK_TIG_BOOKING` | Booking notifications |
| `DISCORD_WEBHOOK_CONTENT_REVIEW` | Content review channel |
| `DISCORD_WEBHOOK_CONTENT_QUEUE` | Content queue reminders |
| `DISCORD_WEBHOOK_NEWSLETTER_REVIEW` | Newsletter review |
| `DISCORD_WEBHOOK_RESEARCH_QUEUE` | Research queue items |

**Usage in n8n Workflows:**
```
{{ $env.DISCORD_WEBHOOK_AGENT_LOG }}
```

**Active Ezer Workflows:**
| Workflow | Schedule | Purpose |
|----------|----------|---------|
| SMS Approval Webhook | Always-on | Route incoming SMS to dev VM |
| Ezer Morning Health Check-in | Daily 7 AM PT | Proactive health reminder |
| Ezer Discord DM Poller | Every 3 min | Process Discord DM voice messages |

### Migrating Workflows from Cloud Pro to Self-Hosted ⭐ MP TRAINING

This section documents how to migrate n8n workflows from Cloud Pro (or any exported JSON) to the self-hosted instance. This is an excellent **MP Student training opportunity** (Contributor tier+).

#### Key Differences: Cloud Pro vs Self-Hosted

| Aspect | Cloud Pro | Self-Hosted Community |
|--------|-----------|----------------------|
| Variables syntax | `$vars.variable_name` | `$env.VARIABLE_NAME` |
| Variables UI | Built-in Settings → Variables | Server environment variables |
| SSH credentials | May have different ID | Credential ID: `<SSH_CREDENTIAL_ID>` |
| SSH credential name | Varies | "QWU Backoffice SSH - 20251224a" |

#### Step-by-Step Migration Process

**1. Export the workflow from Cloud Pro:**
```bash
# In Cloud Pro: Workflow → ⋮ menu → Export
# Save as JSON file
```

**2. Identify changes needed:**

Run this check on the exported JSON:
```bash
# Check for $vars references (need to change to $env)
grep -o '\$vars\.[a-z_]*' workflow.json | sort -u

# Check SSH credential references
grep -A5 '"sshPrivateKey"' workflow.json
```

**3. Convert variable references:**

| Find | Replace With |
|------|--------------|
| `$vars.discord_webhook_agent_log` | `$env.DISCORD_WEBHOOK_AGENT_LOG` |
| `$vars.discord_webhook_*` | `$env.DISCORD_WEBHOOK_*` (UPPERCASE) |
| Any `$vars.lowercase` | `$env.UPPERCASE_UNDERSCORES` |

**4. Update SSH credentials:**

Replace any SSH credential block with:
```json
"credentials": {
  "sshPrivateKey": {
    "id": "<SSH_CREDENTIAL_ID>",
    "name": "QWU Backoffice SSH - 20251224a"
  }
}
```

**5. Clean the JSON for API import:**

The n8n API rejects certain properties. Remove these before import:
```bash
# Create clean version for API
cat workflow.json | python3 -c "
import json, sys
data = json.load(sys.stdin)
for key in ['staticData', 'triggerCount', 'tags', 'id', 'meta']:
    data.pop(key, None)
print(json.dumps(data))
" > workflow-clean.json
```

**6. Deploy via API:**
```bash
# Source environment (or use literal values)
source .env

# Create workflow
curl -s -X POST \
  -H "X-N8N-API-KEY: $N8N_API_KEY" \
  -H "Content-Type: application/json" \
  -d @workflow-clean.json \
  "$N8N_API_URL/workflows"

# Note the returned workflow ID
```

**7. Activate the workflow:**
```bash
curl -s -X POST \
  -H "X-N8N-API-KEY: $N8N_API_KEY" \
  "$N8N_API_URL/workflows/{WORKFLOW_ID}/activate"
```

**8. Verify deployment:**
```bash
# List all workflows and check status
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" "$N8N_API_URL/workflows" | \
  python3 -c "import json,sys; data=json.load(sys.stdin); \
  [print(f\"{w['id']}: {w['name']} (active: {w['active']})\") for w in data.get('data',[])]"
```

#### Common Pitfalls

| Issue | Solution |
|-------|----------|
| `$vars` not found | Self-hosted uses `$env` - convert all variable references |
| SSH authentication fails | Ensure `authentication: "privateKey"` is set in SSH node parameters |
| API returns "additional properties" | Remove `staticData`, `triggerCount`, `tags` from JSON |
| Webhook doesn't trigger | Known API bug - see Troubleshooting section; import via UI instead |
| Wrong credential ID | Use ID `<SSH_CREDENTIAL_ID>` for all SSH nodes |

#### Save the Workflow Locally

Always save the migrated workflow JSON to version control:
```bash
# Standard location for workflow JSON files
005 Operations/Workflows/your-workflow-name.json
```

#### MP Student Learning Objectives

Students completing this module will learn:
- JSON editing and transformation
- API authentication patterns
- Environment variable conventions
- CI/CD concepts (deploy → activate → verify)
- Debugging API responses
- Version control for infrastructure

### n8n Version Management ⭐ NEW

The self-hosted n8n instance uses pinned version tags for stability.

**Current Version:** 2.8.0 (as of 2026-02-11)

| Property | Value |
|----------|-------|
| Image | `docker.n8n.io/n8nio/n8n:2.8.0` |
| Location | `~/n8n/docker-compose.yml` on qwu-n8n |
| Monitor Workflow | "n8n Version Monitor" (checks Mondays 9 AM) |

**Update Procedure:**
```bash
# 1. SSH to n8n VM
ssh qwu-n8n

# 2. Backup database
cd ~/n8n
docker exec n8n-postgres pg_dump -U n8n n8n | gzip > backup_$(date +%Y%m%d).sql.gz

# 3. Update version in docker-compose.yml
# Change: image: docker.n8n.io/n8nio/n8n:2.8.0
# To:     image: docker.n8n.io/n8nio/n8n:X.Y.Z

# 4. Pull new image and restart
docker compose pull n8n && docker compose up -d

# 5. Verify version
docker exec n8n n8n --version

# 6. Verify all workflows still active
docker exec n8n-postgres psql -U n8n -d n8n -c \
  "SELECT COUNT(*) as total, SUM(CASE WHEN active THEN 1 ELSE 0 END) as active FROM workflow_entity;"
```

**Version Monitoring (v2.0.0 - Release Intelligence):**
- The "n8n Version Monitor" workflow checks GitHub releases every Monday 9 AM
- Parses release notes for QWU-relevant changes using node inventory
- Color-coded notifications by severity:
  - 🚨 Major (X.0.0) - Red, high priority
  - 🔄 Minor (X.Y.0) - Orange, medium priority
  - 📦 Patch (X.Y.Z) - Green, routine
- Skips pre-release versions (e.g., 2.5.x)
- Update the `currentVersion` constant in the workflow after each upgrade

**QWU Node Inventory** (what the monitor tracks):
| Node | Usage | Notes |
|------|-------|-------|
| httpRequest | 63 | Discord webhooks, API calls |
| code | 59 | JavaScript parsing |
| ssh | 56 | Running Python scripts |
| if | 54 | Conditional logic |
| scheduleTrigger | 47 | Cron scheduling |
| noOp | 39 | No-op endpoints |
| webhook | 11 | Incoming webhooks |
| respondToWebhook | 10 | Webhook responses |

**Directive:** See `005 Operations/Directives/n8n_version_management.md` for full process

**Workflow Publishing (n8n 2.x):**
n8n 2.x uses a publish/unpublish model instead of activate/deactivate:
```bash
# Publish a workflow (after import)
docker exec n8n n8n publish:workflow --id=<workflow_id>

# Unpublish (disable)
docker exec n8n n8n unpublish:workflow --id=<workflow_id>

# Restart required after publishing
cd ~/n8n && docker compose restart n8n
```

**Workflow Archiving:**
n8n has a native archive feature via the `isArchived` database column:
```bash
# Archive an old workflow
docker exec n8n-postgres psql -U n8n -d n8n -c \
  "UPDATE workflow_entity SET \"isArchived\" = true WHERE id = '<workflow_id>';"
```
Archived workflows are hidden from the main list but preserved for reference.

---

## Running Agent Jobs

### tmux for Persistent Sessions ⭐

**Why it matters**: When you disconnect from the workspace, running processes normally stop. tmux keeps your agents running even when you're not connected.

**Essential Commands:**

```bash
# Start a new named session
tmux new -s agents

# Detach from session (process keeps running)
Ctrl+B, then D

# List all sessions
tmux ls

# Reattach to a session
tmux attach -s agents

# Kill a session when done
tmux kill-session -s agents
```

**Multiple Windows Inside tmux:**

```bash
Ctrl+B, then C          # Create new window
Ctrl+B, then N          # Next window  
Ctrl+B, then P          # Previous window
Ctrl+B, then 0-9        # Jump to window by number
Ctrl+B, then ,          # Rename current window
```

**Best Practice for Overnight Jobs:**

1. Start a tmux session with a descriptive name: `tmux new -s lead-scraper`
2. Run your agent script
3. Detach: `Ctrl+B, then D`
4. Go to sleep 😴 (VM runs 24/7, no shutdown concerns)
5. Reconnect next day: `tmux attach -s lead-scraper`

---

## Overnight/Long-Running Jobs

### 24/7 Operation Mode

As of January 2026, the QWU Backoffice VM runs **24/7**. Auto-shutdown has been disabled to enable:
- Continuous n8n workflow execution
- Ezer email response handling at any hour
- Overnight batch processing jobs
- True autonomous operations

**Cost Trade-off:** ~$50-85/month (vs. ~$35-40 with auto-shutdown). Worth it for always-on automation.

### Server Maintenance

With 24/7 operation, we follow a maintenance schedule:

| Frequency | Task | How |
|-----------|------|-----|
| **Daily** | Health check | n8n workflow at 6 AM |
| **Weekly** | Scheduled restart | Sunday 3 AM Pacific |
| **Monthly** | Security updates review | Manual check of applied patches |
| **Quarterly** | Deep maintenance | Disk cleanup, Docker prune, log rotation |

See `server_maintenance.md` directive for full procedures.

---

## Mobile Access via Termux (Android) ⭐

Access your Azure VM from your phone... check on overnight agent runs from anywhere.

### Why This Matters

When you kick off a long-running agent job in tmux and go to bed, you can check on it from your phone without getting out of bed. 📱

### Installation (One-Time Setup)

**Important:** Don't use the Google Play Store version... it's outdated.

1. Install **F-Droid** from https://f-droid.org
2. Open F-Droid and install these four apps:
   - **Termux** (main terminal)
   - **Termux:API** (clipboard, notifications)
   - **Termux:Widget** (home screen shortcuts)
   - **Termux:Styling** (customize appearance)

### Initial Configuration

Open Termux and run:

```bash
# Update packages
pkg update && pkg upgrade -y

# Install essentials
pkg install openssh git termux-api nano curl netcat-openbsd -y

# Grant storage access
termux-setup-storage
```

### Generate SSH Key

```bash
ssh-keygen -t ed25519 -C "termux-mobile"
```

Press Enter for defaults. View your public key:

```bash
cat ~/.ssh/id_ed25519.pub
```

### Add Key to Azure VM

From another terminal connected to your VM, add the public key:

```bash
echo "YOUR_PUBLIC_KEY_HERE" >> ~/.ssh/authorized_keys
```

### Configure SSH Shortcut

Create the config file:

```bash
nano ~/.ssh/config
```

Add this (update IP if it changes):

```
Host qwu
    HostName <VM_IP_CLAUDE_DEV>
    User <VM_USER>
    IdentityFile ~/.ssh/id_ed25519
    ServerAliveInterval 60
    ServerAliveCountMax 3
```

Save (`Ctrl+O`, Enter, `Ctrl+X`) and set permissions:

```bash
chmod 600 ~/.ssh/config
```

### Daily Use

| Command | What It Does |
|---------|--------------|
| `ssh qwu` | Connect to Azure VM |
| `tmux ls` | Check running sessions |
| `tmux attach` | Jump into existing session |
| `tmux attach -t agents` | Attach to specific session |
| `Ctrl+B, D` | Detach (leaves session running) |
| `exit` | Disconnect from VM |

### Keyboard Tips

Termux shows an extra keys row. Useful shortcuts:
- **Volume Up + Q** = ESC
- **Volume Up + E** = CTRL
- Swipe left from right edge for drawer with more keys

### Troubleshooting

**"Connection timed out"**
- Rare with 24/7 operation, but could indicate network issue or VM restart. Check Azure Portal for status.

**"Connection refused"**
- Check if VM IP changed (it can change when stopped/started). Update `~/.ssh/config` with new IP.

**"Permission denied (publickey)"**
- Your key wasn't added to the VM. Re-run the `echo` command on the VM to add it.

---

## Obsidian + GitHub Integration: Unified Workspace

The QWU Backoffice uses a unified workspace architecture where the Obsidian vault and agent codebase live in the same repository. This allows you to edit agent code (directives, execution scripts) from Obsidian on any device.

### Architecture Overview

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│  Obsidian       │     │     GitHub      │     │    Azure VM     │
│  (Windows)      │◄───►│   (Full Repo)   │◄───►│  (Filtered)     │
│  Full vault     │     │                 │     │  Text files only│
└─────────────────┘     └─────────────────┘     └─────────────────┘
```

| Location | What it contains |
|----------|------------------|
| Obsidian (Windows) | Everything - full vault with all files |
| GitHub | Everything - complete repository |
| Azure VM | Filtered - only what agents need (no images, canvas files, etc.) |

### Local Vault Location

```
C:\Users\<USERNAME>\qwu_backOffice
```

This folder serves as both:
- Your Obsidian vault (open in Obsidian as a vault)
- Your git repository (syncs to GitHub)

### Obsidian Git Plugin Settings

The `obsidian-git` community plugin handles automatic sync:

| Setting | Value |
|---------|-------|
| Auto commit-and-sync interval | 10 minutes |
| Auto pull interval | 10 minutes |
| Pull on startup | ON |
| Push on commit-and-sync | ON |
| Pull on commit-and-sync | ON |

### Manual Sync Commands

In Obsidian, use the Command Palette (`Ctrl+P`):
- **Obsidian Git: Commit all changes** - Save current changes
- **Obsidian Git: Push** - Upload to GitHub
- **Obsidian Git: Pull** - Download from GitHub

### .gitignore Configuration

Located at the root of the vault, excludes files that shouldn't sync:

```
# Obsidian workspace cache & plugins
.obsidian/workspace.json
.obsidian/workspace-mobile.json
.obsidian/plugins/

# Smart Connections plugin data
.smart-env/
.smart-connections/
smart-chats/

# Trash & temporary files
.trash/
.tmp.driveupload/
.tmp/

# Supervisor escalation outputs (legacy safety net — now routed to ___Supervisor_Escalations/)
000 Inbox/___Tasks/SUPERVISOR-*.md
000 Inbox/___Supervisor_Escalations/

# Environment and credentials (NEVER commit)
.env
.credentials/

# Node.js
node_modules/

# Python
.venv/
__pycache__/
*.pyc

# IDE & OS
.vscode/
.DS_Store
Thumbs.db
```

---

## Sparse Checkout: Filtering Files on Azure VM

The Azure VM uses **sparse checkout** to only download files that agents need. This excludes images, canvas files, and other non-text content.

### How It Works

Git's sparse checkout feature tells the VM: "Only pull these types of files." The full repo stays on GitHub, but the VM only sees what's relevant for agent work.

### Sparse Checkout Configuration File

Located at: `~/qwu_backOffice/.git/info/sparse-checkout`

**Current configuration:**

```
# Include everything by default
/*

# ===================
# EXCLUDE: Obsidian visual/UI files
# ===================
!*.canvas
!*.excalidraw
!/Excalidraw/

# ===================
# EXCLUDE: Obsidian plugin data (not needed by agents)
# ===================
!/.smart-connections/
!/.smart-env/
!/smart-chats/
!/www.help.obsidian.md/
!/{{savePath}}/

# ===================
# EXCLUDE: Large media files (agents work with text)
# ===================
!*.jpg
!*.jpeg
!*.png
!*.gif
!*.webp
!*.mp4
!*.mp3
!*.pdf

# ===================
# EXCLUDE: Misc
# ===================
!/Omnivore/
!/Clippings/
```

### Editing Sparse Checkout Rules

**To add or remove exclusions:**

```bash
nano ~/qwu_backOffice/.git/info/sparse-checkout
```

**After editing, apply changes:**

```bash
cd ~/qwu_backOffice
git sparse-checkout reapply
```

### Sparse Checkout Syntax

| Pattern | Meaning |
|---------|---------|
| `/*` | Include everything |
| `!*.canvas` | Exclude all .canvas files |
| `!/Excalidraw/` | Exclude the Excalidraw folder |
| `!*.jpg` | Exclude all .jpg files |

The `!` prefix means "exclude this pattern."

### Verifying Sparse Checkout

**Check what's included:**
```bash
ls -la ~/qwu_backOffice
```

**Verify specific files are excluded:**
```bash
find ~/qwu_backOffice -name "*.canvas" 2>/dev/null
# Should return nothing if working correctly
```

---

## Syncing Workflow

### Your Daily Workflow (Obsidian)

1. Open Obsidian (it auto-pulls on startup)
2. Edit notes, directives, execution scripts
3. Auto-commits every 10 minutes, or manually via Command Palette
4. Changes sync to GitHub automatically

### Agent Workflow (Azure VM)

Before agents read/write:
```bash
cd ~/qwu_backOffice
git pull
```

After agents write outputs:
```bash
git add .
git commit -m "Agent work log: $(date +%Y-%m-%d)"
git push
```

These outputs will appear in your Obsidian vault on the next sync!

### Handling Sync Conflicts

If you edit on multiple devices simultaneously, you may get merge conflicts.

**To resolve:**
```bash
git status                    # See conflicted files
git diff                      # See the conflicts
nano <conflicted-file>        # Edit to resolve
git add <conflicted-file>
git commit -m "Resolved merge conflict"
git push
```

**Prevention tip:** Let auto-sync run before switching devices.

---

## Claude Code: Modes and Commands

Claude Code is a command-line AI assistant that can read, write, and execute code directly on your system.

### Starting Claude Code

```bash
cd ~/qwu_backOffice
source .env
claude
```

### Operating Modes

| Mode | How to activate | What it can do |
|------|-----------------|----------------|
| **Normal** | Default when you start | Read files, write files, run commands, full power |
| **Plan Mode** | Type `/plan` | Think and plan only, NO file changes or commands |
| **Auto-accept** | Start with `claude --dangerously-skip-permissions` | Runs without asking permission for each action |

### Normal Mode (Default)

Claude asks permission before:
- Writing/editing files
- Running terminal commands
- Installing packages

**Best for:** Learning, careful work, when you want to review each step.

### Plan Mode

Toggle on/off by typing `/plan` inside Claude Code.

Claude will:
- ✅ Read files
- ✅ Think through problems
- ✅ Create detailed plans
- ❌ NOT write any files
- ❌ NOT run any commands

**Best for:** Complex problems where you want to think before acting. Architecture decisions. Reviewing what SHOULD happen before doing it.

### Auto-accept Mode

```bash
claude --dangerously-skip-permissions
```

Claude executes without asking "May I run this command?" each time.

**Best for:** Trusted, repetitive tasks. Overnight agent runs. When you've already validated the workflow.

**⚠️ Use with caution** - it will do exactly what it decides to do!

### Useful Commands Inside Claude Code

| Command | What it does |
|---------|--------------|
| `/help` | Show all commands |
| `/plan` | Toggle plan mode |
| `/clear` | Clear conversation history |
| `/compact` | Summarize conversation to save context |
| `/cost` | Show token usage and cost |
| `/quit` or `Ctrl+C` | Exit Claude Code |

### Tips for Effective Use

1. **Start in Normal Mode** until you're comfortable with how Claude operates
2. **Use Plan Mode** before tackling complex refactors or new features
3. **Be specific** in your requests - Claude works better with clear goals
4. **Review changes** before approving in Normal Mode
5. **Use Auto-accept** only for well-tested, repetitive workflows

### Agent Memory Architecture

Claude Code maintains persistent memory across conversations through a layered system:

**Always loaded (every conversation):**
- `CLAUDE.md` — Operating manual, conventions, infrastructure access (~500 lines)
- `MEMORY.md` — High-consequence behavioral rules, mission/language standards, topic file index (~104 lines, limit 200)

**On-demand (loaded when domain work starts via Domain Start Protocol):**

| Topic File | Trigger | Purpose |
|-----------|---------|---------|
| `memory/l4g.md` | L4G work | Fundraiser behavioral notes, vault pointers |
| `memory/bni.md` | BNI work | Pre-flight checklist, roster rules |
| `memory/email_patterns.md` | Email tasks | Outlook draft rule, TIG's style |
| `memory/content_pipeline.md` | Video/YouTube | Script inventory, output locations |
| `memory/lovable.md` | App building | Vite gotchas, placeholder key warning |
| `memory/llm_api.md` | Model config | OpenRouter parameter mapping |
| `memory/web_design.md` | Visual design | RevSlider, Spline, frontend stack |
| `memory/wordpress.md` | WPMU/Divi | System Status pointer |
| `memory/tool_wisdom_libraries.md` | TWL work | Standard overview, coverage stats |

**Key principles:**
- MEMORY.md contains behavioral rules (what I get wrong). Topic files contain domain-specific notes + vault pointers.
- Topic files reference vault files (System Status, Entities, Directives) but never copy their content.
- Line budgets enforced at session wrap-up: MEMORY.md < 180 lines, topic files < 50 lines each.
- Domain Start Protocol: read System Status file + topic file before beginning domain-scoped work.
- Multi-session safe: sessions are domain-scoped, topic files are domain-scoped, parallel writes hit different files.

**Context window best practice:** Manually clear conversations at natural breakpoints (task completion, domain switches) rather than waiting for auto-compaction. Use `/session-wrap-up` before clearing. The persistent file system is designed for clean breaks.

### QCM — QWU Context Manager

QCM is a homegrown context management system that automatically recovers working state after context compaction. Built as 4 Python hook scripts with zero external dependencies (no npm packages, no MCP servers).

**What it solves:** During long sessions, Claude Code's context window fills and compacts. When this happens, Claude loses track of which files were being edited, what tasks remained, what decisions were made, and what errors were diagnosed. QCM captures all of this automatically and restores it after compaction.

**Architecture:**

| Component | Hook Event | Purpose |
|-----------|-----------|---------|
| `qcm_event_logger.py` | PostToolUse, UserPromptSubmit | Logs every tool call and user message to SQLite, classified by priority (P1-P4) |
| `qcm_snapshot_builder.py` | Stop | Builds a <=2KB priority-budgeted markdown snapshot from events |
| `qcm_session_restore.py` | SessionStart | Injects the snapshot as additionalContext after compaction |
| `qcm_output_compressor.py` | PostToolUse (Bash) | Compresses large outputs (>3KB) — saves full output to disk, returns summary to context |

**Priority tiers:**

| Priority | What gets captured | Snapshot budget |
|----------|-------------------|----------------|
| P1 (critical) | User requests, project focus, errors | 800 bytes (guaranteed) |
| P2 (high) | Decisions, script runs, directive reads | 600 bytes |
| P3 (medium) | File edits | 400 bytes |
| P4 (low) | File reads, searches | Dropped from snapshot |

**File locations:**
- Hook scripts: `.claude/hooks/qcm_*.py`
- Session events DB: `.tmp/context/session_events.db` (SQLite, WAL mode)
- Snapshots: `.tmp/context/snapshots/snapshot_{session_id}.md`
- Compressed outputs: `.tmp/context/compressed/{hash}.txt`
- Hook configuration: `.claude/settings.json` (hooks section)
- Directive: `005 Operations/Directives/context_management.md`

**Security design:** Zero external dependencies (Python stdlib only), no network access, no credential access, fail-open (never blocks Claude), all data in `.tmp/` (ephemeral). Built in-house after security analysis rejected context-mode (npm supply chain risk with 30+ API keys on the VM).

**Debugging:**
```bash
# Check events
python3 -c "import sqlite3; c=sqlite3.connect('.tmp/context/session_events.db'); [print(f'P{r[0]} [{r[1]}] {r[2]}') for r in c.execute('SELECT priority, category, summary FROM events ORDER BY id DESC LIMIT 10')]"

# Check snapshot
cat .tmp/context/snapshots/snapshot_*.md

# Nuclear reset (safe)
rm -rf .tmp/context/
```

---

## Quick Reference Sheets

Printable reference cards for efficient terminal work. These are designed to be printed and kept nearby while learning.

### Terminal Copy/Paste (The Big One!)

Coming from Windows, this is the #1 gotcha:

| Action | Shortcut | Why Different? |
|--------|----------|----------------|
| Copy | `Ctrl+Shift+C` | `Ctrl+C` kills processes |
| Paste | `Ctrl+Shift+V` | Matches copy shortcut |
| Paste (alt) | `Shift+Insert` | Works everywhere |

### Line Editing (Readline)

Navigate and edit commands without arrow keys:

| Action | Shortcut |
|--------|----------|
| Start of line | `Ctrl+A` |
| End of line | `Ctrl+E` |
| Back one word | `Alt+B` or `Ctrl+←` |
| Forward one word | `Alt+F` or `Ctrl+→` |
| Delete word before cursor | `Ctrl+W` |
| Delete word after cursor | `Alt+D` |
| Delete to end of line | `Ctrl+K` |
| Delete to start of line | `Ctrl+U` |
| Undo | `Ctrl+_` |
| Clear screen | `Ctrl+L` |

### Command History

| Action | Shortcut |
|--------|----------|
| Previous command | `↑` or `Ctrl+P` |
| Next command | `↓` or `Ctrl+N` |
| Search history (reverse) | `Ctrl+R` then type |
| Cancel search | `Ctrl+G` |
| Run last command | `!!` |
| Run last command with sudo | `sudo !!` |
| Last argument of previous | `!$` |

### Process Control

| Action | Shortcut |
|--------|----------|
| Cancel/interrupt | `Ctrl+C` |
| Suspend (background) | `Ctrl+Z` |
| End input / exit | `Ctrl+D` |
| Resume suspended | `fg` |

### tmux Quick Reference

| Action | Shortcut |
|--------|----------|
| New session | `tmux new -s name` |
| Detach | `Ctrl+B`, then `D` |
| List sessions | `tmux ls` |
| Attach | `tmux attach -s name` |
| Kill session | `tmux kill-session -s name` |
| New window | `Ctrl+B`, then `C` |
| Next window | `Ctrl+B`, then `N` |
| Previous window | `Ctrl+B`, then `P` |
| Window by number | `Ctrl+B`, then `0-9` |
| Rename window | `Ctrl+B`, then `,` |
| Split horizontal | `Ctrl+B`, then `"` |
| Split vertical | `Ctrl+B`, then `%` |
| Switch panes | `Ctrl+B`, then arrow |

### Claude Code Commands

| Command | What it does |
|---------|--------------|
| `/help` | Show all commands |
| `/plan` | Toggle plan mode |
| `/clear` | Clear conversation |
| `/compact` | Summarize to save context |
| `/cost` | Show token usage |
| `/quit` or `Ctrl+C` | Exit |

### Nano Editor (Quick Edits)

| Action | Shortcut |
|--------|----------|
| Save | `Ctrl+O`, then Enter |
| Exit | `Ctrl+X` |
| Cut line | `Ctrl+K` |
| Paste | `Ctrl+U` |
| Search | `Ctrl+W` |
| Go to line | `Ctrl+_` |

### Git Essentials

| Command | What it does |
|---------|--------------|
| `git status` | See what changed |
| `git pull` | Get latest from remote |
| `git add .` | Stage all changes |
| `git commit -m "msg"` | Commit with message |
| `git push` | Send to remote |
| `git log --oneline -5` | Recent commits |
| `git diff` | See unstaged changes |

### VS Code Remote Shortcuts

| Action | Shortcut |
|--------|----------|
| Command Palette | `Ctrl+Shift+P` |
| Terminal | `` Ctrl+` `` |
| New terminal | `` Ctrl+Shift+` `` |
| File search | `Ctrl+P` |
| Find in files | `Ctrl+Shift+F` |
| Close tab | `Ctrl+W` |

### Termux (Android) Tips

| Action | Method |
|--------|--------|
| ESC key | `Volume Up + Q` |
| CTRL key | `Volume Up + E` |
| Extra keys | Swipe left from right edge |
| Tab completion | `Tab` key on extra row |

---

## DOE Architecture & Skills System

The QWU Backoffice uses a 3-layer DOE (Directive-Orchestration-Execution) architecture.

### Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│  LAYER 1: DIRECTIVE (What to do)                                │
│  Natural language instructions in Markdown                      │
│  Location: 005 Operations/Directives/                           │
├─────────────────────────────────────────────────────────────────┤
│  LAYER 2: ORCHESTRATION (Decision making)                       │
│  AI agent reads directives, makes routing decisions             │
│  Handles errors, asks for clarification, updates directives     │
├─────────────────────────────────────────────────────────────────┤
│  LAYER 3: EXECUTION (Doing the work)                            │
│  Deterministic Python scripts                                   │
│  Location: 005 Operations/Execution/                            │
└─────────────────────────────────────────────────────────────────┘
```

| Layer | Location | Purpose |
|-------|----------|---------|
| Directive | `005 Operations/Directives/` | SOPs in Markdown defining goals, inputs, tools, outputs |
| Orchestration | AI Agent | Intelligent routing, error handling, learning |
| Execution | `005 Operations/Execution/` | Deterministic Python scripts for API calls, data processing |

### Key Principles

- **Check for tools first** - Before writing a script, check if one exists
- **Self-anneal when things break** - Fix, test, update directive
- **Update directives as you learn** - Directives are living documents
- **Deliverables in cloud** - Use Google Sheets, Slides, etc. for outputs
- **Local files for processing only** - Everything in `.tmp/` is temporary

### Skills System

Skills provide domain-specific knowledge and capabilities that agents reference. Each skill has a `SKILL.md` with YAML frontmatter (`name` + `description`) that controls when Claude triggers it.

**QWF Program & Voice Skills:**

| Skill | Purpose | Dependencies |
|-------|---------|-------------|
| `qwf-brand-voice` | Voice profiles for all QWF communications (TIG, WOH, L4G, etc.) | None |
| `qwf-programs` | Program context, audience, sensitivities for all QWF programs | None |

**Operations & Audit Skills:**

| Skill | Purpose | Dependencies |
|-------|---------|-------------|
| `system-audit` | Comprehensive system architecture audit | None |
| `session-wrap-up` | End-of-session documentation sync checklist | None |
| `process-zoom` | Meeting Intelligence Pipeline for Zoom recordings | FFmpeg |
| `capture-triage` | GTD-style inbox triage for Master Capture | None |
| `vista-social` | Social media management via Vista Social API | Python |
| `tool-wisdom` | Query tool-specific wisdom from wisdom.db | None |

**Lead Generation Skills:**

| Skill | Purpose | Dependencies |
|-------|---------|-------------|
| `lead-generation` | Multi-source lead generation (LinkedIn, Maps, Apollo, etc.) | Python |
| `linkedin-scraping` | LinkedIn Sales Navigator scraping | Apify |
| `gmaps-scraping` | Google Maps business scraping | Apify |
| `apollo-scraping` | Apollo.io lead scraping | Apify |
| `lead-enrichment` | Enrich lead lists with emails, reviews, company data | Python |
| `email-enrichment` | Email lookup via Anymail Finder | API key |
| `review-enrichment` | Google reviews + AI sentiment analysis | Python |
| `friendly-name-enrichment` | Clean up formal company names to brand names | LLM |

**Visual & Creative Skills (adapted from Nate Herk / AI Automation Society):**

| Skill | Purpose | Dependencies | Cost |
|-------|---------|-------------|------|
| `excalidraw-diagram` | Editable `.excalidraw` JSON diagrams | None | Free |
| `excalidraw-visuals` | Hand-drawn PNG images via Kie.ai API | `KIE_AI_API_KEY`, Node.js | ~$0.02-0.09/image |
| `nano-banana-images` | Hyper-realistic photos via Kie.ai Nano Banana 2 | `KIE_AI_API_KEY`, Python | ~$0.04-0.09/image |
| `frontend-design` | Anti-AI-slop design guidelines for distinctive UIs | None | Free |
| `video-to-website` | Scroll-driven animated websites from video files | FFmpeg | Free |

```
.claude/skills/
├── qwf-brand-voice/          # Voice profiles (TIG, WOH, L4G, etc.)
├── qwf-programs/             # Program context and audience
├── system-audit/             # System architecture audit
├── session-wrap-up/          # End-of-session checklist
├── process-zoom/             # Meeting intelligence pipeline
├── capture-triage/           # Inbox triage
├── vista-social/             # Social media management
├── tool-wisdom/              # Wisdom database queries
├── lead-generation/          # Multi-source leads
├── linkedin-scraping/        # LinkedIn Sales Navigator
├── gmaps-scraping/           # Google Maps businesses
├── apollo-scraping/          # Apollo.io leads
├── lead-enrichment/          # Lead data enrichment
├── email-enrichment/         # Email lookup
├── review-enrichment/        # Google reviews
├── friendly-name-enrichment/ # Company name cleanup
├── excalidraw-diagram/       # Editable diagrams (JSON)
├── excalidraw-visuals/       # Hand-drawn PNGs (Kie.ai)
├── nano-banana-images/       # Hyper-realistic photos (Kie.ai)
├── frontend-design/          # Design guidelines
└── video-to-website/         # Scroll-driven animated sites
```

### Agent Templates

Agents live in `.claude/agents/`:

```
.claude/agents/
├── qwf-master-router.md      # Routes incoming work
├── qwf-creative-director.md  # Oversees creative production
├── qwf-writer.md             # Content creation
└── qwf-visual-designer.md    # Graphics execution
```

### MCP Server Configuration

The workspace uses MCP (Model Context Protocol) servers for tool access. MCP servers are configured at the **project level** in `.mcp.json` (gitignored, contains tokens) and are **opt-in per session** to conserve memory.

**File:** `.mcp.json` (project root, NOT committed to git)

```json
{
  "mcpServers": {
    "discord-mcp": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "discord-mcp@latest"],
      "env": { "DISCORD_BOT_TOKEN": "..." }
    },
    "apify": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@apify/actors-mcp-server"],
      "env": { "APIFY_TOKEN": "..." }
    }
  }
}
```

**Settings:** `.claude/settings.local.json` has `enableAllProjectMcpServers: false` — new sessions do NOT auto-spawn MCP servers. Enable per-session via `/mcp` when needed.

**Why opt-in:** Each MCP server spawns ~3 Node.js processes (~160 MB). With 5 concurrent sessions, auto-spawning Discord MCP alone consumed 786 MB. Most sessions don't need Discord access, so opt-in saves significant memory on the 16 GB VM.

**To enable Discord MCP in a session:** Use the `/mcp` command within the session to connect.

---

## Supervisor Architecture

The QWU Backoffice uses five domain-specific **supervisors** that orchestrate automated script execution across the entire system. Each supervisor owns a domain, runs its scripts on a schedule via n8n, logs results to SQLite, and escalates failures to Discord.

### Why Supervisors Exist

Before supervisors, a single router agent handled all automation. As the system grew to 60+ scripts, the router became a bottleneck — errors compounded, scheduling conflicted, and failures in one domain could block others. The supervisor architecture splits responsibility into five independent domains that run in parallel.

### The Five Supervisors

| Supervisor | Domain | Schedule | Scripts |
|------------|--------|----------|---------|
| **Operations** | System health, briefings, audits | 6 AM + 6 PM Pacific | 7 |
| **Lead Intelligence** | Lead scraping, enrichment, BNI | Daily 6 AM (check mode) | 24 |
| **Content Pipeline** | Content queue, expert monitoring, YouTube, wisdom | Every 30 min (queue) + Daily 7 AM (full) | 21 |
| **Relationship Intelligence** | Email, calendar, meetings, Ezer AI, BNI 1-2-1 | Every 15 min + Daily 9 PM + Thu 12 PM | 36 |
| **Student Programs** | MP tracker, program inquiries | Weekly Mon 9 AM | 2 |

### How It Works

```
┌──────────────┐     ┌────────────────────┐     ┌──────────────────┐
│   n8n         │────▶│   Supervisor .py    │────▶│   Scripts         │
│   (schedule)  │     │   (orchestrator)    │     │   (deterministic) │
└──────────────┘     └────────────────────┘     └──────────────────┘
                              │
                     ┌────────┴────────┐
                     ▼                 ▼
              ┌──────────┐     ┌──────────────┐
              │ SQLite DB │     │ Discord Alert │
              │ (logging) │     │ (escalation)  │
              └──────────┘     └──────────────┘
```

1. **n8n triggers** the supervisor on schedule (SSH to backoffice VM)
2. **Supervisor checks** the cross-domain queue for tasks from other supervisors
3. **Supervisor runs** its pipeline scripts in sequence
4. **Each script result** is logged to the supervisor's SQLite database
5. **On failure**, the supervisor retries (up to 2x), then escalates to Discord `#supervisor-alerts`
6. **On completion**, the supervisor logs the run summary and notifies Discord

### Key Files

| File | Purpose |
|------|---------|
| `005 Operations/Execution/supervisor_base.py` | Abstract base class all supervisors inherit from |
| `005 Operations/Execution/operations_supervisor.py` | Operations & Admin supervisor |
| `005 Operations/Execution/lead_intelligence_supervisor.py` | Lead Intelligence supervisor |
| `005 Operations/Execution/content_pipeline_supervisor.py` | Content Pipeline supervisor |
| `005 Operations/Execution/relationship_intelligence_supervisor.py` | Relationship Intelligence supervisor |
| `005 Operations/Execution/student_programs_supervisor.py` | Student Programs supervisor |
| `005 Operations/Execution/generate_supervisor_dashboard.py` | Health dashboard generator |
| `005 Operations/Execution/error_handling.py` | Centralized error handling: Discord alerts + escalation file creation (v2.1.0) |
| `005 Operations/Dashboards/Supervisor-Health.md` | Generated health dashboard |
| `005 Operations/Workflows/supervisor-rollback.md` | Emergency rollback procedures |

### Databases

Each supervisor maintains its own SQLite database in `005 Operations/Data/`:

| Database | Tables |
|----------|--------|
| `005 Operations/Data/operations_supervisor.db` | `supervisor_runs`, `script_executions` |
| `005 Operations/Data/lead_intelligence_supervisor.db` | Same schema |
| `005 Operations/Data/content_pipeline_supervisor.db` | Same schema |
| `005 Operations/Data/relationship_intelligence_supervisor.db` | Same schema |
| `005 Operations/Data/student_programs_supervisor.db` | Same schema |

### Escalation Routing

When a supervisor detects a failure requiring human attention, it escalates via two channels:
1. **Discord `#supervisor-alerts`** — Immediate visibility (via `escalate_to_discord()`)
2. **Escalation file** — Audit trail in `000 Inbox/___Supervisor_Escalations/` (via `escalate_to_task()` in `error_handling.py` v2.1.0)

These escalation files are intentionally kept **separate** from `___Tasks/` so they don't pollute the user's HQ Command Center task list. As defense-in-depth, `sync_hq_tasks.py` v1.5.0 also skips any files with a `SUPERVISOR-` prefix.

### Running Supervisors Manually

```bash
# Run with JSON output (used by n8n)
python "005 Operations/Execution/operations_supervisor.py" --json

# Run specific pipeline
python "005 Operations/Execution/content_pipeline_supervisor.py" --pipeline queue --json

# Dry run (shows what would execute)
python "005 Operations/Execution/lead_intelligence_supervisor.py" --dry-run --json

# Run a single script through the supervisor
python "005 Operations/Execution/content_pipeline_supervisor.py" --script newsletter_monitor.py --json
```

### Cross-Supervisor Queue

Supervisors can create tasks for each other via `000 Inbox/___Supervisor_Queue/`. Tasks are YAML-frontmatter Markdown files with `from`, `to`, and `priority` fields. The receiving supervisor picks up tasks on its next run and moves completed tasks to `000 Inbox/___Supervisor_Completed/`.

### Health Dashboard

Generate a health dashboard at any time:

```bash
# Quick summary
python "005 Operations/Execution/generate_supervisor_dashboard.py"

# Full markdown dashboard
python "005 Operations/Execution/generate_supervisor_dashboard.py" --markdown

# JSON for programmatic use
python "005 Operations/Execution/generate_supervisor_dashboard.py" --json
```

### n8n Workflows

Each supervisor has a corresponding n8n workflow:

| Supervisor | Workflow ID | Webhook Trigger |
|------------|-------------|-----------------|
| Operations | <WORKFLOW_ID> | *(schedule only)* |
| Lead Intelligence | <WORKFLOW_ID> | `POST /webhook/lead-intelligence-trigger` |
| Content Pipeline | <WORKFLOW_ID> | `POST /webhook/content-pipeline-trigger` |
| Relationship Intelligence | <WORKFLOW_ID> | `POST /webhook/rel-intel-trigger` |
| Student Programs | <WORKFLOW_ID> | `POST /webhook/student-programs-trigger` |

### Troubleshooting

**Dashboard shows "CRITICAL" but supervisors are running:**
Supervisors with `ON_DEMAND_SCRIPTS` sets (Content Pipeline v1.1.0+, Lead Intelligence v1.1.0+) automatically skip scripts that need user-provided inputs during automated runs. If you still see failures, check for scripts missing from the `ON_DEMAND_SCRIPTS` set — they may need required arguments (`--sheet-url`, `--json-file`, etc.) that the supervisor can't provide. Fix: add the script to `ON_DEMAND_SCRIPTS` in the supervisor.

**A supervisor isn't running on schedule:**
1. Check n8n: `ssh <VM_USER>@qwu-n8n "docker exec n8n n8n list:workflow"`
2. Verify the workflow is published (not just active)
3. Check recent executions in n8n UI at https://n8n.quietlyworking.org

**Script failures escalating to Discord too often:**
The supervisor retries each script up to 2 times before escalating. If a script consistently fails, either fix the script or remove it from the supervisor's script list until it's ready.

**Cross-supervisor tasks not being picked up:**
Check `000 Inbox/___Supervisor_Queue/` for stuck tasks. Verify the `to:` field in the YAML frontmatter matches the receiving supervisor's `domain_name`.

**Rolling back to legacy workflows:**
Follow `005 Operations/Workflows/supervisor-rollback.md` for emergency rollback procedures. Legacy workflows are deactivated (not deleted) and can be re-enabled with a single command.

---

## Morning Briefing System ⭐

The Morning Briefing is an automated daily summary that surfaces what matters when you begin work.

### What It Shows

| Section | Source |
|---------|--------|
| Today's Schedule | Google Calendar (Main + Alerts & Reminders calendars) |
| Priority Tasks | `___Tasks/` files with `priority: critical` or `high` |
| Due Today | Tasks with `due:` matching today's date |
| Overdue | Tasks past their due date |
| Blocked | Tasks with `status: blocked` or `blocked_by:` set |
| Needs Decision | Items in `___Review/` folder |

### Running the Briefing

**Manual (via Claude Code):**
```
Let's do a morning briefing
```

**Script (direct):**
```bash
cd ~/qwu_backOffice && source .env
python "005 Operations/Execution/morning_briefing.py"
```

**Options:**
```bash
--dry-run    # Preview without writing
--discord    # Also post to Discord (default: daily note only)
--no-daily   # Skip daily note append
--json       # Output JSON for n8n
```

### Output Locations

| Output | Location |
|--------|----------|
| Daily Note | `001 Daily/YYYY/YYYYMMDD.md` (appended) |
| Discord | #daily-digest channel (if `--discord` flag used) |
| Log | `.tmp/logs/YYYY-MM-DD.log` |

### Project Task Scanning

The briefing also scans all active projects for tasks:

1. **Active Tasks section** - Items in `## Active Tasks` within project `_Overview.md` files
2. **Incomplete checkboxes** - Any `- [ ]` items in project files

Project tasks inherit the project's priority level.

### Day Boundary Feature

**Late-night work handling:** If you're working past midnight (before 4 AM), the briefing logs to "yesterday's" date. This prevents late-night sessions from bleeding into the next day's records.

```
2:00 AM on Jan 8 → logs to Jan 7's daily note
5:00 AM on Jan 8 → logs to Jan 8's daily note
```

This feature is powered by the [Canonical Datetime System](#canonical-datetime-system) via the `effective_date()` function in `qwu_datetime.py`.

---

## Daily Summary System ⭐

End-of-session summaries capture completed work, decisions, and next actions for institutional memory.

### When to Use

Run the summary when wrapping up a work session:
```
Let's summarize this session
```
or
```
Wrap up for the day
```

### What Gets Captured

| Element | Purpose |
|---------|---------|
| Tasks Completed | What was accomplished with goal alignment |
| Strategic Context | How work fits larger plans |
| Key Decisions | Decisions made with reasoning and implications |
| Files Changed | Git diff summary |
| Blockers & Resolutions | Issues hit and how they were resolved |
| Apify Costs | 30-day Apify spend with per-actor breakdown (via `collect_apify_costs.py`) |
| Open Questions | Unresolved items for future sessions |
| Proposed Next Actions | Prioritized by goal alignment |

### Output Format

```markdown
## Session Summary - 2026-01-08

### What Was Accomplished
- Implemented morning briefing calendar integration - *Advances: M5 milestone*
- Fixed inbox processing bug - *Advances: Automation reliability*

### Key Decisions Made
| Decision | Reasoning | Implications |
|----------|-----------|--------------|
| Use day boundary | Prevents late-night date confusion | Work before 4am counts as yesterday |

### Proposed Next Actions
1. **[High]** Complete user manual update *(Advances: Documentation)*
2. **[Medium]** Test calendar integration edge cases
```

### Integration Points

The summary system can optionally read:
- `002 Projects/_Goals and Priorities.md` - For goal alignment
- `002 Projects/_Current Roadmap.md` - For roadmap context

---

## Google Calendar Integration

The backoffice integrates with Google Calendar for morning briefings and scheduling awareness.

### Configured Calendars

| Calendar | Purpose | Environment Variable |
|----------|---------|---------------------|
| Main | Appointments, day blocking | `GOOGLE_CALENDAR_MAIN` |
| Alerts & Reminders | Alerts, reminders, payment schedules | `GOOGLE_CALENDAR_ALERTS` |
| Timeslots | Future: goal time blocks | `GOOGLE_CALENDAR_TIMESLOT` |

### Setup Requirements

1. **Google Cloud Service Account** with Calendar API enabled
2. **Credentials JSON file** stored securely on VM
3. **Calendar sharing** with service account email

### Environment Variables

```bash
GOOGLE_CALENDAR_CREDENTIALS="/path/to/service-account.json"
GOOGLE_CALENDAR_MAIN="<ADMIN_EMAIL>"
GOOGLE_CALENDAR_ALERTS="bills-calendar-id@group.calendar.google.com"
GOOGLE_CALENDAR_TIMESLOT="timeslot-calendar-id@group.calendar.google.com"
```

### Testing Calendar Integration

```bash
cd ~/qwu_backOffice && source .env
python "005 Operations/Execution/calendar_events.py" --dry-run  # Validate credentials
python "005 Operations/Execution/calendar_events.py"            # Fetch today's events
python "005 Operations/Execution/calendar_events.py" --json     # JSON output
```

### Google Calendar API Timestamp Gotcha (RFC3339)

The Google Calendar API requires **RFC3339 timestamps with explicit timezone offset** for `timeMin`/`timeMax` parameters — not bare ISO 8601 timestamps. This is a subtle but critical distinction:

| Format | Example | Works? |
|--------|---------|--------|
| RFC3339 with offset | `2026-02-28T00:00:00-08:00` | Yes |
| RFC3339 with Z (UTC) | `2026-02-28T00:00:00Z` | Yes |
| Bare ISO 8601 | `2026-02-28T00:00:00` | **No — 400 Bad Request** |

When building Supabase Edge Functions (TypeScript/Deno) that call Google Calendar API, always include the timezone offset. For Pacific time, calculate the offset dynamically to handle DST:

```typescript
// Determine Pacific offset (PST = -08:00, PDT = -07:00)
const jan = new Date(now.getFullYear(), 0, 1).getTimezoneOffset();
const jul = new Date(now.getFullYear(), 6, 1).getTimezoneOffset();
const stdOffset = Math.max(jan, jul);
const isDST = now.getTimezoneOffset() < stdOffset;
const tzOffset = isDST ? '-07:00' : '-08:00';

// Build RFC3339 timestamp
const timeMin = `${year}-${month}-${day}T00:00:00${tzOffset}`;
```

This was the root cause of the HQ Command Center calendar edge function failure (Feb 2026). AI code generators (including Lovable) tend to produce bare timestamps without offsets.

---

## Google Docs Sync System

The backoffice supports two-way synchronization between Obsidian markdown files and Google Docs, enabling external collaboration while preserving Obsidian as the primary editing environment.

### Use Case

Share documents with non-technical collaborators (advisors, board members, partners) via Google Docs while maintaining source-of-truth in Obsidian. Format conversion ensures readers see native Google Docs formatting—not raw Markdown or YAML frontmatter.

### Architecture

```
┌─────────────────┐        ┌─────────────────┐        ┌─────────────────┐
│   Obsidian      │  push  │   Google Docs   │  edit  │   Collaborator  │
│   (Markdown)    │───────►│   (Native fmt)  │◄───────│   (Browser)     │
│                 │◄───────│                 │        │                 │
└─────────────────┘  pull  └─────────────────┘        └─────────────────┘
```

**Key Design Decisions:**
- **Bidirectional sync** via `revisionId` tracking (v1.1.0) — auto-detects remote edits and pulls them
- Google Docs wins conflicts (Obsidian backed up before overwriting)
- YAML frontmatter stripped from Google Docs (readers never see it)
- Obsidian syntax converted to readable format (wiki-links → plain text)
- 15-minute automated sync via n8n

### Enabling Sync on a File

Add YAML frontmatter to opt-in:

```yaml
---
title: "QWU Backoffice User Manual [PUBLIC]"
google_doc_sync: true
---
```

After first sync, additional fields are auto-populated:

```yaml
---
title: "Document Title"
google_doc_sync: true
google_doc_id: 1Abc123XyZ...           # Auto-populated
google_doc_last_sync: '2026-01-10T10:30:00-08:00'  # Auto-updated
---
```

### Format Conversion

**Push: Obsidian → Google Docs**

| Obsidian | Google Docs |
|----------|-------------|
| `# Heading` | Native Heading 1 |
| `**bold**` | **Bold text** |
| `*italic*` | *Italic text* |
| `- bullet` | Native bullet list |
| `[[Page Name]]` | Plain text "Page Name" |
| `#tag` | Removed |
| `> [!callout]` | Bold header |
| YAML frontmatter | Stripped (hidden) |
| `[link](url)` | Native hyperlink |

**Pull: Google Docs → Obsidian**

| Google Docs | Obsidian |
|-------------|----------|
| Heading 1 | `# Heading` |
| Bold | `**text**` |
| Hyperlink | `[text](url)` |
| Original YAML | Preserved from backup/state |

### Running Sync Manually

```bash
cd ~/qwu_backOffice && source .env

# Dry run - see what would sync
python "005 Operations/Execution/sync_gdocs.py" --dry-run

# Sync all enabled files
python "005 Operations/Execution/sync_gdocs.py"

# Sync specific file
python "005 Operations/Execution/sync_gdocs.py" --file "path/to/file.md"

# Force push local changes
python "005 Operations/Execution/sync_gdocs.py" --force push

# Force pull from Google Docs
python "005 Operations/Execution/sync_gdocs.py" --force pull

# JSON output for automation
python "005 Operations/Execution/sync_gdocs.py" --json
```

### Automated Sync via n8n

**Workflow:** `005 Operations/Workflows/gdocs-sync-workflow.json`

```
Schedule (15min) → SSH execute script → Parse JSON →
├── Has Activity? → Post to #agent-log
│                   └── Has Errors? → Post to #inbox-alerts
└── No Activity → Skip (silent)
```

Posts to Discord only when there's actual sync activity (pushes, pulls, creates, or errors).

### Environment Variables

```bash
# Reuses calendar service account (needs Docs API scope enabled)
GOOGLE_DOCS_CREDENTIALS=/path/to/service-account.json

# Default Drive folder for new synced documents
GOOGLE_DOCS_FOLDER_DEFAULT=<drive-folder-id>

# Directories to scan for sync-enabled files (comma-separated)
GOOGLE_DOCS_SYNC_DIRS=100 Resources,002 Projects,003 Entities
```

### Google Cloud Setup

1. **Enable APIs** in Google Cloud Console:
   - Google Docs API
   - Google Drive API (if not already)

2. **Service account setup:**
   - Can reuse existing calendar service account
   - Needs scopes: `documents`, `drive.file`

3. **Create Drive folder:**
   - Create folder in Google Drive
   - Share with service account email (Editor permission)
   - Copy folder ID from URL

### Execution Scripts

| Script | Purpose |
|--------|---------|
| `sync_gdocs.py` | Main sync orchestrator |
| `gdocs_converter.py` | Bidirectional format conversion |

### State and Backups

| Location | Purpose |
|----------|---------|
| `.tmp/sync_state/gdocs_sync.json` | Tracks sync state per file |
| `.tmp/backups/gdocs/YYYY-MM-DD/` | Backups before overwrites |
| `.tmp/logs/YYYY-MM-DD.log` | Sync operation logs |

### n8n Environment Variables Used

```
$env.DISCORD_WEBHOOK_AGENT_LOG     - Sync activity notifications
$env.DISCORD_WEBHOOK_INBOX_ALERTS  - Error alerts
```

**Note:** Self-hosted n8n uses `$env.VARIABLE_NAME` syntax (not `$vars`).

---

## Video Content Pipeline

Transform YouTube videos into content assets (articles, social snippets, quotes, intelligence) using Gemini transcription, Claude analysis, and voice profile application.

### Architecture

```
URL → Gemini 2.5 Transcribe → Claude Analyze → Voice Profile → Discord Review → Distribute
         (multimodal)         (structure)      (brand voice)    (approve/edit)
```

### Processing a Video

```bash
# Full pipeline with Discord review
.venv/bin/python "005 Operations/Execution/process_video_content.py" "https://youtube.com/watch?v=xxx"

# Skip Discord review (just generate drafts)
.venv/bin/python "005 Operations/Execution/process_video_content.py" "https://youtube.com/watch?v=xxx" --skip-discord

# Dry run (preview without saving)
.venv/bin/python "005 Operations/Execution/process_video_content.py" "https://youtube.com/watch?v=xxx" --dry-run

# Different voice profile
.venv/bin/python "005 Operations/Execution/process_video_content.py" "https://youtube.com/watch?v=xxx" --voice "Chaplain TIG"
```

### Output Structure

All generated content is saved to `000 Inbox/___Content/{uid}/`:

| File | Contents |
|------|----------|
| `_metadata.json` | Source info, status, timestamps |
| `article.md` | Full article draft with voice profile applied |
| `social.md` | Platform-specific social snippets (Twitter, LinkedIn, Instagram) |
| `quotes.md` | Key quotes extracted from video |
| `intel.md` | Internal intelligence summary (for knowledge base) |
| `transcript.md` | Raw Gemini transcription with visual context |

### Discord Review Commands

Reply in `#content-review` channel:

| Command | Action |
|---------|--------|
| `approve` | Approve most recent pending content |
| `approve <uid>` | Approve specific content by UID |
| `reject` | Reject and archive content |
| `edit: <instructions>` | Regenerate with specific changes |
| `rewrite intro` | Rewrite the introduction |
| `shorter` | Reduce length by ~30% |
| `more personal` | Increase vulnerability/personal tone |

### Automated Review Processing

The n8n workflow `content-review-workflow.json` polls every 5 minutes:
1. SSH to Azure VM
2. Run `process_content_review.py`
3. Process any approve/reject/edit commands
4. Log actions to #agent-log

### Content Lifecycle

```
000 Inbox/___Content/{uid}/     → Draft (pending_review)
000 Inbox/___Approved/{uid}/    → Approved (ready for distribution)
```

### Environment Variables

```bash
GOOGLE_AI_STUDIO_API_KEY="xxx"           # Gemini API key
DISCORD_CHANNEL_CONTENT_REVIEW="xxx"     # Channel ID for review
DISCORD_WEBHOOK_CONTENT_REVIEW="xxx"     # Webhook URL for notifications
```

### Gemini API Billing

The video content pipeline uses Google's Gemini API for video transcription. Understanding the billing tiers is important for production use.

**Free Tier Limits:**
- 20 requests/day for Gemini 2.5 Flash
- Sufficient for testing and occasional manual processing
- Will hit `429 RESOURCE_EXHAUSTED` errors when exceeded

**Enabling Billing (Production Use):**
1. Go to [Google AI Studio](https://aistudio.google.com/)
2. Create a new project (or use existing)
3. Settings → Billing → Link a billing account
4. Create new API key in the billing-enabled project
5. Update `GOOGLE_AI_STUDIO_API_KEY` in `.env`

**Pricing (Gemini 2.5 Flash):**
- Input: $0.30 per 1M tokens
- Output: $2.50 per 1M tokens
- Estimated cost per video: ~$0.003-0.015 (depending on length)
- Daily monitoring of ~20 videos: ~$0.10/day

**Cost Tracking:**
Monitor usage at [Google AI Studio → Activity](https://aistudio.google.com/activity).

### Related Files

- **Directive:** `005 Operations/Directives/process_video_content.md`
- **Scripts:** `005 Operations/Execution/process_video_content.py`, `process_content_review.py`
- **Workflow:** `005 Operations/Workflows/content-review-workflow.json`

---

## Voice Profiles

Voice profiles define how content should be written for specific personas or brands. They ensure consistent tone, style, and messaging across all generated content.

### Location

Voice profiles live in `003 Entities/Voice Profiles/`:

```
003 Entities/
└── Voice Profiles/
    ├── Chaplain TIG/
    │   └── Brand Voice.md
    └── GreenCal Construction/
        └── voice.md
```

### Profile Structure

Each voice profile folder contains:

| File | Purpose |
|------|---------|
| `voice.md` or `Brand Voice.md` | Core voice guide with attributes, tone, examples |
| Supporting docs | Linked resources like wisdom libraries |

### Available Profiles

| Profile | Path | Use Case |
|---------|------|----------|
| Chaplain TIG | `003 Entities/Voice Profiles/Chaplain TIG/` | Personal content, QWU, Missing Pixel |
| Ezer Aión | `003 Entities/Voice Profiles/Ezer Aión/` | QWU Backoffice assistant, automated outreach, verification |
| GreenCal Construction | `003 Entities/Voice Profiles/GreenCal Construction/` | Client: roofing/construction company |

### Listing Available Profiles

```bash
# List all discoverable voice profiles
.venv/bin/python "005 Operations/Execution/wisdom_synthesizer.py" --list-voices
```

Output:
```
=== Available Voice Profiles ===

  GreenCal Construction
    Type: folder
    Path: .../Voice Profiles/GreenCal Construction/voice.md

  Chaplain TIG
    Type: folder
    Path: .../Voice Profiles/Chaplain TIG/Brand Voice.md
```

### Using Voice Profiles

Voice profiles are used by both the video content pipeline and wisdom synthesizer:

```bash
# Video processing with default voice
.venv/bin/python "005 Operations/Execution/process_video_content.py" "https://..."

# Video processing with specific voice
.venv/bin/python "005 Operations/Execution/process_video_content.py" "https://..." --voice "Chaplain TIG"

# Wisdom synthesis with voice profile
.venv/bin/python "005 Operations/Execution/wisdom_synthesizer.py" \
  --vertical nonprofit --topic ai_adoption --voice "Chaplain TIG"
```

### Creating New Profiles

1. Create folder: `003 Entities/Voice Profiles/{Profile Name}/`
2. Create `Brand Voice.md` with:
   - Core voice attributes
   - Tone spectrum
   - Language preferences
   - Format examples
   - What to avoid
3. Link to supporting resources (wisdom libraries, etc.)

### Why Voice Profiles as Entities

Voice profiles are entities (not just templates) because:
- They have identity and evolve over time
- Can link to people: `linked_to: [[Person Name]]`
- Scale to multiple profiles per person or organization
- Keep operations clean (just reference the profile)

---

## Expert Intelligence System ⭐

Monitor thought leaders and subject matter experts across **four platforms** (YouTube, Twitter/X, LinkedIn, Newsletters), automatically capturing their new content, indexing it to the wisdom database, and sending Discord notifications.

### Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        EXPERT INTELLIGENCE PIPELINE                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ┌───────────────┐ ┌───────────────┐ ┌───────────────┐ ┌───────────────┐    │
│  │YouTube Monitor│ │Twitter Monitor│ │LinkedIn Monitor│ │Newsletter Mon.│    │
│  │  (6 hours)    │ │  (6 hours)    │ │   (6 hours)   │ │  (12 hours)   │    │
│  │youtube_monitor│ │twitter_monitor│ │linkedin_monitor│ │newsletter_mon │    │
│  └───────┬───────┘ └───────┬───────┘ └───────┬───────┘ └───────┬───────┘    │
│          │                 │                 │                 │             │
│          └─────────────────┴─────────────────┴─────────────────┘             │
│                                    │                                         │
│                                    ▼                                         │
│  ┌─────────────────────────────────────────────────────────────────┐        │
│  │                    Raw Captures (Obsidian-readable)              │        │
│  │  000 Inbox/___Intelligence/{youtube,twitter,linkedin,newsletters}│        │
│  └──────────────────────────────┬──────────────────────────────────┘        │
│                                 │                                            │
│                                 ▼                                            │
│  ┌─────────────────────────────────────────────────────────────────┐        │
│  │                   Wisdom Indexer (Claude API)                    │        │
│  │              Classifies by vertical, topic, concern              │        │
│  └──────────────────────────────┬──────────────────────────────────┘        │
│                                 │                                            │
│                                 ▼                                            │
│  ┌─────────────────────────────────────────────────────────────────┐        │
│  │                     .tmp/wisdom.db (SQLite)                      │        │
│  │               Queryable database of classified insights          │        │
│  └─────────────────────────────────────────────────────────────────┘        │
│                                 │                                            │
│                                 ▼                                            │
│  ┌─────────────────────────────────────────────────────────────────┐        │
│  │                  Discord #intel-digest Notifications             │        │
│  └─────────────────────────────────────────────────────────────────┘        │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

> **Missing Pixel Training Opportunity**
>
> The Expert Intelligence Pipeline is an excellent **Tier 2 curriculum module** covering:
> - **Multi-source data integration** - YouTube, Twitter, LinkedIn, Newsletters into unified workflow
> - **n8n automation** - Scheduled triggers, SSH execution, conditional logic, Discord notifications
> - **API integrations** - YouTube Data API, Apify (Twitter/LinkedIn scraping), MS Graph (Outlook)
> - **Database design** - SQLite for wisdom indexing, classification taxonomies
> - **Cost management** - Understanding API billing (Gemini free tier vs paid)
> - **Troubleshooting** - SSH authentication, rate limiting, API quotas
>
> Students can shadow a working production system, then build their own expert monitoring pipeline for a topic of interest.

### Expert Profiles

Expert profiles live in `003 Entities/Experts/` with YAML frontmatter supporting multiple platforms:

```yaml
---
name: Qiusheng Wu
status: active
priority: A
fields: [gis, geospatial, python, remote-sensing]
platforms:
  youtube:
    url: https://youtube.com/@giswqs
    channel_id: <YOUTUBE_CHANNEL_ID>
    frequency: weekly
    last_checked: '2026-01-14T12:00:00'
  twitter:
    handle: giswqs
    last_checked: '2026-01-14T12:00:00'
---
```

### Managing Experts

```bash
# Add a new expert with YouTube
.venv/bin/python "005 Operations/Execution/expert_registry.py" add "Simon Sinek" \
  --priority A --youtube "https://youtube.com/@simonsinek" --fields leadership,culture

# List all active experts
.venv/bin/python "005 Operations/Execution/expert_registry.py" list

# Get specific expert
.venv/bin/python "005 Operations/Execution/expert_registry.py" get "Simon Sinek"
```

### Source 1: YouTube Monitoring

Monitor expert YouTube channels for new videos, then process through the content pipeline.

```bash
# Check all channels for new videos
.venv/bin/python "005 Operations/Execution/youtube_monitor.py" --check

# Check A-tier experts only
.venv/bin/python "005 Operations/Execution/youtube_monitor.py" --check --priority A

# Check and process new videos through content pipeline (transcribe + index)
.venv/bin/python "005 Operations/Execution/youtube_monitor.py" --check --process
```

**n8n Workflow:** `expert-intelligence-workflow.json` (every 6 hours)

### Source 2: Twitter/X Monitoring

Monitor expert Twitter accounts for recent tweets using Apify.

```bash
# Check all experts with Twitter handles for recent tweets
.venv/bin/python "005 Operations/Execution/twitter_monitor.py" --check

# Check and process (capture + index to wisdom database)
.venv/bin/python "005 Operations/Execution/twitter_monitor.py" --check --process

# Check specific expert only
.venv/bin/python "005 Operations/Execution/twitter_monitor.py" --expert "Qiusheng Wu"

# Test specific handles directly
.venv/bin/python "005 Operations/Execution/twitter_monitor.py" --test-handles giswqs,deepseadawn
```

**n8n Workflow:** `twitter-intelligence-workflow.json` (every 6 hours)

**Cost:** ~$0.40 per 1,000 tweets via Apify (`apidojo/tweet-scraper`)

### Source 3: Newsletter Monitoring

Monitor Outlook inbox for newsletters from whitelisted sources only.

```bash
# List whitelisted newsletter sources
.venv/bin/python "005 Operations/Execution/newsletter_monitor.py" --list

# Check for new newsletters (dry run first)
.venv/bin/python "005 Operations/Execution/newsletter_monitor.py" --check --dry-run

# Check and process new newsletters (capture + index)
.venv/bin/python "005 Operations/Execution/newsletter_monitor.py" --check --process
```

**n8n Workflow:** `newsletter-intelligence-workflow.json` (every 12 hours)

**Whitelist:** `003 Entities/Taxonomies/newsletter_intel_sources.yaml`

```yaml
sources:
  nir_eyal:
    name: Nir Eyal
    email: nir@nirandfar.com
    match_type: email
    priority: A
    topics: [productivity, behavior-design, habits]
  vp_land:
    name: VP Land
    domain: vpland.io
    match_type: domain
    priority: B
    topics: [drone-mapping, surveying, geospatial]
```

### Source 4: LinkedIn Monitoring

Monitor LinkedIn profiles of watched experts for new posts. LinkedIn has become the professional "town square" as many thought leaders shift from Twitter/X.

```bash
# List LinkedIn-enabled experts
.venv/bin/python "005 Operations/Execution/linkedin_monitor.py" --list

# Test with a specific profile
.venv/bin/python "005 Operations/Execution/linkedin_monitor.py" --test-profile satyanadella

# Check for new posts (dry run first)
.venv/bin/python "005 Operations/Execution/linkedin_monitor.py" --check --dry-run

# Check and process new posts (capture + index)
.venv/bin/python "005 Operations/Execution/linkedin_monitor.py" --check --process
```

**n8n Workflow:** `linkedin-intelligence-workflow.json` (every 6 hours)

**Cost:** ~$5 per 1,000 posts via Apify (`apimaestro/linkedin-profile-posts`)

### Priority Tiers

| Priority | YouTube | Twitter | LinkedIn | Newsletters | Use Case |
|----------|---------|---------|----------|-------------|----------|
| A | Every 6 hours | Every 6 hours | Every 6 hours | Every 12 hours | Core thought leaders |
| B | Every 12 hours | Every 6 hours | Every 6 hours | Every 12 hours | Important experts |
| C | Every 24 hours | Every 6 hours | Every 6 hours | Every 12 hours | Secondary sources |

### Reviewing Captured Intelligence

**Option 1: Browse Raw Captures in Obsidian**
```
000 Inbox/___Intelligence/
├── youtube/           # Full video transcripts with metadata
├── twitter/           # Tweet captures organized by expert
├── linkedin/          # LinkedIn posts organized by expert
└── newsletters/       # Newsletter content with frontmatter
```

**Option 2: Query the Wisdom Database**
```bash
# See what's available
.venv/bin/python "005 Operations/Execution/wisdom_query.py" --list-filters

# Get wisdom from a specific expert
.venv/bin/python "005 Operations/Execution/wisdom_query.py" --expert "Qiusheng Wu"

# Filter by topic
.venv/bin/python "005 Operations/Execution/wisdom_query.py" --topic gis --limit 10

# Last 7 days only
.venv/bin/python "005 Operations/Execution/wisdom_query.py" --days 7
```

### Environment Variables

```bash
GOOGLE_API_KEY="xxx"          # YouTube Data API v3
APIFY_API_TOKEN="xxx"         # Twitter + LinkedIn scraping via Apify
MSGRAPH_CLIENT_ID="xxx"       # Outlook/newsletter access
MSGRAPH_CLIENT_SECRET="xxx"
MSGRAPH_TENANT_ID="xxx"
DISCORD_WEBHOOK_INTEL_DIGEST="xxx"  # #intel-digest notifications
```

### Related Files

**Directives:**
- `005 Operations/Directives/expert_intelligence.md`
- `005 Operations/Directives/twitter_intelligence.md`
- `005 Operations/Directives/linkedin_intelligence.md`
- `005 Operations/Directives/newsletter_intelligence.md`

**Scripts:**
- `expert_registry.py` - Expert profile management
- `youtube_monitor.py` - YouTube channel monitoring
- `twitter_monitor.py` - Twitter/X monitoring via Apify
- `linkedin_monitor.py` - LinkedIn monitoring via Apify
- `newsletter_monitor.py` - Outlook newsletter monitoring
- `digest_generator.py` - Intelligence digest generation

**Workflows:**
- `expert-intelligence-workflow.json` (YouTube)
- `twitter-intelligence-workflow.json` (Twitter)
- `linkedin-intelligence-workflow.json` (LinkedIn)
- `newsletter-intelligence-workflow.json` (Newsletters)

---

## Wisdom Synthesis System ⭐

Aggregate insights from multiple thought leaders across **YouTube, Twitter, LinkedIn, and Newsletters**, classify by audience vertical and topic, then synthesize audience-specific content with proper attribution and brand voice.

### Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                          WISDOM SYNTHESIS FLOW                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ┌────────────────┐ ┌────────────────┐ ┌────────────────┐ ┌────────────────┐│
│  │ YouTube Videos │ │ Twitter Tweets │ │ LinkedIn Posts │ │ Newsletters    ││
│  │ (transcripts)  │ │ (tweet text)   │ │ (post text)    │ │ (email content)││
│  └───────┬────────┘ └───────┬────────┘ └───────┬────────┘ └───────┬────────┘│
│          │                  │                  │                  │          │
│          └──────────────────┴──────────────────┴──────────────────┘          │
│                                 ▼                                            │
│                    ┌───────────────────────┐                                 │
│                    │    Wisdom Indexer     │                                 │
│                    │   (Claude API + SQL)  │                                 │
│                    └───────────┬───────────┘                                 │
│                                │                                             │
│           ┌────────────────────┼────────────────────┐                        │
│           ▼                    ▼                    ▼                        │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐              │
│  │   verticals     │  │     topics      │  │    concerns     │              │
│  │  (audiences)    │  │   (subjects)    │  │  (pain points)  │              │
│  │  nonprofit      │  │  ai_adoption    │  │  accuracy       │              │
│  │  surveying      │  │  trust          │  │  cost           │              │
│  │  healthcare     │  │  quality        │  │  compliance     │              │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘              │
│                                │                                             │
│                                ▼                                             │
│                   ┌────────────────────────┐                                 │
│                   │   Wisdom Synthesizer   │                                 │
│                   │   + Voice Profile      │                                 │
│                   │   + Format Templates   │                                 │
│                   └────────────────────────┘                                 │
│                                │                                             │
│                                ▼                                             │
│        ┌───────────────────────────────────────────────┐                     │
│        │  linkedin_post │ twitter_thread │ newsletter  │                     │
│        │  talking_points │ email_outreach │ article    │                     │
│        └───────────────────────────────────────────────┘                     │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Data Flow

1. **Capture:** Content from YouTube (transcripts), Twitter (tweets), Newsletters (email body)
2. **Index:** `wisdom_indexer.py` extracts insights, classifies by vertical/topic/concern
3. **Query:** `wisdom_query.py` retrieves wisdom by audience + topic + expert
4. **Synthesize:** `wisdom_synthesizer.py` generates attributed content with voice profile

### Indexing Wisdom

```bash
# Index wisdom from processed video content
.venv/bin/python "005 Operations/Execution/wisdom_indexer.py" \
  "000 Inbox/___Content/20260111-020429" --expert "Pragmatic Architect"

# View database statistics
.venv/bin/python "005 Operations/Execution/wisdom_indexer.py" --stats
```

### Querying Wisdom

```bash
# Find AI adoption wisdom for nonprofits
.venv/bin/python "005 Operations/Execution/wisdom_query.py" \
  --vertical nonprofit --topic ai_adoption

# Get leadership quotes from specific expert
.venv/bin/python "005 Operations/Execution/wisdom_query.py" \
  --expert "Simon Sinek" --topic leadership

# List available filters
.venv/bin/python "005 Operations/Execution/wisdom_query.py" --list-filters
```

### Synthesizing Content

```bash
# Generate LinkedIn post for nonprofits about AI adoption
.venv/bin/python "005 Operations/Execution/wisdom_synthesizer.py" \
  --vertical nonprofit --topic ai_adoption --format linkedin_post

# Generate talking points for surveyors with GreenCal voice
.venv/bin/python "005 Operations/Execution/wisdom_synthesizer.py" \
  --vertical surveying --topic quality --format talking_points \
  --voice "GreenCal Construction" --save

# List available content formats
.venv/bin/python "005 Operations/Execution/wisdom_synthesizer.py" --list-formats
```

### Content Formats

| Format | Description | Max Length |
|--------|-------------|------------|
| `linkedin_post` | Professional post with line breaks | 1300 chars |
| `twitter_thread` | Numbered tweets | 280 chars/tweet |
| `newsletter_section` | Long-form with storytelling | 4000 chars |
| `talking_points` | Presentation bullet points | 2000 chars |
| `email_outreach` | Cold/warm email | 1500 chars |
| `article_intro` | Opening paragraphs with expert voices | 2500 chars |

### Taxonomies

Located in `003 Entities/Taxonomies/`:

| File | Contents |
|------|----------|
| `verticals.yaml` | 12 industry/audience categories (nonprofit, surveying, healthcare...) |
| `topics.yaml` | 20 subject matter categories (ai_adoption, trust, quality...) |
| `concerns.yaml` | 15 pain points (accuracy, cost, job_displacement...) |

### Output Location

Synthesized content saved to `000 Inbox/___Synthesis/`:

```
000 Inbox/___Synthesis/
└── 20260111-025328-nonprofit.md
```

Each file includes:
- YAML frontmatter (format, vertical, topic, voice, timestamp)
- Generated content
- Source attribution with links

### Wiki Links

Generated content includes Obsidian `[[wiki links]]` for knowledge graph building:
- Key concepts: `[[Explainable AI]]`, `[[Software Architecture]]`
- Named people: `[[Simon Sinek]]`, `[[Geoffrey Hinton]]`
- Organizations: `[[OpenAI]]`, `[[Google DeepMind]]`

Social snippets remain link-free for platform export.

### Related Files

- **Directive:** `005 Operations/Directives/wisdom_synthesis.md`
- **Scripts:** `wisdom_indexer.py`, `wisdom_query.py`, `wisdom_synthesizer.py`
- **Database:** `.tmp/wisdom.db` (SQLite)
- **Taxonomies:** `003 Entities/Taxonomies/`

---

## Canonical Datetime System

The QWU Backoffice runs on an Azure VM in UTC timezone, but all user-facing operations use Pacific Time. The **qwu_datetime** module provides a single source of truth for date/time operations across all scripts.

### Why This Matters

| Server Time (UTC) | User Time (PST) | Without qwu_datetime |
|-------------------|-----------------|---------------------|
| Friday 6:00 AM | Thursday 10:00 PM | Shows "Friday" (WRONG) |
| Friday 6:00 AM | Thursday 10:00 PM | Shows "Thursday" (CORRECT) |

Without canonical timezone handling, morning briefings, calendar queries, and daily notes would display the wrong date for ~8 hours every day.

### The Module: qwu_datetime.py

**Location:** `005 Operations/Execution/qwu_datetime.py`

All QWU scripts **MUST** import from this module instead of using `datetime.now()` directly:

```python
# CORRECT - Use canonical QWU datetime
from qwu_datetime import now, today, effective_date, format_date

current_time = now()          # Timezone-aware datetime in PST
current_date = today()        # Date in PST
log_date = effective_date()   # Date for logging (handles 4am boundary)

# WRONG - Never use these directly
from datetime import datetime
bad_time = datetime.now()     # Returns UTC on server!
```

### Available Functions

| Function | Returns | Use Case |
|----------|---------|----------|
| `now()` | Timezone-aware datetime | Current time operations |
| `today()` | date | Current date comparisons |
| `effective_date()` | date | Logging (handles 4am boundary) |
| `effective_datetime()` | datetime | Timestamps for logs |
| `format_date(d, style)` | str | Consistent date formatting |
| `format_time(dt, style)` | str | Consistent time formatting |
| `format_datetime(dt, style)` | str | Combined formatting |
| `to_utc(dt)` | datetime | Convert to UTC for APIs |
| `from_utc(dt)` | datetime | Convert from UTC responses |
| `get_timezone_info()` | dict | Debug/status information |

### Format Styles

**Date styles** (`format_date`):
- `"iso"` → `2026-01-08`
- `"display"` → `January 8, 2026`
- `"file"` → `20260108`
- `"weekday"` → `Thursday, January 8, 2026`
- `"short"` → `Jan 8`

**Time styles** (`format_time`):
- `"12h"` → `10:46 PM`
- `"24h"` → `22:46`
- `"full"` → `10:46:30 PM`
- `"log"` → `22:46:30`

### Day Boundary Feature

Work before 4 AM counts as "yesterday" for logging purposes:

```
2:00 AM on Jan 9 → effective_date() returns Jan 8
5:00 AM on Jan 9 → effective_date() returns Jan 9
```

This prevents late-night sessions from bleeding into the next day's records.

### Environment Variables

```bash
# Canonical timezone for all QWU operations (IANA format)
QWU_TIMEZONE=America/Los_Angeles

# Day boundary hour (work before this counts as "yesterday")
QWU_DAY_BOUNDARY_HOUR=4
```

### Testing the Module

```bash
cd ~/qwu_backOffice && source .env
python "005 Operations/Execution/qwu_datetime.py"            # Human-readable status
python "005 Operations/Execution/qwu_datetime.py" --json     # JSON output
```

**Sample output:**
```
============================================================
QWU DATETIME STATUS
============================================================
Timezone:        America/Los_Angeles
Current offset:  -0800 (PST)
DST active:      False
Day boundary:    4:00 AM
------------------------------------------------------------
Now:             January 8, 2026 at 10:51 PM
Today:           Thursday, January 8, 2026
Effective date:  Thursday, January 8, 2026
============================================================
```

### Scripts Updated

All execution scripts have been updated to use qwu_datetime:

| Script | Version | Status |
|--------|---------|--------|
| `qwu_datetime.py` | v1.0.0 | Core module |
| `morning_briefing.py` | v1.6.0 | ✅ Goals integration |
| `calendar_events.py` | v1.2.0 | ✅ Updated |
| `summarize_session.py` | v1.4.0 | ✅ Goals alignment |
| `process_inbox.py` | v2.6.0 | ✅ Duplicate detection |
| `api_logger.py` | v1.1.0 | ✅ Updated |
| `api_rate_limiter.py` | v1.1.0 | ✅ Updated |
| `vista_social_api.py` | v1.1.0 | ✅ Updated |
| `azure_costs.py` | v1.1.0 | ✅ Updated |
| `ez_chat_handler.py` | v2.2.0 | ✅ Updated |
| `calendar_booking.py` | v1.1.0 | ✅ Updated |
| `extract_unresolved_links.py` | v1.3 | ✅ Updated |

**Important:** Any new scripts MUST import from `qwu_datetime` instead of using `datetime.now()` directly. This ensures consistent timezone handling across the entire codebase.

### Lovable Frontend Standard (Foundational Directive)

**Promoted to Foundational Directive:** February 13, 2026

The same timezone problem affects all QWF Lovable apps. JavaScript's `new Date().toISOString()` returns UTC. After 4 PM Pacific (midnight UTC), the UTC date flips to the next calendar day. Since Supabase stores dates in Pacific time, all Supabase date-boundary queries silently return wrong results for 8 hours every day. No errors are thrown — dashboards just show empty/stale data.

**Every QWF Lovable project must include `src/utils/timezone.ts`** with 7 helper functions. This file is required in every Prompt 001 (foundation prompt) — see CLAUDE.md Lovable Prompt Conventions.

**Canonical utility functions:**

| Function | Returns | Use Case |
|----------|---------|----------|
| `getPacificToday()` | `"2026-02-13"` | Supabase `.eq('date', today)` queries |
| `getPacificDaysAgo(n)` | `"2026-02-06"` | Date range filters ("last 7 days") |
| `getPacificMonthStart()` | `"2026-02-01"` | Monthly financial summaries |
| `getPacificMonthsAgo(n)` | `"2025-09-01"` | Sparkline/trend chart ranges |
| `getPacificYearMonth()` | `"2026-02"` | `usage_monthly.month` matching |
| `isPacificToday(ts)` | `true/false` | Display logic ("2:34 PM" vs "Feb 11") |
| `toPacificDate(ts)` | `"2026-02-13"` | Chart grouping by Pacific day |

**Wrong patterns (search and replace in every Lovable codebase):**
```typescript
new Date().toISOString().split('T')[0]     // UTC — wrong after 4 PM Pacific
new Date().toISOString().slice(0, 10)       // Same problem
new Date().toLocaleDateString()             // Locale-dependent, unreliable
```

**Correct pattern:**
```typescript
import { getPacificToday, getPacificDaysAgo } from '@/utils/timezone';
const today = getPacificToday();              // Always Pacific YYYY-MM-DD
const weekAgo = getPacificDaysAgo(7);         // 7 days ago in Pacific
```

**Why `en-CA`?** The Canadian English locale formats dates as `YYYY-MM-DD` (ISO 8601), matching Supabase's date column format. **Why `America/Los_Angeles`?** IANA timezone name that handles PST/PDT transitions automatically — never hardcode `-08:00`.

**History:** First identified in HQ Command Center (Feb 2026, calendar edge function showed tomorrow's events after 4 PM). Recurred in QQT (11 affected locations) and QMP (18 affected locations) before the convention was established. Root cause: the original timezone directive called frontend JS "Generally safe" — this assessment was wrong for Supabase date queries and was corrected Feb 13, 2026.

**3-layer defense:**
1. **Prevention:** Every Prompt 001 must include `timezone.ts` (CLAUDE.md Lovable Prompt Conventions)
2. **Enforcement:** Agent instructions require Pacific helpers in all Lovable prompt code examples (never raw `new Date()`)
3. **Remediation:** `005 Operations/Prompts/timezone-fix-handover.md` for auditing/fixing legacy apps built before the convention

**Apps fixed:** QQT (Prompt 009), QMP (Prompt 008), Pocket Ez (Prompt 007). New apps built after Feb 2026 should not need remediation.

**Full directive:** `005 Operations/Directives/timezone_standard.md`

### Training Opportunities

| Component | Skills Developed | Difficulty |
|-----------|------------------|------------|
| Timezone Bug Analysis | UTC vs local time, silent failures, date boundary math | Beginner |
| `Intl.DateTimeFormat` API | Browser APIs, locale formatting, IANA timezones | Intermediate |
| Systematic Codebase Audit | Pattern matching, regex search, impact analysis | Intermediate |
| Prevention Architecture | Convention design, agent instruction, defense-in-depth | Advanced |

---

## Azure Cost Tracking

Monitor Azure spending directly from the backoffice for cost awareness. Azure is one of 7 variable cost sources tracked by the [[#Cost Intelligence System]] — see that section for the unified cost tracking architecture including LLM, Apify, Supabase, and budget alerting.

### What's Tracked

| Metric | Description |
|--------|-------------|
| Yesterday's cost | Previous day's total spend |
| Month-to-date | Cumulative spending this month (always queries full month from 1st) |
| 3-day average | Rolling average for trend analysis |
| Daily breakdown | Per-day costs over configurable window (default 7 days) |

### Setup Requirements

Uses the same Azure Service Principal as VM control, but requires **Cost Management Reader** role:

```bash
az role assignment create \
  --assignee $AZURE_CLIENT_ID \
  --role "Cost Management Reader" \
  --scope "/subscriptions/$AZURE_SUBSCRIPTION_ID"
```

### Environment Variables

```bash
AZURE_SUBSCRIPTION_ID="your-subscription-id"
AZURE_TENANT_ID="your-tenant-id"
AZURE_CLIENT_ID="your-client-id"
AZURE_CLIENT_SECRET="your-client-secret"
```

### Usage

```bash
cd ~/qwu_backOffice && source .env
python "005 Operations/Execution/azure_costs.py"            # Human-readable output
python "005 Operations/Execution/azure_costs.py" --json     # JSON for automation
python "005 Operations/Execution/azure_costs.py" --dry-run  # Validate credentials
```

### Sample Output

```
AZURE COST SUMMARY
========================================
Yesterday: $0.42
Month-to-date: $12.87
3-day avg: $0.38/day
----------------------------------------
Daily breakdown:
  2026-01-05: $0.35
  2026-01-06: $0.41
  2026-01-07: $0.42
```

---

## Lead Generation System

The backoffice includes a comprehensive lead generation and enrichment system supporting L4G (Locals 4 Good) business development.

**Full L4G Technical Documentation:** `003 Entities/Organizations/Locals 4 Good.md`

The L4G system includes:
- **Website:** locals4good.org (Lovable app, published Feb 27, 2026)
- **Data Layer:** Supabase (`<SUPABASE_PROJECT_ID_L4G>`) — 14 tables, migrated from Google Sheets
- **APIs:** 3 Supabase Edge Functions (submit-contact-form, create-checkout-session, check-availability)
- **Payments:** Stripe Checkout via `create-checkout-session` edge function + n8n `L4G Stripe Payment Handler` webhook
- **Automation:** n8n workflows for payment processing, contact pipeline
- **Migration:** Data migrated from Google Sheets → Supabase via `migrate_l4g_sheets_to_supabase.py` (Feb 27, 2026)

**Lead Generation Webhook:** `https://n8n.quietlyworking.org/webhook/lead-request`

### Available Skills

Lead generation skills live in `.claude/skills/`:

| Skill | Purpose |
|-------|---------|
| `linkedin-scraping` | Scrape leads from LinkedIn Sales Navigator |
| `gmaps-scraping` | Scrape local businesses from Google Maps |
| `apollo-scraping` | Scrape verified leads from Apollo.io |
| `lead-generation` | Multi-source lead generation routing |
| `lead-enrichment` | Enrich existing lead lists |
| `email-enrichment` | Find/verify emails via Anymail Finder |
| `friendly-name-enrichment` | Clean company names to brand names |
| `review-enrichment` | Add Google reviews to leads |

### Execution Scripts

Scripts in `005 Operations/Execution/`:

**Scraping Scripts:**

| Script | Purpose |
|--------|---------|
| `scrape_leads_linkedin.py` | LinkedIn Sales Navigator scraping |
| `scrape_leads_gmaps.py` | Google Maps local business scraping |
| `scrape_leads_apollo.py` | Apollo.io lead scraping |
| `scrape_leads_yelp.py` | Yelp business scraping |
| `scrape_leads_crunchbase.py` | Crunchbase company scraping |
| `scrape_leads_yellowpages.py` | Yellow Pages scraping |
| `process_lead_request.py` | Master orchestrator for all sources |

**Enrichment Scripts:**

| Script | Purpose |
|--------|---------|
| `enrich_email.py` | Email discovery via Anymail Finder |
| `enrich_email_reoon.py` | Cheaper bulk email validation via Reoon |
| `enrich_reviews_google.py` | Google review enrichment |
| `enrich_friendly_company_name.py` | AI-powered name cleaning |
| `find_decision_makers.py` | Find 1-3 decision makers per company |
| `extract_personalization.py` | Deep website scraping for outreach hooks |
| `group_competitors.py` | Cluster businesses for competitor FOMO |

**Delivery Scripts:**

| Script | Purpose |
|--------|---------|
| `upload_to_sheets.py` | Push results to Google Sheets |
| `analyze_leads.py` | Data quality audit |

### L4G Cold Email Pipeline

The L4G pipeline is specialized for fundraising cold email campaigns with a two-phase enrichment strategy.

**Phase 1: Initial Cold Email (Minimal Cost)**
Use for first outreach to new prospects:
1. Scrape from Google Maps (local businesses)
2. Clean company names with AI
3. Find 1-3 decision makers per company
4. Validate emails with Reoon (cheaper)
5. Group into competitor clusters (5-7 per group)

**Phase 2: Full Enrichment (Post-Conversion)**
Use only after prospect becomes a paying customer:
1. Deep personalization from website scraping
2. Google reviews + AI summaries
3. LinkedIn depth enrichment

**Key Features:**
- **Decision Makers:** 1-3 contacts per company with first names for personalization
- **Email Validation:** Reoon validates emails at lower cost than Anymail
- **Competitor FOMO:** "We're also reaching out to [Business A], [Business B]..."
- **Deep Personalization:** AI-extracted hooks from website scraping

**Directive:** `005 Operations/Directives/generate_l4g_leads.md`

**Cost Estimates (Per 100 Leads):**

| Component | Cost |
|-----------|------|
| GMaps scraping | ~$0.10 |
| Friendly names (Claude) | ~$0.20 |
| Decision makers | ~$0.60 |
| Reoon validation | ~$0.50 |
| Personalization | ~$2.00 |
| **Total (without personalization)** | **~$1.40** |
| **Total (with personalization)** | **~$3.40** |

### Output Destination

Lead data is delivered to Google Sheets (QWU Backoffice shared drive) for team access and further processing. The `upload_to_sheets.py` script handles the transfer.

### Rate Limiting

All scraping scripts include rate limiting via `api_rate_limiter.py` to avoid bans and respect source terms of service.

---

## Communications Architecture

The QWU ecosystem uses a hybrid communications approach.

### Three Layers

| Layer | Tool | Purpose |
|-------|------|---------|
| Personal Capture | Telegram | Quick capture, private notes |
| Team Hub | Discord | Staff, students, community |
| Power Tools | Azure VM + Claude Code | Development work |

### Why Discord?

| Factor | Assessment |
|--------|------------|
| Cost | Free (sufficient for our needs) |
| Culture fit | Gamer/VFX/creative... matches our people |
| Bot support | Excellent, no paywalls |
| Student readiness | Used in creative industry |
| Community building | Built for this |

### Discord Server Structure

```
🏠 QWU - UNIVERSE HUB
├── 📢 welcome-and-rules
├── 📢 announcements
├── 💬 general
├── 💬 off-topic
├── 🎉 wins
└── 💰 fundraising-general

🔒 STAFF
├── 🔒 leadership
├── 🔒 staff-only
├── 🔒 operations
└── 🔒 moderator-only

🤖 AGENTS (automation hub)
├── 🤖 agent-log           # Processing summaries
├── 🤖 inbox-alerts        # Notes needing review
├── 🔥 l4g-leads           # Lead notifications
├── 🔔 system-status       # VM/system alerts
└── 📊 daily-digest        # Morning summary

🎓 MISSING PIXEL
├── 📢 mp-announcements
├── 💬 mp-general
├── 📝 mp-assignments
├── ❓ mp-help (forum)
├── 🎨 mp-show-your-work
└── 📚 mp-resources

[Additional categories for ACOFH, IYSR, WOH, QWC, L4G, Community]
```

### Discord Role Hierarchy

| Role | Color | Purpose |
|------|-------|---------|
| @Admin | Red (#E74C3C) | Full server control |
| @Staff | Blue (#3498DB) | Core team members |
| @MP-Maintainer | Purple (#9B59B6) | Tier 4 students |
| @MP-Builder | Green (#2ECC71) | Tier 3 students |
| @MP-Contributor | Teal (#1ABC9C) | Tier 2 students |
| @MP-Student | Gray (#95A5A6) | Tier 1 students |
| @Volunteer | Orange (#E67E22) | Program volunteers |
| @Supporter | Gold (#F1C40F) | Donors, fans |
| @Community | Default | General public |

### Webhook Configuration

Store webhook URLs in `.env`:

```bash
DISCORD_WEBHOOK_AGENT_LOG="https://discord.com/api/webhooks/xxx/yyy"
DISCORD_WEBHOOK_INBOX_ALERTS="https://discord.com/api/webhooks/xxx/yyy"
DISCORD_WEBHOOK_L4G_LEADS="https://discord.com/api/webhooks/xxx/yyy"
DISCORD_WEBHOOK_SYSTEM_STATUS="https://discord.com/api/webhooks/xxx/yyy"
DISCORD_WEBHOOK_DAILY_DIGEST="https://discord.com/api/webhooks/xxx/yyy"
```

### Testing a Webhook

```bash
curl -X POST "$DISCORD_WEBHOOK_AGENT_LOG" \
  -H "Content-Type: application/json" \
  -d '{"content": "🧪 Webhook test successful!"}'
```

---

## Data Architecture

### SuiteDash vs Obsidian Boundaries

| SuiteDash (CRM) | Obsidian (PKM) |
|-----------------|----------------|
| Contact records | Relationship notes |
| Transactions | Knowledge insights |
| Operational data | Agent skills |
| Tasks & projects | Research & learning |
| Communication logs | Decision rationale |

**Principle:** Agents facilitate intelligent handoffs between systems. SuiteDash handles transactional/operational data while Obsidian manages knowledge and insights.

### Entity Resolution Security (Critical)

**The Problem:** Substring matching for entity lookups caused critical bugs where display names matched wrong entities.

**Example Bug (2026-01-23):** A BNI meeting recap email was incorrectly sent to "<EXTERNAL_EMAIL>" (an organization) because:
- Zoom display name: "Chapter President"
- Matched entity: "[Member Name], Associate Vice President..."
- Root cause: "president" substring exists in both strings

**The Solution:** Centralized `entity_resolver.py` with safety features:

```python
from entity_resolver import resolve_for_enrichment

# Safe - uses centralized resolver with role blocklist
entity_path = resolve_for_enrichment("John Smith", caller="my_script.py")

# NEVER use substring matching directly:
# DANGEROUS: if name.lower() in f.stem.lower():
```

**Key Features:**
| Feature | Purpose |
|---------|---------|
| **Role Blocklist** | Blocks 30+ terms like "Chapter President", "Vice President", "Secretary" |
| **Strictness Levels** | STRICT (email routing), STANDARD (enrichment), PERMISSIVE (history) |
| **Purpose Declaration** | EMAIL_ROUTING, DATA_ENRICHMENT, HISTORY_LINKING |
| **Confidence Scoring** | Requires exact or near-exact matches, rejects fuzzy matches |

**Scripts Migrated (18 total):**
- All `enrich_member_*.py` scripts (6)
- All `*_121_*.py` and briefing scripts (5)
- All `*_suitedash_*.py` and sync scripts (5)
- `predictive_intelligence.py`, `generate_connection_report.py`, `update_person_health.py`

**Rule:** Any new script that looks up entity files MUST use `entity_resolver.py`. Never implement direct substring matching.

### What to Store in Entity Notes (003 Entities/)

| Store in Obsidian | Let Agents Search Online |
|-------------------|--------------------------|
| Your account tier/plan | General "how to" docs |
| Your specific configurations | API reference details |
| API key location (not the key) | Troubleshooting generic issues |
| Workflows YOU actually use | Feature changelogs |
| Gotchas you've discovered | Best practices guides |
| Integration notes | |

### Mobile-to-Obsidian Workflow

**Dual Input System:**
- **Drop files** → `000 Inbox/___Capture/` (Claude artifacts, Perplexity exports, research)
- **Quick dumps** → `000 Inbox/Notes from my phone.md` (rapid mobile text captures)

```
1. You drop files → 000 Inbox/___Capture/
   OR append quick notes → Notes from my phone.md
2. Agent splits quick notes into individual files → ___Capture/
3. Agent moves each file to → 000 Inbox/___Processing/
4. Agent enriches (YAML, tags, internal links)
5. High confidence → auto-filed to destination
   Low confidence → 000 Inbox/___Review/
6. You review items in ___Review/ (or auto-file based on threshold)
7. Final destination in appropriate folder
```

---

## Project Organization

### Naming Conventions

Projects in `002 Projects/` follow a visual naming convention that indicates lifecycle status at a glance.

| Type | Convention | Example |
|------|------------|---------|
| **Evergreen** | `_ProjectName/` | `_QWU Backoffice Automation/` |
| **Client Container** | `_ClientName/` | `_Aim High BNI Projects/` |
| **Active Time-bound** | `ProjectName/` | `Conference 2026/` |
| **Completed** | `zzz-YYYYMMDD-Name/` | `zzz-20251215-Old Campaign/` |

**Key principles:**
- Underscore prefix (`_`) = ongoing, no foreseeable end date
- `zzz-YYYYMMDD-` prefix = completed (sorts to bottom, chronological within)

### What Makes Something Evergreen?

| Evergreen | Not Evergreen |
|-----------|---------------|
| Client relationship containers | One-time deliverable |
| Ongoing internal systems (backoffice) | Conference with a date |
| Newsletter (continuous publication) | Specific campaign |

**Test:** If you can't imagine a "done" state, it's evergreen.

### Project Folder Structure

Every project folder contains:

```
_ProjectName/
├── _Overview.md              # Index/summary (required)
├── Task1.md                  # Individual tasks as files
├── Task2.md
├── SubProject/               # Sub-projects as folders
│   └── _Overview.md
└── zzz-20251215-Done Thing/  # Completed sub-work (bottom, chronological)
```

### Special Files

| File | Purpose |
|------|---------|
| `_Overview.md` | Project index, status, active tasks |
| `_Project List.md` | Global project index at `002 Projects/` root |

### Example: Client Container

```
_Aim High BNI Projects/               # Evergreen (client relationship)
├── _Overview.md                      # Client overview, active work
├── BNI Visitor Host.md               # Task (plain name)
├── 20260108 Presentation/            # Time-bound sub-project
│   └── _Overview.md
└── zzz-20251215-Holiday Card/        # Completed sub-project
```

### Completing a Project

When a project, sub-project, or task is done:

1. Rename with `zzz-YYYYMMDD-` prefix: `zzz-YYYYMMDD-Name/` or `zzz-YYYYMMDD-Name.md`
2. Add completion notes to the bottom of the `_Overview.md` or task file
3. Completed items sort to bottom (`zzz-` after letters)
4. Within completed items, chronological order (by date prefix)
5. Archive during annual reviews if list gets too long

**Example folder:** `Conference 2026/` → `zzz-20260315-Conference 2026/`

**Example task:** `Design Logo.md` → `zzz-20260115-Design Logo.md`

### Completion Notes Template

Add to the bottom of completed project/task files:

```markdown
---

## Completion Notes (YYYYMMDD)

**Outcome:** [What was delivered/accomplished]

**Lessons Learned:**
- [Key insight 1]
- [Key insight 2]

**Deliverables:**
- [[Link to deliverable]]
- [External URL if applicable]
```

---

## YAML Frontmatter Standards

### Standard Schema for SOPs

```yaml
---
uid: 20241229-143022
title: "Document Title"
created: 2024-12-20
modified: 2024-12-29
version: 2.0
version_date: 251229
type: [sop]
status: [evergreen]
program: [qwf]
dg-publish: true
tags: []
---
```

### Document History Section

Every SOP includes at the bottom:

```markdown
---

## Document History

*Do not use content below this line for operations.*

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 2.0 | 251229 | TIG | Added section X |
| 1.0 | 251220 | TIG | Initial release |
```

### Publishing to Transparency Site

Notes with `dg-publish: true` in YAML frontmatter become eligible for transparency.quietlyworking.org. Publishing is fully automated — no Obsidian Digital Garden plugin needed.

**How it works:**
1. `sync_transparency_site.py` scans the vault for all `.md` files with `dg-publish: true` in YAML frontmatter
2. Transforms each file: YAML frontmatter → JSON frontmatter, generates permalink, resolves wikilinks
3. Pushes to `QuietlyWorking/qwu_transparency` GitHub repo
4. Vercel auto-deploys on push (~15 seconds)

**To publish a note:**
1. Add `dg-publish: true` to frontmatter
2. Run: `python "005 Operations/Execution/sync_transparency_site.py" --json`
3. Site updates live at transparency.quietlyworking.org

**To keep private:**
- Omit the field, or set `dg-publish: false`

**Automated sync:**
- After every `/session-wrap-up` (Step 3C)
- Daily at 4 AM Pacific via n8n workflow `YnawyFKfnrOao12P`
- Discord notification to `#system-status` on success/failure

**Safety features:**
- Private User Manual (`QWU Backoffice User Manual.md`) is blocklisted by filename stem — only the `[PUBLIC]` version passes
- Leak detection scans for IP patterns, API tokens, SSH commands before pushing
- `--dry-run` flag for previewing changes without pushing

**Key files:**
| File | Purpose |
|------|---------|
| `005 Operations/Execution/sync_transparency_site.py` | Sync script (v1.0.0) |
| `005 Operations/Directives/sync_transparency_site.md` | Directive/SOP |
| `005 Operations/Workflows/transparency-site-sync.json` | n8n workflow (daily 4 AM Pacific) |

**Currently published pages (14 files):**
- Table of Contents (home), QWU Values, Tool Shed, Nonprofit Tech Access Guide
- QWC, Locals 4 Good, Code & Tips Swipe Page, OMW, IP Rights
- 3 SOPs (User Manual [PUBLIC], BNI Workflow, Automation Workflow)
- 2 Resource pages (Unreal Hotkeys, GoBrunch Media Note)

---

## Docker Fundamentals: Running Isolated Tasks

Docker lets you run code in isolated "containers"... mini computers that do one job and disappear. Your VM stays clean, and every task runs the same way every time.

### Key Concepts

| Term | What It Is | Analogy |
|------|------------|---------|
| **Image** | A template/recipe for containers | Cookie cutter |
| **Container** | A running instance of an image | The cookie |
| **Volume** | A folder shared between VM and container | A window between two rooms |

### Lesson 1: Run a Simple Command

```bash
docker run ubuntu echo "Hello from inside a container!"
```

What happens:
1. Docker downloads the `ubuntu` image (first time only)
2. Creates a container from that image
3. Runs your command inside it
4. Container disappears when done

### Lesson 2: Interactive Container

```bash
docker run -it ubuntu bash
```

The flags:
- `-i` = interactive (keep input open)
- `-t` = terminal (give me a prompt)

Your prompt changes to something like `root@a3b2c1d4:/#`... you're INSIDE the container!

### Lesson 3: Run Python Without Installing Python

```bash
docker run python:3.11 python -c 'print("Hello from Python 3.11")'
```

Docker grabs Python 3.11 and runs your code. You never installed Python on your VM!

### Lesson 4: Access Your Files from Inside a Container

```bash
docker run -v $(pwd):/app -w /app python:3.11 python -c 'import os; print(os.listdir("."))'
```

The magic flags:
- `-v $(pwd):/app` = Mount current folder INTO the container at `/app`
- `-w /app` = Start working in that folder

### Lesson 5: Run a Script with Dependencies

```bash
docker run -v $(pwd):/app -w /app python:3.11 sh -c 'pip install -r requirements.txt && python your_script.py'
```

### Lesson 6: Pass Environment Variables (API Keys)

**Never hardcode API keys!** Pass them securely:

```bash
docker run -v $(pwd):/app -w /app --env-file .env python:3.11 python your_script.py
```

### Quick Reference: Docker Commands

| Command | What It Does |
|---------|--------------|
| `docker run IMAGE` | Run a container from an image |
| `docker run -it IMAGE bash` | Interactive shell inside container |
| `docker run -v $(pwd):/app` | Mount current folder into container |
| `docker run --env-file .env` | Pass environment variables |
| `docker ps` | Show running containers |
| `docker ps -a` | Show all containers (including stopped) |
| `docker images` | Show downloaded images |
| `docker system prune` | Clean up unused containers/images |

### Real-World Pattern: Running an Agent

```bash
docker run \
  -v $(pwd):/app \
  -w /app \
  --env-file .env \
  python:3.11 \
  sh -c 'pip install -r requirements.txt && python execution/your_agent.py'
```

---

## Docker Sandbox Security

### Files in `.devcontainer/`

| File | Purpose |
|------|---------|
| `Dockerfile` | Container image definition |
| `devcontainer.json` | VS Code configuration |
| `init-firewall.sh` | Network isolation setup |

### Domain Allowlist Categories

```bash
# Core services (required)
CORE_DOMAINS=(
    "api.anthropic.com"
    "registry.npmjs.org"
    "github.com"
    "marketplace.visualstudio.com"
)

# Package registries
PACKAGE_DOMAINS=(
    "pypi.org"
    "files.pythonhosted.org"
    "registry.yarnpkg.com"
)

# MCP servers (QWF n8n)
MCP_DOMAINS=(
    "n8n.quietlyworking.org"
    "vistasocial.com"
)
```

### Adding New Domains

1. Edit `.devcontainer/init-firewall.sh`
2. Add domain to appropriate array
3. Rebuild container: Command Palette → `Dev Containers: Rebuild Container`

### Verifying Firewall

View logs inside container:
```bash
cat /var/log/firewall-init.log
```

---

## Meeting Intelligence System ⭐

### Overview

The Meeting Intelligence System transforms Zoom meetings from isolated events into relationship intelligence nodes. Every meeting captures context, every briefing surfaces that context, and over time the system builds a comprehensive map of your professional relationships.

**Components:**
1. **Post-Meeting Processing** - Automatically processes Zoom recordings when ready
2. **Pre-Meeting Briefings** - Generates relationship-aware briefings before meetings
3. **Historical Import** - Bootstraps the system with past meeting data
4. **Transcript Archive** - Searchable meeting transcripts deep-linked to Person files

### The Intelligence Flywheel

```
Meeting Scheduled (Calendar)
       ↓
Briefing Generated (20 min before)
   - Pulls context from transcript archive
   - Shows interaction history
   - Lists open action items
       ↓
Meeting Happens
   - You enter prepared
   - Better conversation quality
       ↓
Recording Processed (Zoom Pipeline)
   - Uses calendar attendees for accurate matching
   - Links to Person/Org files
   - Captures decisions, actions, goal alignment
       ↓
Transcript Archived
   - Full text searchable
   - Deep-linked from Person files
       ↓
Next Meeting with Same People
   - Briefing has richer history
   - Pattern recognition emerges
```

### Post-Meeting Processing (Zoom Pipeline)

**Trigger:** n8n webhook when Zoom recording is ready

**Pipeline Stages:**
1. **Download** - OAuth authentication, VTT transcript parsing (inline speaker format + `<v>` tags)
2. **Analyze** - Claude API extracts topics, decisions, action items, goal alignment
3. **Calendar Enrichment** - Match to Google Calendar event for attendee emails
4. **Resolve Entities** - Match participants to Person/Org files (uses calendar + transcript speakers + analysis-derived names)
5. **Contact History** - Record interaction in relationship intelligence
6. **Person Insights** - Extract and update Person files with intelligence, action items, quotes
7. **Update Vault** - Append meeting section to daily note (dedup-aware, replaces stale sections)
8. **Link Projects** - Detect and link to relevant project files (word-boundary matching, stop words)
9. **HQ Tasks** - Owner-based routing: TIG's action items → `___Tasks/` files (sync to HQ), other people's items → entity files (`003 Entities/People/[Name].md` under "Their Commitments") + Discord notification

**Scripts:**
| File | Purpose |
|------|---------|
| `zoom_pipeline.py` | Main orchestrator |
| `zoom_transcript_download.py` | OAuth + VTT parsing |
| `meeting_intel_analyze.py` | Claude API analysis |
| `meeting_entity_resolve.py` | Entity matching + SuiteDash CRM |
| `meeting_update_vault.py` | Vault file updates |
| `meeting_project_link.py` | Project detection |
| `send_meeting_followup.py` | Post-meeting follow-up emails (personalized) | v1.3.0 |
| `appreciation_followup_db.py` | Deferred appreciation state management + cancel | v1.1.0 |
| `process_appreciation_queue.py` | SMS reminders + timeout fallback poller | v1.0.0 |

**Pipeline Flowchart:** See `005 Operations/Execution/zoom_pipeline_flowchart.md` for the full 8-stage visual diagram including follow-up emails, BCC monitoring, and error handling.

**Usage:**
```bash
# Manual processing (rare - usually triggered by webhook)
.venv/bin/python "005 Operations/Execution/zoom_pipeline.py" --meeting-id ABC123 --json

# With test fixtures (no API calls)
.venv/bin/python "005 Operations/Execution/zoom_pipeline.py" --meeting-id test-123 --use-fixtures --dry-run
```

### Appreciation Followup System (SMS Wait-for-Response)

**v1.1 | Updated 2026-03-01** (v1.0 created 2026-02-08)

When `send_meeting_followup.py` can't find specific quotes for an attendee, instead of immediately sending a generic fallback, it now **defers the email** and asks TIG for a personal appreciation via SMS. The system waits up to 5 hours for TIG's reply before falling back to the generic message.

**Timeline:**
- **T+0:** SMS asks TIG "What do you appreciate about {name}?" — email is staged (not sent)
- **T+1h:** No response? SMS reminder 1
- **T+2h:** No response? SMS reminder 2 (last call)
- **T+5h:** No response? Send email with generic warm fallback, notify TIG
- **Any time before T+5h:** TIG replies via SMS → personalized email sent immediately

**Three actors:**
| Actor | Role | Trigger |
|-------|------|---------|
| `send_meeting_followup.py` v1.3.0 | **Producer** — stages deferred appreciation | Zoom pipeline stage 8 |
| `twilio_webhook_server.py` v3.5.0 | **Listener** — captures TIG's SMS reply or cancel | Incoming SMS (Priority 2.7) |
| `process_appreciation_queue.py` v1.0.0 | **Timer** — sends reminders, handles timeouts | n8n every 5 min |

**State:** `appreciation_followup_db.py` v1.1.0 with `pending_appreciations` + `appreciation_audit_log` tables. Race safety via `BEGIN IMMEDIATE` transactions.

**Commands via SMS** (when appreciations are pending):
- **Free-form text** — used as the personalized appreciation for the next pending attendee
- **"skip" / "next" / "pass"** — sends the generic fallback immediately
- **"don't send to John" / "cancel follow-up for Miller"** — cancels the follow-up entirely (no email sent, not even fallback)
- **"cancel all"** — cancels all pending follow-ups
- **Multi-recipient:** "don't send to John or Miller" — cancels specific people by name

**LLM-based intent classification (v3.5.0):** When appreciations are pending, all inbound messages (except compliance, health vitals, and video commands) are routed through an LLM classifier (STANDARD tier) that determines: appreciation text, cancel request, skip, or unrelated. Unrelated messages (e.g., "what's on my calendar?") fall through to normal routing. This replaced a keyword-exclusion list that falsely matched words like "meeting" as calendar queries.

**n8n workflow:** `appreciation-queue-poller.json` (ID: `<WORKFLOW_ID>`) — every 5 min, SSH to poller script, logs actions to #agent-log, SSH errors to #system-status.

### Meeting Reconciliation System (Defense-in-Depth)

**v2.0 | Updated 2026-01-26**

The system ensures **zero silent failures** through 4-layer protection. With 2-5 Zoom meetings per week, every meeting must be captured for relationship intelligence.

**Architecture:**
```
┌───────────────────────────────────────────────────────────────────────┐
│  LAYER 1: Webhook (Primary Path)                                      │
│  ┌──────────┐    ┌──────────────┐    ┌────────────┐                  │
│  │ Zoom     │───▶│ zoom_        │───▶│ #daily-    │ (success)        │
│  │ Webhook  │    │ pipeline.py  │    │ digest     │                  │
│  └──────────┘    └──────┬───────┘    └────────────┘                  │
│                         │            ┌────────────┐                  │
│                         └───────────▶│ #system-   │ (failure)        │
│                                      │ status     │                  │
├───────────────────────────────────────────────────────────────────────┤
│  LAYER 2: Daily Reconciliation (Safety Net) - 9 PM Pacific            │
│  ┌──────────┐    ┌──────────────┐    ┌────────────┐                  │
│  │ 9 PM     │───▶│ zoom_        │───▶│ Catches    │                  │
│  │ Schedule │    │ reconcile.py │    │ 7-day      │                  │
│  └──────────┘    │ --days 7     │    │ misses     │                  │
│                  └──────────────┘    └────────────┘                  │
├───────────────────────────────────────────────────────────────────────┤
│  LAYER 3: Weekly Deep Scan (Full Recovery) - Sunday 3 AM              │
│  ┌──────────┐    ┌──────────────┐    ┌────────────┐                  │
│  │ Sunday   │───▶│ zoom_        │───▶│ Catches    │                  │
│  │ 3 AM     │    │ reconcile.py │    │ 30-day     │                  │
│  └──────────┘    │ --days 30    │    │ misses     │                  │
│                  │ --retry-     │    │ + retries  │                  │
│                  │ failed       │    │ failures   │                  │
│                  └──────────────┘    └────────────┘                  │
├───────────────────────────────────────────────────────────────────────┤
│  LAYER 4: Health Monitoring (Observability) - Every 4 hours           │
│  ┌──────────┐    ┌──────────────┐    ┌────────────┐                  │
│  │ Every    │───▶│ zoom_health_ │───▶│ Alerts if  │                  │
│  │ 4 hours  │    │ check.py     │    │ unhealthy  │                  │
│  └──────────┘    └──────────────┘    └────────────┘                  │
├───────────────────────────────────────────────────────────────────────┤
│                      ┌────────────────────────┐                      │
│                      │  meetings_tracker.db   │                      │
│                      │  (005 Operations/Data/)│                      │
│                      │  • Locking prevents    │                      │
│                      │    race conditions     │                      │
│                      │  • Status tracking     │                      │
│                      └────────────────────────┘                      │
└───────────────────────────────────────────────────────────────────────┘
```

**How It Works:**
1. **Layer 1 (Webhook):** Zoom webhook fires → n8n SSH to `zoom_pipeline.py` → success to #daily-digest, failure to #system-status
2. **Layer 2 (Daily):** 9 PM Pacific queries Zoom API for last 7 days → processes any missed webhooks
3. **Layer 3 (Weekly):** Sunday 3 AM deep scan of last 30 days → force-retries failed meetings
4. **Layer 4 (Health):** Every 4 hours checks pending count, failure count, hours since success → alerts if unhealthy
5. **Locking:** SQLite exclusive transactions prevent webhook/reconciliation race conditions

**Scripts:**
| File | Purpose | Version |
|------|---------|---------|
| `zoom_pipeline.py` | Main processing orchestrator | v1.12.0 |
| `zoom_transcript_download.py` | OAuth + VTT parsing (inline speaker support) | v1.2.0 |
| `meeting_intel_analyze.py` | Claude API analysis | v1.1.0 |
| `meeting_entity_resolve.py` | Entity matching + SuiteDash CRM | v1.0.0 |
| `meeting_update_vault.py` | Vault file updates (dedup-aware) | v1.2.0 |
| `meeting_project_link.py` | Project detection (word-boundary matching) | v1.1.0 |
| `zoom_reconcile.py` | Reconciliation - discovers and processes missed meetings (defense-in-depth: content-aware classification, targeted UUID recheck, 3-tier in-progress detection with 4-hour time gate, Discord escalation, HQ task on permanent skip) | v1.6.0 |
| `zoom_health_check.py` | Health monitoring - detects system issues | v1.0.0 |
| `zoom_list_recordings.py` | Query Zoom API for recent cloud recordings | v1.0.0 |
| `meeting_tracker.py` | SQLite tracking with locking | v1.1.0 |

**n8n Workflows:**
| Workflow | Schedule | Purpose |
|----------|----------|---------|
| Zoom Recording Webhook | On webhook | Primary processing path |
| Zoom Meeting Reconciliation - Daily | 9 PM Pacific | Catch webhook failures |
| Zoom Meeting Reconciliation - Weekly Deep Scan | Sunday 3 AM | Full 30-day recovery |
| Zoom Meeting Health Monitor | Every 4 hours | Proactive issue detection |

**Usage:**
```bash
# Check health status
.venv/bin/python "005 Operations/Execution/zoom_health_check.py"
.venv/bin/python "005 Operations/Execution/zoom_health_check.py" --json

# Check reconciliation status
.venv/bin/python "005 Operations/Execution/zoom_reconcile.py" --status

# Dry-run reconciliation (check what would be processed)
.venv/bin/python "005 Operations/Execution/zoom_reconcile.py" --dry-run --json

# Run reconciliation (7-day lookback)
.venv/bin/python "005 Operations/Execution/zoom_reconcile.py" --json

# Run deep scan (30-day lookback with retry-failed)
.venv/bin/python "005 Operations/Execution/zoom_reconcile.py" --days 30 --retry-failed --json

# Force-process a specific meeting (bypasses tracker status)
.venv/bin/python "005 Operations/Execution/zoom_pipeline.py" --meeting-id "UUID==" --force --json

# Check tracker stats
.venv/bin/python "005 Operations/Execution/meeting_tracker.py" --stats

# List Zoom recordings from last 7 days
.venv/bin/python "005 Operations/Execution/zoom_list_recordings.py" --days 7
```

**Failure Scenarios:**
| Scenario | What Happens |
|----------|--------------|
| Webhook arrives, pipeline succeeds | Processed immediately, #daily-digest notification |
| Webhook arrives, pipeline fails | #system-status alert, retry at 9 PM reconciliation |
| Webhook missed | Discovered at 9 PM, processed, #system-status report |
| SSH failure | #system-status SSH error alert |
| Pipeline fails 3+ times | Flagged "needs attention", appears in health check |
| Transcript not ready (Zoom still processing) | `skipped_transient` with 7 retry attempts. Defense-in-depth chain: content detection (empty meetings skip immediately), targeted UUID recheck on final attempt, Discord escalation + starred HQ task on permanent skip |
| Extended outage | Sunday 3 AM deep scan recovers up to 30 days back |
| System unhealthy | Health monitor alerts every 4 hours until resolved |

> **Missing Pixel Training Opportunity (Tier 3: Specialist)**
>
> The Defense-in-Depth architecture teaches enterprise-grade reliability patterns:
> - **Multi-layer redundancy** - Primary + backup + deep scan + monitoring (defense-in-depth)
> - **SQLite locking** - Exclusive transactions, stale lock detection, race condition prevention
> - **n8n error handling** - `onError: continueErrorOutput`, error branches, failure alerting
> - **Health monitoring** - Threshold-based alerting, status dashboards, observability
> - **Idempotent design** - Making operations safe to retry without side effects
>
> **Exercise:** Design a Defense-in-Depth system for a different webhook service (e.g., Stripe payments). Include: (1) primary webhook handler with error alerting, (2) daily reconciliation, (3) weekly deep scan, (4) health monitoring. Document your 4-layer architecture diagram.

### Pre-Meeting Briefings

**Trigger:** n8n polls calendar every 15 minutes, generates briefings 20 minutes before meetings

**Briefing Includes:**
- Attendee profiles with circle status (inner, trusted, professional, new)
- Last interaction history (from daily notes)
- Open action items (unchecked tasks mentioning the person)
- Organization context
- Suggested agenda template
- "Definition of Success" placeholders

**Scripts:**
| File | Purpose |
|------|---------|
| `calendar_monitor.py` | Check for upcoming meetings, coordinate briefings |
| `meeting_briefing.py` | Generate briefing content |

**Usage:**
```bash
# Check upcoming meetings
.venv/bin/python "005 Operations/Execution/calendar_monitor.py" --check-upcoming --minutes 60

# Generate briefings for next hour
.venv/bin/python "005 Operations/Execution/calendar_monitor.py" --check-upcoming --generate-briefings --minutes 60 --dry-run

# Manual briefing for specific meeting
.venv/bin/python "005 Operations/Execution/meeting_briefing.py" --topic "Q1 Planning" --names "Sue,[Participant]" --duration 60
```

### Pre-Meeting Prep Emails ⭐ NEW

**v1.0 | Added 2026-02-07**

Automated 7-day-ahead emails to external meeting attendees, sent in Ezer's voice. Also generates 30-day enriched briefings for the HQ Command Center "Upcoming Meetings" module.

**Architecture:**
```
Google Calendar (30-day lookahead)
       ↓
Filter External Attendees (skip TIG, @quietlyworking.org, resource calendars)
       ↓
Vault Enrichment (entity file, meeting history, outstanding actions, intelligence)
       ↓
Contact History (last contact date, relationship health assessment)
       ↓
├── [7-day emails] → SQLite dedup check → MS Graph send → Discord #agent-log
└── [30-day briefings] → Enriched JSON → HQ Upcoming Meetings module
```

**Key Features:**
- **7-day lookahead emails** — Warm, concise prep email asking attendees for agenda input
- **30-day enriched briefings** — Full attendee profiles with vault data, relationship health, outstanding actions
- **SQLite dedup** — UNIQUE(event_id, attendee_email) prevents duplicate sends
- **Relationship health assessment** — thriving (≤14d) → healthy (≤30d) → stable (≤60d) → cooling (≤90d) → dormant (>90d)

**Scripts:**
| File | Purpose | Version |
|------|---------|---------|
| `send_meeting_prep_email.py` | 7-day emails + 30-day briefings | v1.0.0 |

**n8n Workflows:**
| Workflow | Schedule | Purpose |
|----------|----------|---------|
| Meeting Prep Email - Daily | 9 AM Pacific | Send prep emails + generate briefings |

**Usage:**
```bash
# Send 7-day prep emails (dry run)
.venv/bin/python "005 Operations/Execution/send_meeting_prep_email.py" send --dry-run --json

# Generate 30-day enriched briefings for HQ module
.venv/bin/python "005 Operations/Execution/send_meeting_prep_email.py" briefings --days 30 --json

# Check send status
.venv/bin/python "005 Operations/Execution/send_meeting_prep_email.py" status --json

# Cleanup old records (60+ days)
.venv/bin/python "005 Operations/Execution/send_meeting_prep_email.py" cleanup --days 60
```

**HQ Integration:**
The `briefings` subcommand returns enriched JSON consumed by the HQ Command Center's "Upcoming Meetings" module. Each meeting includes: attendee vault profiles, last met date, outstanding actions, intelligence snippets, relationship health scores, and prep email status.

See `002 Projects/_HQ Command Center/handoff-meeting-intelligence-pipeline.md` for the full JSON schema and HQ integration guide.

### Meeting-Ready BNI 1-2-1 Briefings ⭐ NEW

**v1.0 | Added 2026-01-20**

Enhanced briefings specifically for BNI 1-2-1 meetings that serve as **working documents during the meeting itself** (not just pre-meeting prep).

**Key Features:**
1. **Template Integration** - Maps BNI 1-2-1 Meeting Template questions to entity data
2. **Intel Status Indicators:**
   - ✅ **Confirmed** - Data exists in entity file
   - ⚠️ **Partial** - Data exists but needs verification
   - ❓ **Unknown** - Need to ask during meeting
3. **Enhanced Review Intel:**
   - Star distribution table (count at each 1-5 star level)
   - Verbatim customer quotes (10-20 examples)
   - "No negative reviews" explicit messaging
   - Review trends (improving/stable/declining)
4. **Meeting Capture Space** - Action items, relationship assessment, notes

**Usage:**
```bash
.venv/bin/python "005 Operations/Execution/generate_121_briefing.py" "[Member Name]" \
  --date "2026-01-20" --time "13:00" --location "In-person" --type "BNI 1-2-1"
```

**Output Sections:**
- Quick Contact info
- Customer Review Intel (star distribution, verbatim quotes)
- Discovery Checklist (with intel status for each template question)
- Power Team Exploration
- Personal Connection gaps
- Communication Preferences
- My Referral TO Them (capture space)
- Action Items (my commitments, their commitments, next 1-2-1)
- Relationship Assessment

**Related Scripts:**
| File | Purpose |
|------|---------|
| `generate_121_briefing.py` | Generate meeting-ready BNI 1-2-1 briefings |
| `enrich_member_reviews.py` v1.3 | Enhanced review intel with star distribution |

### 1-2-1 Recording Processing ⭐ NEW

**v1.0 | Added 2026-01-21**

Process audio recordings from in-person 1-2-1 meetings (Voice Memos, etc.) into structured intelligence for Person entity files.

**Pipeline:**
```
Audio Recording (Voice Memo/m4a)
       ↓
[Compress if >25MB] (ffmpeg)
       ↓
[transcribe_121_recording.py] → Whisper API
       ↓
Transcript (.json + .md)
       ↓
[extract_121_insights.py] → Claude API
       ↓
Structured Insights (personal, professional, action items)
       ↓
Entity File Update
       ↓
[Archive & Cleanup]
├── Transcripts → 100 Resources/Meeting Transcripts/YYYY/YYYYMMDD-slug/
├── Recording → Google Drive: Meetings/YYYY/YYYYMMDD-slug/
└── Delete .tmp files
```

**File Storage Architecture:**

| Artifact | Location | Retention |
|----------|----------|-----------|
| Original recording | Google Drive: `Meetings/YYYY/YYYYMMDD-slug/original.m4a` | Permanent |
| Transcript JSON | `100 Resources/Meeting Transcripts/YYYY/YYYYMMDD-slug/transcript.json` | Permanent |
| Transcript MD | `100 Resources/Meeting Transcripts/YYYY/YYYYMMDD-slug/transcript.md` | Permanent |
| Insights JSON | `100 Resources/Meeting Transcripts/YYYY/YYYYMMDD-slug/insights.json` | Permanent |
| Entity updates | `003 Entities/People/{person}.md` | Permanent |

**Naming Convention:** `YYYYMMDD-firstname-lastname-121` (all lowercase, hyphens)

**Scripts:**
| File | Purpose |
|------|---------|
| `transcribe_121_recording.py` | Audio → transcript via Whisper API |
| `extract_121_insights.py` | Transcript → structured insights via Claude |
| `gdrive_upload.py` | Upload recordings to Google Drive shared drive |

**Usage:**
```bash
# Step 1: Transcribe
.venv/bin/python "005 Operations/Execution/transcribe_121_recording.py" \
  --file /path/to/recording.m4a --person "[Member Name]"

# Step 2: Extract insights (preview first)
.venv/bin/python "005 Operations/Execution/extract_121_insights.py" \
  --file .tmp/121_transcripts/2026-01-21_Ramona_Petersen_transcript.json --preview

# Step 3: Apply to entity
.venv/bin/python "005 Operations/Execution/extract_121_insights.py" \
  --file .tmp/121_transcripts/2026-01-21_Ramona_Petersen_transcript.json --update-entity

# Step 4: Archive (after verifying entity updates)
mkdir -p "100 Resources/Meeting Transcripts/2026/20260121-ramona-petersen-121"
mv .tmp/121_transcripts/*Ramona* "100 Resources/Meeting Transcripts/2026/20260121-ramona-petersen-121/"

# Step 5: Upload recording to Drive
.venv/bin/python "005 Operations/Execution/gdrive_upload.py" \
  --file ".tmp/original.m4a" --folder "Meetings/2026/20260121-ramona-petersen-121" --name "original.m4a"
```

**Directive:** `005 Operations/Directives/process_121_recording.md`

### Historical Import

Import past Zoom recordings to bootstrap relationship intelligence.

**What it does:**
- Scans local folder of downloaded Zoom recordings
- Parses VTT transcripts
- Archives as searchable markdown in `100 Resources/Meeting Transcripts/`
- Creates draft Person files for unknown people
- Updates existing Person files with meeting history
- Deep-links everything

**Script:** `zoom_history_import.py`

**Usage:**
```bash
# Scan without changes
.venv/bin/python "005 Operations/Execution/zoom_history_import.py" --scan

# Full import (transcripts + drafts + history)
.venv/bin/python "005 Operations/Execution/zoom_history_import.py" --full-import

# Dry run first
.venv/bin/python "005 Operations/Execution/zoom_history_import.py" --full-import --dry-run
```

### Transcript Archive

Location: `100 Resources/Meeting Transcripts/`

Format: Searchable markdown with YAML frontmatter

```yaml
---
type: meeting-transcript
tags: [transcript, imported]
source: "Auto-generated from private manual v3.44 by generate_public_manual.py"
generated: "2026-03-17 08:02"
date: 2025-07-18
topic: "Time with Sue & [Participant]"
duration_minutes: 69
word_count: 6103
speakers: [TIG, [Member Name]]
---
```

Deep-linked from Person files:
```markdown
- **2025-07-18** - Time with Sue & [Participant] (69 min) [[Meeting Transcripts/2025-07-18 - Time with Sue & [Participant].md|📝]]
```

### Configuration

**Environment Variables:**
```bash
# Zoom OAuth (required for live processing)
ZOOM_ACCOUNT_ID=your_account_id
ZOOM_CLIENT_ID=your_client_id
ZOOM_CLIENT_SECRET=your_client_secret
ZOOM_WEBHOOK_SECRET=your_webhook_secret

# Google Calendar (already configured)
GOOGLE_CALENDAR_CREDENTIALS=/path/to/service-account.json
GOOGLE_CALENDAR_MAIN=calendar_id@group.calendar.google.com

# Discord (for notifications)
DISCORD_WEBHOOK_DAILY_DIGEST=https://discord.com/api/webhooks/...

# Anthropic (for analysis)
ANTHROPIC_API_KEY=your_api_key
```

**n8n Workflows:**
| Workflow | File | Schedule |
|----------|------|----------|
| Pre-Meeting Briefings | `pre-meeting-briefing-monitor.json` | Every 15 min |
| Meeting Prep Email - Daily | `meeting-prep-email-daily.json` | 9 AM Pacific |
| Zoom Recording Webhook | `zoom-recording-webhook.json` | On webhook |

**Directives:**
- `005 Operations/Directives/pre_meeting_briefing.md`
- `005 Operations/Directives/process_zoom_recording.md`
- `005 Operations/Directives/process_121_recording.md`

### Phase 3 Roadmap

Review scheduled: **April 10, 2026**

Potential enhancements:
- Morning digest (all meetings for the day)
- Relationship health alerts ("You haven't met with X in 30 days")
- AI-suggested meeting prep questions
- ~~Post-meeting auto-follow-up drafts~~ → ✅ Built (`send_meeting_followup.py` v1.3.0 — personalized action items, deferred appreciation with SMS wait-for-response, preference footer, opt-out check)
- ~~Appreciation wait-for-response (SMS retry + timeout + cancel)~~ → ✅ Built (`appreciation_followup_db.py` v1.1.0 + `process_appreciation_queue.py` v1.0.0 — T+1h/T+2h SMS reminders, T+5h fallback email, Twilio reply handler, LLM-based cancel via SMS)
- ~~Pre-meeting prep emails~~ → ✅ Built (`send_meeting_prep_email.py` — preference footer, opt-out check)
- Meeting pattern analytics
- Voice capture for quick context additions

---

## Outlook Email Processing ⭐

### Overview

The Outlook Email Processing system automatically monitors Microsoft 365 Outlook inbox and sent items, classifies emails, resolves sender entities, updates vault files with correspondence history, and creates tasks for action items. It integrates with SuiteDash CRM for relationship-aware processing.

**Philosophy:** Email handles people and conversations. RSS feeds handle content and newsletters. This separation keeps the vault focused on relationships.

### Pipeline Architecture

```
Outlook (Inbox + Sent Items)
     │
     ▼
[outlook_fetch_emails.py] ← Microsoft Graph API (OAuth2)
     │  Fetch from: Inbox, SentItems
     │
     ▼
[email_classify.py] ← Claude API
     │  Classifications: action-required, waiting-on, informational,
     │                   conversation, transactional, newsletter
     │
     ▼
[email_entity_resolve.py]
     │  1. Match contact → Person file (email, name, alias)
     │     - Received: resolve sender
     │     - Sent: resolve recipient
     │  2. Query SuiteDash CRM (if not in vault)
     │  3. Create [DRAFT] for significant unknowns
     │  4. Detect circle tier (inner/trusted/professional/new)
     │
     ├── VIP? → Discord #inbox-alerts (immediate)
     │
     ▼
[email_update_vault.py]
     ├── Person file: ### Email Thread section
     ├── Daily journal: ## Email Activity table
     │
     ▼
[email_task_create.py] (if action-required)
     │  → 000 Inbox/___Tasks/
     │
     ▼
[Sender Tracking] (v1.6.0)
     │  → hq_email_senders (Supabase) — PostgREST upsert
     │
     ▼
[Newsletter Audit] (if newsletter detected)
     └── → 000 Inbox/___Review/Newsletter-Audit.md
```

### Email Classification Types

| Type | Description | Action |
|------|-------------|--------|
| `action-required` | Needs response or action | Create task, priority alert |
| `waiting-on` | Awaiting their reply | Track in "Waiting On" |
| `informational` | FYI, announcements | Log only |
| `conversation` | Ongoing thread | Update thread summary |
| `transactional` | Receipts, confirmations | Archive, minimal processing |
| `newsletter` | Marketing emails | Route to Newsletter Audit |

### VIP Handling

VIP contacts get immediate Discord notifications and priority processing:
- **Inner circle** contacts (from SuiteDash)
- Emails/domains in `OUTLOOK_VIP_EMAILS` / `OUTLOOK_VIP_DOMAINS`

### Scripts

| File | Purpose |
|------|---------|
| `outlook_pipeline.py` | Main orchestrator (v1.6.0 — suppression pre-check + sender tracking to `hq_email_senders`) |
| `outlook_fetch_emails.py` | Microsoft Graph API: OAuth, fetch, pagination |
| `email_classify.py` | Claude API classification of email intent |
| `email_entity_resolve.py` | Match sender to People/Organizations, SuiteDash CRM lookup |
| `email_update_vault.py` | Append correspondence sections to vault files |
| `email_task_create.py` | Create tasks for action items (with deduplication & consolidation) |

### Task Creation Intelligence (v1.3.0)

Not all `action-required` emails need a task. The system uses intelligent filtering to reduce noise:

**Task Creation Rules:**
Only create a task when ALL conditions are met:
1. Classification is `action-required`
2. `effort_level` is `moderate` or `significant` (not trivial/quick)
3. `action_type` is `research` or `project` (not reply/calendar/routine)
4. Due date is in the future (or not set)
5. Email is NOT forwarded (no "Fw:", "Fwd:" prefix)
6. Subject doesn't match exclude patterns in `OUTLOOK_TASK_EXCLUDE_PATTERNS`
7. No existing task for same person + similar topic in last 7 days

**What DOESN'T Become a Task:**
| Type | Handling |
|------|----------|
| Quick replies | Just respond in email, no task needed |
| Calendar events | Add to calendar instead |
| Routine notifications | Log only (BNI visitors, invoices, etc.) |
| Forwarded emails | Already being actioned |
| Past-due items | Event already happened |

**Classification Fields (from Claude):**
- `effort_level`: trivial, quick, moderate, significant
- `action_type`: reply, calendar, research, project, routine

**Duplicate Detection:**
- Jaccard similarity (70% threshold) checks existing task titles
- Person+topic dedup: Skip if same person + 2+ matching keywords in last 7 days
- Prevents task pile-up from repeated email reminders

**Person Consolidation:**
- Multiple action items from the same person/org are grouped into one consolidated task
- Consolidated tasks include a checklist of all action items with email context
- Uses the highest priority among all grouped items
- Tagged with `["email-task", "consolidated"]` for filtering

**Environment Variable:**
```bash
# Add to .env for pattern-based filtering
OUTLOOK_TASK_EXCLUDE_PATTERNS=BNI: A visitor has registered,Your invoice is ready,Your weekly report
```

**Example:** If Alice sends 3 research-related emails, the system creates one task "Multiple action items from Alice Smith (3 items)" with a checklist. But if she sends a quick "yes, confirmed" reply, no task is created.

### Usage

```bash
# Manual run (usually triggered by n8n)
.venv/bin/python "005 Operations/Execution/outlook_pipeline.py" --json

# With options
.venv/bin/python "005 Operations/Execution/outlook_pipeline.py" \
  --limit 10 \
  --dry-run \
  --json

# Test with fixtures
.venv/bin/python "005 Operations/Execution/outlook_pipeline.py" \
  --use-fixtures \
  --dry-run \
  --json
```

### n8n Workflow

**Workflow:** `outlook-email-workflow.json`
**Schedule:** Every 15 minutes

**Flow:**
```
Schedule Trigger (every 15 min)
    → SSH: Run outlook_pipeline.py --json
    → Parse JSON output
    → If emails_processed > 0:
        → Post to #agent-log
        → If vip_count > 0: Post to #inbox-alerts (VIP alert)
        → If tasks_created > 0: Post to #inbox-alerts (task alert)
```

### Directive

**Full documentation:** `005 Operations/Directives/process_outlook_email.md`

---

## SuiteDash CRM Integration ⭐

### Overview

SuiteDash is QWF's CRM platform. The QWU Backoffice integrates with SuiteDash to provide relationship-aware automation across all pipelines (email, meetings, briefings).

**Key Concepts:**
- **Circles** = SuiteDash groupings that control portal access and marketing
- **Tiers** = QWF relationship levels (Inner, Trusted, Professional, New)
- **Two-way sync** = Vault Person files ↔ SuiteDash contacts

### Circle Architecture

#### The Two Circle Systems

| Relationship Tiers | Purpose |
|--------------------|---------|
| Inner | Full trust, immediate response, highest priority |
| Trusted | Proven relationships, same-day response |
| Professional | Active business relationships, 24-48 hour response |
| New | Fresh contacts, unproven |
| Unknown | Not in system |

#### Tier → Priority Mapping

| Tier | Email Priority | Meeting Priority | Access Level |
|------|----------------|------------------|--------------|
| Inner | Immediate alert | Direct calendar | Full transparency |
| Trusted | High | Priority slots | Project-level |
| Professional | Normal | Standard booking | Standard |
| New | Normal | Limited slots | Basic |

#### SuiteDash Circle Names

| Circle Name | Relationship Tier | Purpose |
|-------------|-------------------|---------|
| `Chaplain TIG Inner Circle` | Inner | Highest trust, manual only |
| `QWF Trusted` | Trusted | Proven relationships |
| `QWF Professional` | Professional | Active business |
| `QWF New` | New | Default for new contacts |

### Two-Way Sync Architecture

```
┌─────────────────────┐         ┌─────────────────────┐
│  Obsidian Vault     │         │  SuiteDash CRM      │
│  003 Entities/      │         │                     │
│  People/*.md        │◀───────▶│  Contacts           │
│                     │         │                     │
│  - YAML frontmatter │  sync   │  - Custom fields    │
│  - circle: trusted  │─────────│  - Circle membership│
│  - suitedash_id     │         │  - Program status   │
└─────────────────────┘         └─────────────────────┘
```

#### Sync Direction 1: Vault → SuiteDash

**Script:** `vault_to_suitedash.py`
**Schedule:** Daily at 6:00 AM Pacific
**What syncs:** Person file frontmatter → SuiteDash custom fields

#### Sync Direction 2: Tier → Circles

**Script:** `circle_sync.py`
**Schedule:** Daily at 6:30 AM Pacific (after vault sync)
**What syncs:** Person's calculated tier → SuiteDash Circle membership

**How tier is determined:**
1. Read Person's program statuses from vault frontmatter
2. Apply tier mapping (e.g., MP `maintainer` = Inner, QWC `active` = Trusted)
3. Use highest applicable tier
4. Update SuiteDash Circle membership

### Scripts

| File | Purpose |
|------|---------|
| `vault_to_suitedash.py` | Push vault Person data → SuiteDash custom fields |
| `circle_sync.py` | Sync relationship tier → SuiteDash Circle membership |
| `suitedash_contacts.py` | SuiteDash API wrapper: lookup, create, update contacts |

### n8n Workflows

| Workflow | Schedule | Purpose |
|----------|----------|---------|
| `vault-to-suitedash-workflow.json` | Daily 6:00 AM | Sync vault → SuiteDash fields |
| `circle-sync-workflow.json` | Daily 6:30 AM | Sync tiers → Circle membership |

### Usage

```bash
# Vault → SuiteDash sync
.venv/bin/python "005 Operations/Execution/vault_to_suitedash.py" --all --json

# Circle tier sync
.venv/bin/python "005 Operations/Execution/circle_sync.py" --all --json

# Dry run (preview without changes)
.venv/bin/python "005 Operations/Execution/circle_sync.py" --all --dry-run --json
```

### Integration Points

SuiteDash CRM data is used by:
- **Email Processing** → Detect circle tier for priority handling
- **Meeting Intelligence** → Include circle status in briefings
- **Pre-Meeting Briefings** → Show relationship context
- **Entity Resolution** → Create full Person files for unknown contacts found in CRM

### Directives

**Full documentation:**
- `005 Operations/Directives/circle_architecture.md` (comprehensive tier definitions)
- `005 Operations/Directives/sync_vault_to_suitedash.md` (vault → CRM sync)

---

## Transcript Extraction System (Planned)

### Purpose

Extract detailed transcripts from Claude Code sessions for:
- Student curriculum (showing how agents think)
- Transparency publishing
- Debugging and improvement

### Adaptation from Simon Willison's Tool

Based on [claude-code-transcripts](https://github.com/simonw/claude-code-transcripts), adapted for QWU:

| Simon's Approach | QWU Adaptation |
|-----------------|----------------|
| HTML output | Obsidian Markdown |
| GitHub Gists | transparency.quietlyworking.org |
| Standalone tool | Integrated with DOE architecture |
| Generic naming | QWU tag taxonomy + YAML frontmatter |

### Output Location

```
qwu_backOffice/
└── transparency/
    └── agent-transcripts/
        ├── _index.md
        ├── 2024-12-30-backoffice-auth-fix.md
        └── 2024-12-30-vista-social-setup.md
```

**Status:** Planning phase. Implementation TBD.

---

## Ez/Ezer Mascot

QWF's official mascot... an intelligent, empathetic octopus composed of transformable pixel-blocks.

### Character Details

| Attribute | Description |
|-----------|-------------|
| Name | Ez or Ezer (Hebrew: "strength, warrior-ally") |
| Form | Octopus made of "stoicheia" pixel-blocks |
| Connection | Each block represents a Missing Pixel student |
| Personality | Background empowerer, patient teacher |
| Visual Style | Colorful, transformable, adaptive |

### Why an Octopus?

- Multiple arms reaching out to help
- Highly intelligent and adaptable
- Each arm can work independently (like QWF's programs)
- Soft exterior, strong interior (vulnerability + strength)

### Character Bible Location

Full character bible (visual guidelines, personality, animation principles) stored in:
`Resources/Brand/ez-ezer-character-bible.md`

---

## Ez Terminal (Scheduler) ⭐ NEW

**Added: Session 42 (January 23, 2026) | Updated: Session 48 (January 24, 2026)**

The Ez Terminal is an interactive retro-styled terminal interface for scheduling appointments with TIG. Available at https://qwu-twin.quietlyworking.org (port 8765)

### Version History

| Version | Date | Key Features |
|---------|------|--------------|
| v5.0.0 | 260124 | QWU Universe adventure, TIG Trivia, Guestbook, 4 Easter Eggs |
| v4.0.0 | 260123 | Oregon Trail game with cross-session save |
| v3.9.0 | 260123 | Achievements system (40 achievements, 8 categories) |
| v3.8.0 | 260122 | Smart Suggestions system |
| v3.7.0 | 260122 | Daily Wisdom system |
| v3.6.0 | 260122 | Cross-session memory via localStorage |
| v3.5.0 | 260122 | Recognized Identities (TIG device detection) |
| v3.3.0 | 260118 | Initial deployment |

### Features

**Core Scheduling:**
- Circle-based scheduling with access tiers (inner, trusted, professional, new, unknown)
- Calendar integration with Google Calendar
- Multiple theme support (green, amber, matrix, deep sea, synthwave)

**Engagement Systems:**
- **Daily Wisdom:** Rotating quotes from TIG's reading list, one per day per visitor
- **Smart Suggestions:** Contextual command recommendations based on session state
- **Oregon Trail:** Classic game ported to JavaScript with full save/load support
- **QWU Universe:** Text adventure exploring the QWF ecosystem (v5.0.0)
- **TIG Trivia:** Quiz game on TIG izms, QWF programs, and pop culture (v5.0.0)
- **Guestbook:** Leave messages for future visitors (v5.0.0)

**Achievement System (v3.9.0 → v5.0.0):**
- 47 achievements across 8+ categories (expanded in v5.0.0):
  - Explorer (navigation), Traveler (visits), Sage (wisdom), Connector (scheduling)
  - Timekeeper (sessions), Lorekeeper (stories), Legendary (epic feats), Hidden (secrets)
  - Adventurer (games, trivia, guestbook), Easter Eggs (secrets found)
- 5-tier point system: Bronze (10), Silver (25), Gold (50), Platinum (100), Diamond (250)
- Commands: `achievements`, `trophies`, `badges`, `achievements all`
- Persistent tracking via localStorage

**Oregon Trail (v4.0.0):**
- Full game with 15 landmarks (Independence, MO → Willamette Valley)
- Party management, shop system, hunting, river crossings
- Random events: diseases, weather, encounters, equipment failures
- Cross-session save: game state persists in localStorage
- Commands: `trail`, `oregon`, `oregon trail`

**QWU Universe Adventure (v5.0.0):**
- 12+ explorable locations representing the QWF ecosystem
- Locations: Gates of Hope, WHELHO Plaza, TIG's Lighthouse, Dream Forge (L4G), Gratitude Garden, Legacy Summit, Mentor's Grove, Reflection Pool, Archive of Dreams, Chamber of Origins, Hope's Heart
- 9 collectible items with narrative significance
- 5 NPCs with dialog trees (Blacksmith, Mentor, Ez, Keeper, Librarian)
- Commands: `adventure`, `universe`

**TIG Trivia (v5.0.0):**
- Three categories: TIG izms, QWF Programs, Pop Culture (Ted Lasso, Firefly, Star Trek)
- Streak bonuses for consecutive correct answers
- Score tracking with achievements
- Commands: `trivia`

**Easter Eggs (v5.0.0):**
14 total secrets discoverable through hidden commands and behaviors:

| Command | Secret Name | Theme |
|---------|-------------|-------|
| `kobayashi`, `kobayashi maru` | Kobayashi Wisdom | Star Trek |
| `firefly`, `serenity` | Firefly Fan | Firefly |
| `believe`, `ted lasso` | Believe Sign | Ted Lasso |
| `biscuits` | Biscuit Box | Ted Lasso |
| `lumala` (as name) | lumala | QWU Lore |
| `lum netsach` | Lum Netsach | QWU Lore |
| `pix`, `the pix` | Pix Seeker | Missing Pixel |
| `splinter` | Splinter Whisper | QWU Lore |
| `most precious one`, `mpo` | MPO Memory | QWU Lore |
| `philippi` | Philippi's Legacy | QWU Lore |
| `ezer`, `who are you` | Ez Origin | QWU Lore |
| 10+ visits | Loyal Friend | Behavioral |
| `theme deep` | Deep Dweller | Behavioral |
| `sdf` x3 | SDF Master | Behavioral |

### Commands Reference

| Command | Description |
|---------|-------------|
| `help` | Show available commands |
| `book`, `schedule` | Start scheduling flow |
| `wisdom` | View daily wisdom quote |
| `achievements` | View unlocked achievements |
| `trail` | Start/continue Oregon Trail |
| `adventure` | Start QWU Universe adventure |
| `trivia` | Start TIG Trivia game |
| `guestbook` | View/sign the guestbook |
| `theme <name>` | Change terminal theme |
| `clear` | Clear terminal output |

### Files

| File | Purpose |
|------|---------|
| `002 Projects/Terminal-Scheduler/index.html` | Main terminal interface (single-file app) |
| `005 Operations/Execution/oregon_trail.py` | Python backend (reference implementation) |
| `005 Operations/Execution/ezer_memory.py` | Session memory management |
| `005 Operations/Execution/scheduling_rules.py` | Circle-based scheduling rules |

### Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│  Ez Terminal v5.0.0 (Browser)                                   │
├─────────────────────────────────────────────────────────────────┤
│  ┌───────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐  │
│  │ Scheduling│ │ Achievements│ │ Oregon Trail│ │QWU Universe │  │
│  │ Flow      │ │ Manager     │ │ Game Engine │ │ Adventure   │  │
│  └─────┬─────┘ └──────┬──────┘ └──────┬──────┘ └──────┬──────┘  │
│        │              │               │               │         │
│        │   ┌──────────┴───────────────┴───────────────┘         │
│        │   │   ┌─────────────┐ ┌─────────────┐                  │
│        │   │   │ TIG Trivia  │ │  Guestbook  │                  │
│        │   │   │ Engine      │ │  System     │                  │
│        │   │   └──────┬──────┘ └──────┬──────┘                  │
│        │   │          │               │                         │
│        └───┴──────────┼───────────────┘                         │
│                       │                                         │
│            ┌──────────▼──────────┐                              │
│            │  localStorage       │                              │
│            │  (session memory)   │                              │
│            └──────────┬──────────┘                              │
└───────────────────────┼─────────────────────────────────────────┘
                        │
    ┌───────────────────┼───────────────────┐
    ▼         ▼         ▼         ▼         ▼
┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐
│Identity│ │ Wisdom │ │ Trail  │ │Universe│ │ Trivia │
│ State  │ │ State  │ │ Save   │ │ Save   │ │ State  │
└────────┘ └────────┘ └────────┘ └────────┘ └────────┘
```

### Missing Pixel Training Opportunity

**Tier 2 - Contributor Level**

The Ez Terminal demonstrates several teachable concepts:

| Skill | What Students Learn |
|-------|---------------------|
| Frontend JavaScript | Single-file app architecture, state management |
| localStorage API | Cross-session persistence, JSON serialization |
| Game Development | State machines, game loops, event handling |
| Terminal UI | ASCII art, text animation, command parsing |
| Achievement Systems | Progress tracking, unlock logic, notification UI |
| Text Adventure Design | Location graphs, inventory systems, NPC dialog trees |
| Quiz/Trivia Logic | Category selection, streak tracking, score management |

**Portfolio Projects Completed (v5.0.0):**
- Text adventure (QWU Universe - 12+ locations, NPCs, items)
- Trivia game (TIG Trivia - 3 categories, streaks)
- Guestbook system (moderated community messages)

**Future Extension Ideas:**
- Additional QWU Universe locations
- More trivia categories
- Theme creator tool
- Mobile gesture support

---

## Troubleshooting

### Can't Connect to VM

1. **Check if VM is running** - Azure Portal → VM should show "Running"
2. **Check IP address** - It may have changed after restart
3. **Try status webhook** - `curl "https://n8n.quietlyworking.org/webhook/vm-control?action=status"`

### VS Code Remote SSH: Stuck at "Opening Remote..."

When VS Code hangs at "Opening Remote..." for more than 2-3 minutes, the VS Code server on the remote VM has likely become corrupted or stuck.

**Diagnosis Steps:**

1. **Verify VM is running**
   - Check Azure Portal or use your mobile VM control widget
   - Confirm the VM isn't stopped or deallocated

2. **Test direct SSH connection**
   ```bash
   ssh claude-dev-vm
   ```
   - If this hangs: problem is network or VM itself
   - If this connects: problem is VS Code server (continue below)

3. **Check VS Code logs**
   - In VS Code: `View → Output`
   - Select "Remote - SSH" from dropdown
   - Look for where the connection stalls

**Resolution Steps:**

Once SSH confirms the VM is accessible:

1. **Kill zombie VS Code server processes**
   ```bash
   pkill -f vscode-server
   ```

2. **Remove corrupted VS Code server cache**
   ```bash
   rm -rf ~/.vscode-server
   ```

3. **Reconnect from VS Code**
   - Close VS Code completely on local machine
   - Reopen and connect to remote
   - VS Code will reinstall server automatically
   - Extensions will reinstall on first connect (takes ~1 minute)

**Prevention Tips:**
- Avoid force-closing VS Code while remote operations are in progress
- If disconnecting for extended periods, use `Remote-SSH: Close Remote Connection` command first
- Keep VS Code and Remote SSH extension updated

**Related Commands:**

| Command | Purpose |
|---------|---------|
| `pkill -f vscode-server` | Kill all VS Code server processes |
| `rm -rf ~/.vscode-server` | Remove VS Code server installation |
| `cat ~/.ssh/config` | View SSH connection aliases |
| `ssh <host-alias>` | Test direct SSH connection |

### Permission Denied Errors

```bash
# For Docker
sudo docker run ...

# For file access
ls -la <file>    # Check permissions
chmod +x <file>  # Make executable
```

### Docker Issues

```bash
# Check if Docker is running
sudo systemctl status docker

# Restart Docker
sudo systemctl restart docker

# Clean up space
docker system prune -a
```

### Web Server 521 Error (Cloudflare)

**Discovered:** January 26, 2026

**Symptoms:**
- Cloudflare shows "521 Web server is down" error
- Browser → Cloudflare: Working
- Cloudflare → Origin: Error
- Sites like `terminal.quietlyworking.org` or `twin.quietlyworking.org` unreachable

**Root Cause:**
Port 80/443 conflict between nginx and Caddy. If nginx starts before Caddy (e.g., after reboot), Caddy fails to bind to ports and the reverse proxy doesn't run.

**Diagnosis:**
```bash
# Check what's using port 80
sudo lsof -i :80

# Check Caddy status
systemctl status caddy

# Check nginx status
systemctl status nginx
```

**Solution:**
```bash
# Stop and disable nginx
sudo systemctl stop nginx
sudo systemctl disable nginx

# Restart Caddy
sudo systemctl restart caddy

# Verify
systemctl status caddy
curl -s -o /dev/null -w "%{http_code}" http://localhost:80
```

**Prevention:**
- nginx was disabled on 2026-01-26 to prevent this conflict
- If nginx is needed for something else, configure it to use different ports or remove Caddy

### Systemd Service Port Conflict (Address Already in Use)

**Discovered:** February 25, 2026

**Symptoms:**
- BetterStack fires "Missed heartbeat" alert for claude-dev VM
- `systemctl status <service>` shows `failed (Result: exit-code)`
- Journal shows `OSError: [Errno 98] Address already in use` repeated 11 times
- Health check reports `critical` (v1.0.0 withheld heartbeat; fixed in v1.1.0 — heartbeat now always pings)

**Root Cause:**
A rogue process started outside systemd (e.g., manual run, previous session) holds the port. When systemd tries to restart its managed service, the new process can't bind and fails. After 11 rapid restart attempts (~5s each), systemd gives up.

**Diagnosis:**
```bash
# Check which process holds the port
ss -tlnp | grep <port>

# Check if systemd thinks the service is running
systemctl status <service>

# Check journal for the crash loop
journalctl -u <service> --since "1 hour ago"
```

**Solution:**
```bash
# Kill the rogue process
kill <pid_from_ss_output>

# Reset systemd's failure state and restart
sudo systemctl reset-failed <service>
sudo systemctl restart <service>

# Verify
systemctl status <service>
```

**Prevention:**
- `digital_twin_server.py` now uses `ReusableHTTPServer` with `SO_REUSEADDR` (added Feb 2026), allowing restarts even if the port is in TIME_WAIT state
- Avoid running services manually when systemd manages them — use `systemctl restart` instead
- If you must test manually, stop the systemd service first: `sudo systemctl stop <service>`
- `<VM_USER>` has passwordless sudo for `systemctl` (added Mar 2026), allowing the agent to self-heal service failures
- `check_vm_health.py` v1.1.0 always pings heartbeat regardless of status, so this scenario no longer causes false "VM down" P1 alarms

### Disk Space Warnings

```bash
# Check disk usage
df -h

# Find large files
du -sh * | sort -h

# Clean Docker
docker system prune -a
```

### MCP Server Connection Issues

1. Check domain is in firewall allowlist
2. Rebuild container after adding domains
3. Test connectivity: `curl -I https://domain.com`

### n8n SSH Node Authentication Error

**Discovered:** January 17, 2026 during LinkedIn workflow debugging

**Symptoms:**
- Workflow executes on schedule but fails immediately
- Error: `"Node does not have any credentials set for \"sshPassword\""`
- SSH credentials (privateKey type) are correctly configured in n8n
- Same credentials work for other workflows

**Root Cause:**
The n8n SSH node defaults to password authentication. When using SSH private key credentials, you must explicitly set `authentication: "privateKey"` in the node's parameters. Without this, the node looks for password-type credentials and fails.

**Solution:**
In your workflow JSON, ensure each SSH node has the authentication parameter:
```json
{
  "parameters": {
    "authentication": "privateKey",  // ← REQUIRED for privateKey credentials
    "command": "your-command-here"
  },
  "type": "n8n-nodes-base.ssh",
  "credentials": {
    "sshPrivateKey": {
      "id": "credential-id",
      "name": "Credential Name"
    }
  }
}
```

**Via API Fix:**
```bash
# Extract workflow, add authentication to SSH nodes, update
cat workflow.json | jq '
  {name, connections, settings, nodes: [.nodes[] |
    if .type == "n8n-nodes-base.ssh"
    then .parameters.authentication = "privateKey"
    else . end
  ]}
' | curl -s -X PUT "$N8N_API_URL/workflows/{id}" \
  -H "X-N8N-API-KEY: $N8N_API_KEY" \
  -H "Content-Type: application/json" -d @-
```

**Prevention:**
Always include `"authentication": "privateKey"` when creating workflow JSON files that use SSH nodes with private key credentials.

**Fleet-Wide Remediation (Feb 13, 2026):**
A comprehensive audit found this issue (or variants) in 19 of 78 active workflows. Three patterns were discovered:
1. **Missing `authentication: privateKey`** — node defaults to password auth, looks for wrong credential type
2. **Wrong credential key (`sshPassword` instead of `sshPrivateKey`)** — works by accident because n8n looks up credentials by ID, not key name
3. **Redundant `sshAuthenticateWith: privateKey`** — non-standard parameter name, harmless but confusing

All 19 workflows were fixed via nuclear export→delete→reimport→publish (SQL UPDATE doesn't affect published versions in `workflow_history`). Additionally, 2 workflows using Discord httpRequest v4.1 (form-encoded `bodyParameters`) were upgraded to v4.2 (JSON body) — Cloudflare silently blocks form-encoded Discord webhook payloads for embed-heavy messages.

---

### n8n API Webhook Registration Issue (Self-Hosted)

**Discovered:** January 15, 2026 during n8n migration

**Symptoms:**
- Workflows created via n8n REST API activate successfully (logs show "Activated workflow")
- Webhook trigger nodes show as configured and enabled
- Calling the production webhook URL returns `{"code":404,"message":"The requested webhook \"xyz\" is not registered"}`
- Same workflow imported manually via UI works correctly

**What We Tried:**
1. Multiple workflow create/delete cycles via API
2. Different webhook paths and configurations
3. Restarting n8n container multiple times
4. Simplifying workflows to minimal webhook → respond patterns
5. Using different webhook node versions (v1, v2)
6. Verifying workflow activation via `/workflows/{id}/activate` endpoint

**Root Cause Analysis:**
The n8n REST API (currently in beta) appears to have a bug where webhooks created programmatically don't register in the internal webhook routing table, even though the workflow activates successfully. The issue may be related to:
- Webhook registration happening during UI import but not API import
- Missing internal event trigger when activating via API
- Race condition between workflow activation and webhook registration

**Status:** Unresolved limitation of n8n REST API (beta)

**Workaround Implemented:**
Rather than relying on n8n for webhook reception, we created a standalone webhook server:

```
Twilio → sms.quietlyworking.org → Caddy (SSL) → twilio_webhook_server.py → sms_approval.py
```

**Components:**
| Component | Purpose |
|-----------|---------|
| `twilio_webhook_server.py` | HTTP server on port 8765, receives Twilio webhooks |
| Caddy reverse proxy | SSL termination, proxies to webhook server |
| `sms-webhook.service` | systemd service for persistence |

**Should This Be Reported?**
Yes. This appears to be a legitimate bug in the n8n REST API. The behavior is:
- API reports success for workflow creation and activation
- Logs confirm activation
- But webhook routing doesn't work

Consider reporting to: https://github.com/n8n-io/n8n/issues with reproduction steps:
1. Create workflow with webhook trigger via REST API
2. Activate workflow via REST API
3. Attempt to call webhook URL
4. Observe 404 despite active workflow

**Learning:**
For critical webhooks that must work immediately, either:
1. Import workflows manually via n8n UI
2. Build standalone webhook endpoints (as we did for SMS)
3. Use n8n's native integrations where available (Twilio node) instead of custom webhooks

---

## Resources

### Key URLs

| Resource | URL |
|----------|-----|
| Azure Portal | https://portal.azure.com |
| VS Code Remote SSH Docs | https://code.visualstudio.com/docs/remote/ssh |
| Anthropic API Docs | https://docs.anthropic.com |
| n8n Dashboard | https://n8n.quietlyworking.org |
| Digital Twin Dashboard | https://twin.quietlyworking.org |
| Ez Terminal (Scheduler) | https://terminal.quietlyworking.org |
| Google Cloud Console | https://console.cloud.google.com |
| Vista Social | https://vistasocial.com |

### Environment Variables Reference

All secrets and configuration are stored in `.env` at the vault root. Here's the complete reference:

**Core Services:**
```bash
# Anthropic API
ANTHROPIC_API_KEY="sk-ant-..."

# OpenAI (for some AI enrichments)
OPENAI_API_KEY="sk-..."

# OpenRouter (LLM calls via model_config.py)
OPENROUTER_API_KEY="sk-or-v1-..."
OPENROUTER_MGMT_KEY="sk-or-v1-..."  # Management Key for Activity API cost cross-validation
```

**Azure (VM Control + Cost Tracking):**
```bash
AZURE_SUBSCRIPTION_ID="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
AZURE_TENANT_ID="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
AZURE_CLIENT_ID="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
AZURE_CLIENT_SECRET="your-client-secret"
```

**Google Services:**
```bash
# Calendar integration
GOOGLE_CALENDAR_CREDENTIALS="/path/to/service-account.json"
GOOGLE_CALENDAR_MAIN="email@domain.com"
GOOGLE_CALENDAR_ALERTS="calendar-id@group.calendar.google.com"
GOOGLE_CALENDAR_TIMESLOT="calendar-id@group.calendar.google.com"

# Sheets (for lead delivery)
GOOGLE_SHEETS_CREDENTIALS="/path/to/service-account.json"

# Google Docs (bidirectional sync with Obsidian)
GOOGLE_DOCS_CREDENTIALS="/path/to/service-account.json"
GOOGLE_DOCS_FOLDER_DEFAULT="drive-folder-id-for-synced-docs"
GOOGLE_DOCS_SYNC_DIRS="002 Projects,Quietly Working Universe Public Transparency Project"
```

**Discord Webhooks:**
```bash
DISCORD_WEBHOOK_AGENT_LOG="https://discord.com/api/webhooks/..."
DISCORD_WEBHOOK_INBOX_ALERTS="https://discord.com/api/webhooks/..."
DISCORD_WEBHOOK_L4G_LEADS="https://discord.com/api/webhooks/..."
DISCORD_WEBHOOK_SYSTEM_STATUS="https://discord.com/api/webhooks/..."
DISCORD_WEBHOOK_DAILY_DIGEST="https://discord.com/api/webhooks/..."
```

**Twilio Phone Registry:**

All QWU Twilio numbers are under the <ADMIN_EMAIL> account with Charity A2P messaging service.

| Number | Friendly Name | Purpose | Voice Config |
|--------|---------------|---------|--------------|
| **(949) 264-5730** | BNI-5730 | Aim High BNI - visitor reminders, member updates, referral alerts | Webhook |
| **(256) 827-7325** | U2SPEAK | Aim High BNI - speaker reminder automations | Webhook to n8n |
| **(949) 373-3730** | — | Locals 4 Good (L4G) - customer/prospect SMS | Studio Workflow |
| **(949) 344-2844** | — | VIP/Personal line → forwards to TIG's cell (949-371-5844) | Studio Transfer |
| **TBD** | EZER | Ezer AI Assistant - TIG command intake | Webhook to n8n |

```bash
# Twilio Account
TWILIO_ACCOUNT_SID="your-account-sid"
TWILIO_AUTH_TOKEN="your-auth-token"

# Phone Numbers by Purpose
TWILIO_BNI_NUMBER="+19492645730"      # Aim High BNI automations
TWILIO_U2SPEAK_NUMBER="+12568277325"  # BNI speaker reminders
TWILIO_L4G_NUMBER="+19493733730"      # Locals 4 Good SMS
TWILIO_VIP_NUMBER="+19493442844"      # VIP/Personal line
```

For detailed number documentation, see: `003 Entities/Tools/Twilio.md`

**Lead Generation/Enrichment:**
```bash
# Anymail Finder (email enrichment)
ANYMAIL_API_KEY="your-api-key"

# Reoon (cheaper bulk email validation)
REOON_API_KEY="your-api-key"

# LinkedIn (Sales Navigator scraping)
LINKEDIN_SCRAPER_API_KEY="your-api-key"

# Apollo.io
APOLLO_API_KEY="your-api-key"
```

**Locals 4 Good (L4G) System:**
```bash
# Supabase (primary backend — migrated from Google Sheets Feb 2026)
L4G_SUPABASE_URL="https://<SUPABASE_PROJECT_ID_L4G>.supabase.co"
L4G_SUPABASE_ANON_KEY="your-anon-key"
L4G_SUPABASE_SERVICE_ROLE_KEY="your-service-role-key"
L4G_SUPABASE_DB_PASSWORD="your-db-password"

# Stripe
L4G_STRIPE_WEBHOOK_SECRET="whsec_..."

# Legacy (deprecated — kept for reference, data migrated to Supabase)
L4G_AVAILABILITY_SHEET_ID="sheet-id"
L4G_CHECKOUT_API="https://script.google.com/macros/s/.../exec"
L4G_AREA_CONFIG_API="https://script.google.com/macros/s/.../exec"
L4G_POSTCARD_API="https://script.google.com/macros/s/.../exec"

# SMS (Twilio via n8n)
L4G_TWILIO_FROM_NUMBER="949-373-3730"
```

**Social Media:**
```bash
# Vista Social MCP
VISTA_SOCIAL_API_KEY="your-api-key"
```

**Canonical Datetime (Timezone Handling):**
```bash
# Timezone for all QWU operations (IANA format)
QWU_TIMEZONE="America/Los_Angeles"

# Day boundary hour (work before this counts as "yesterday")
QWU_DAY_BOUNDARY_HOUR=4
```

**Vault Configuration:**
```bash
VAULT_PATH="/home/<VM_USER>/qwu_backOffice"
```

### Tips & Gotchas

1. **SSH Key is critical** - Cannot be re-downloaded. Back it up immediately.

2. **VM IP can change** - If VM is stopped and started, IP might change. Check Azure Portal and update SSH config if connection fails.

3. **VM runs 24/7** - As of Jan 2026, auto-shutdown is disabled for continuous automation. Weekly restart Sunday 3 AM.

4. **Budget ~$60-85/month** - Always-on cost is higher but enables autonomous operations.

5. **Disk can only grow** - You can increase disk size later, but cannot shrink it. Start small.

6. **B2ms sweet spot** - 8GB RAM is comfortable for Docker + VS Code + agents. B2s (4GB) feels cramped.

7. **Standard SSD is fine** - No need for Premium SSD for development work.

8. **tmux is essential** - Any serious agent work needs persistent sessions.

---

## Notes for Future Sessions

*Add notes here as we continue building...*

- Consider setting up static IP (VM IP can change on restart)
- Create custom Docker images for frequently-used agent setups
- Set up Docker Compose for multi-container workflows
- Implement transcript extraction system
- ~~Build inbox processing automation~~ ✅ Completed (n8n workflow)
- ~~Complete Discord server setup~~ ✅ Completed (Session 9)
- Add Timeslot Planning calendar integration for goal-based scheduling
- Build appointment scheduling system with CRM integration (in planning)
- ~~Create Goals & Priorities document for summary alignment~~ ✅ Completed (M7 milestone)
- Set up n8n workflow for scheduled morning briefings
- Implement Vista Social content calendar integration

---

## BNI Member Dossier System

A comprehensive member enrichment and visitor connection system for BNI (Business Network International) chapter management. Designed for the Aim High chapter in Orange County, CA.

### Purpose

When visitors register for a BNI meeting, generate personalized **Connection Reports** for each chapter member containing:
- Icebreakers based on shared interests
- Commonalities between member and visitor
- Customized value propositions
- Email templates for follow-up

**Goal:** Create deeper connections faster, maximize referrals, increase membership, decrease attrition.

### Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│  DATA SOURCES                                                    │
├─────────────────────────────────────────────────────────────────┤
│  Airtable CSV    │  LinkedIn   │  Website     │  Google/Yelp    │
│  (base member    │  (profiles  │  (services,  │  (reviews,      │
│   data)          │  + posts)   │   about)     │   ratings)      │
└────────┬─────────┴──────┬──────┴───────┬──────┴────────┬────────┘
         │                │              │               │
         ▼                ▼              ▼               ▼
┌─────────────────────────────────────────────────────────────────┐
│  ENRICHMENT PIPELINE                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐           │
│  │ import_bni   │  │ enrich_      │  │ enrich_      │           │
│  │ _members.py  │→ │ linkedin.py  │→ │ website.py   │→ ...      │
│  └──────────────┘  └──────────────┘  └──────────────┘           │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │ enrich_member_orchestrator.py                               │ │
│  │ - Runs full pipeline: LinkedIn → Website → Reviews → AI    │ │
│  │ - Generates final synthesis with ICP, power teams, scripts  │ │
│  └────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
         │
         ▼
┌─────────────────────────────────────────────────────────────────┐
│  ENTITY FILES: 003 Entities/People/                              │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │ [Member Name].md                                          │    │
│  │ - YAML frontmatter (tags, contact, enrichment status)    │    │
│  │ - Professional Summary                                   │    │
│  │ - Services & Offerings                                   │    │
│  │ - Ideal Customer Profile (AI-synthesized)                │    │
│  │ - Power Team Connections                                 │    │
│  │ - Personal Interests & Background                        │    │
│  │ - Customer Sentiment (from reviews)                      │    │
│  └─────────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────────┘
         │
         ▼
┌─────────────────────────────────────────────────────────────────┐
│  CONNECTION REPORTS                                              │
│  Visitor × Member matching with icebreakers, value props, etc.  │
└─────────────────────────────────────────────────────────────────┘
```

### Project Files

| Location | Purpose |
|----------|---------|
| `002 Projects/_Aim High BNI Projects/_Aim High SOP/Aim High BNI - Standard Operating Procedures.md` | Comprehensive chapter SOP (all systems) |
| `002 Projects/_Aim High BNI Projects/Member Dossier System/_Overview.md` | Project documentation |
| `002 Projects/.../Templates/Template - BNI Member Dossier.md` | Member entity template |
| `002 Projects/.../Templates/Template - Visitor Connection Report.md` | Visitor×Member report template |
| `003 Entities/People/*.md` | Individual member entities (23 members) |

### Enrichment Scripts

| Script | Purpose |
|--------|---------|
| `import_bni_members.py` | Import Airtable CSV into entity files |
| `enrich_member_linkedin.py` | LinkedIn profile + posts scraping (Apify) |
| `enrich_member_website.py` | Website content extraction with AI |
| `enrich_member_reviews.py` | Google + Yelp reviews with referral intelligence |
| `enrich_member_orchestrator.py` | Full pipeline runner with AI synthesis |
| `gdrive_oauth.py` | Google Drive OAuth2 for historical data access |
| `generate_connection_report.py` | Generate visitor×member connection reports (v2.1.1 - parallel execution) |
| `bni_visitor_pipeline.py` | End-to-end visitor pipeline with auto-send + housekeeping (v3.1.0) |
| `validate_bni_email.py` | Quality validation for connection report emails (v1.0.0) |
| `sync_bni_roster.py` | Roster sync: scrapes BNI website, diffs entity tags (v1.0.0) |

### Roster Sync — Two Sources of Truth

The roster sync system enforces a critical data governance principle:

| Source | Authority |
|--------|-----------|
| **BNI chapter website** (socalbni.com) | WHO is an active member |
| **Entity files** (`003 Entities/People/`) | Member DATA (email, phone, enrichment, notes) |

The stale CSV export (`AimHighBNI-Members-Grid view exported on 20260109.csv`) must NEVER be used for roster lookups.

**Sync script:** `sync_bni_roster.py` scrapes the BNI website (direct HTTP, no Apify), compares against entity file tags, and applies changes:
- New members → creates entity file with `BNI-Active` tag, `enrichment_status: pending`
- Departed members → changes tag from `BNI-Active` to `BNI-Former`
- Changed fields → updates `company_name` or `bni_category` in frontmatter
- Safety: aborts if < 5 members returned (prevents wipe on broken scrape)

```bash
# Preview changes (always do this first)
python sync_bni_roster.py --dry-run --force

# Apply changes
python sync_bni_roster.py --force

# JSON output (for n8n automation)
python sync_bni_roster.py --dry-run --json
```

**QNT Supabase sync:** `qnt_roster_sync.py` runs daily via n8n, keeping the Quietly Networking app's member database in sync with the same BNI website source. Confirmed active and operational (17 members, 0 errors as of March 2026).

**Directive:** `005 Operations/Directives/sync_bni_roster.md`

### Usage

**Import members from Airtable (legacy — use sync_bni_roster.py for roster updates):**
```bash
python import_bni_members.py "Data Imports/aim_high_members_2024.csv"
```

**Enrich single member:**
```bash
python enrich_member_orchestrator.py "[Member Name]"
```

**Enrich all BNI members:**
```bash
python enrich_member_orchestrator.py --all
```

**Specific sources only:**
```bash
python enrich_member_orchestrator.py "[Member Name]" --sources linkedin,website
```

**Dry run (preview without changes):**
```bash
python enrich_member_orchestrator.py "[Member Name]" --dry-run
```

### Referral Intelligence

A unique feature of the review enrichment: **analyzes 1-3★ reviews to identify improvement areas and potential referral opportunities**.

For example, if a landscaper's reviews mention "wish they did hardscaping," the system suggests referring a hardscape specialist TO that member.

```python
# Output from enrich_member_reviews.py
{
    "referral_opportunities": [
        {
            "improvement_area": "Response time",
            "potential_referral": "Virtual assistant or scheduling service",
            "reasoning": "Multiple reviews mention delayed responses"
        }
    ]
}
```

### Entity Schema

Member entities include these YAML frontmatter fields:

```yaml
# === IDENTITY ===
tags: [AimHigh, BNI-Active]
aliases: [Derek]
type: human

# === CONTACT INFO ===
email: member@company.com
phone_mobile: "(555) 123-4567"
121_link: https://calendly.com/member  # BNI 1-2-1 scheduling

# === BUSINESS INFO ===
company_name: "Company Name LLC"
company_website: https://company.com
bni_category: "Business Category"

# === ENRICHMENT STATUS ===
enrichment_status: pending|partial|complete
last_enriched: 2026-01-11
enrichment_sources: [airtable, linkedin, website, reviews]

# === REVIEW DATA ===
google_rating: 4.8
google_review_count: 47
yelp_rating: 4.5
yelp_review_count: 23
```

### Google Drive Integration

OAuth2 authentication provides full read access to Google Drive for accessing historical BNI data (visitor logs, meeting notes, etc.):

```bash
# Initial setup (one-time)
python gdrive_oauth.py --authorize

# Search for files
python gdrive_oauth.py --search "BNI dossier"

# List folder contents
python gdrive_oauth.py --list-folder "folder-id"
```

**OAuth Credentials:** `.credentials/google-oauth-desktop.json`
**Token Storage:** `.credentials/google-oauth-token.json`

### Environment Variables

```bash
# Apify (for web scraping)
APIFY_API_TOKEN="your-apify-token"

# Anthropic (for AI synthesis)
ANTHROPIC_API_KEY="your-api-key"

# Google OAuth (for Drive access)
GOOGLE_OAUTH_CREDENTIALS_PATH=".credentials/google-oauth-desktop.json"
GOOGLE_OAUTH_TOKEN_PATH=".credentials/google-oauth-token.json"
```

### Terminology

| Term | Meaning |
|------|---------|
| 121 (One-to-One) | Private meeting between two BNI members |
| 121_link | Scheduling URL for booking 1-2-1 meetings |
| Power Team | Complementary business categories that refer well |
| ICP | Ideal Customer Profile |
| Referral Intelligence | Insights from reviews about referral opportunities |

### Advanced Features (Phases 5-7) ⭐ NEW

The Epic Dossier System extends basic enrichment with three advanced intelligence layers:

#### Phase 5: Cross-Platform (Instagram Integration)

Extracts Instagram handles from cached website data and enriches member profiles:

```bash
# Extract Instagram from already-scraped websites (no API calls)
python extract_instagram_from_websites.py

# Full enrichment including Instagram (if handle exists in frontmatter)
python enrich_member_orchestrator.py "Member Name"
```

**Scripts:**
| Script | Purpose |
|--------|---------|
| `extract_instagram_from_websites.py` | Mines Instagram handles from JSON-LD `sameAs` arrays in cached website data |
| `enrich_member_instagram.py` | Apify-based Instagram profile and posts scraping |

**How it works:** When websites include structured data (JSON-LD), they often list social profiles in `sameAs` arrays. This script mines that data without additional API calls.

#### Phase 6: Network Intelligence

Generates "who should meet whom" recommendations using 8 matching algorithms:

```bash
# Generate chapter-wide connection recommendations
python network_intelligence.py --chapter AimHigh --write
```

**Matching Algorithms:**
1. **Power Team Matching** - Complementary BNI categories (e.g., roofer ↔ real estate)
2. **Referral Reciprocity** - Bidirectional referral potential
3. **Style Compatibility** - Communication style matching (connector ↔ thought_leader)
4. **Industry Overlap** - Shared industry experience
5. **Values Overlap** - Mission alignment and shared values
6. **Mission Alignment** - Charitable/community focus matching
7. **Entrepreneur Affinity** - Fellow business owner connection
8. **Volunteer Affinity** - Shared community involvement

**Output:** Writes "Recommended Connections" section to each member's entity file with Obsidian wiki links:
```markdown
## Recommended Connections

Based on network intelligence analysis:

1. **[[[Member Name]]]** (Score: 60)
   - Reasons: Power team match, Values overlap, Mission alignment
```

#### Phase 7: Predictive Intelligence

Forward-looking insights using FLAGSHIP LLM analysis:

```bash
# Generate predictive insights for members with sufficient data
python predictive_intelligence.py --write
```

**Analysis Types:**
| Insight | Description |
|---------|-------------|
| Trajectory Direction | expanding / deepening / pivoting / legacy_building / maintaining |
| Career Stage | early / mid / established / senior / legacy |
| Growth Areas | 3-5 areas the member appears to be developing |
| Hopes We See | Aspirational reading of their public persona |

**Output:** Writes "Predictive Insights" section to entity files:
```markdown
## Predictive Insights

**Trajectory:** Expanding (established stage)
**Growth Areas:** Digital marketing, strategic partnerships, community leadership
**Hopes We See:** Scaling impact while maintaining service quality
```

#### Updated Enrichment Pipeline (v1.4.0)

The orchestrator now runs 7 steps:
1. LinkedIn profile and posts
2. Website content extraction
3. Google/Yelp reviews
4. AI synthesis
5. Meeting intelligence (from transcripts)
6. Instagram (if handle in frontmatter)
7. Network intelligence (chapter-wide)

```bash
# Full pipeline including all phases
python enrich_member_orchestrator.py --all
```

### Visitor Enrichment (Symmetric Intelligence) ⭐ NEW

Enriches BNI visitors with the same depth of intelligence as chapter members, enabling symmetric connection matching.

**Problem Solved:** Members have rich Epic Dossier profiles, but visitors only had basic registration data. This created asymmetric matching where AI couldn't generate quality icebreakers from limited visitor information.

**Solution:** `enrich_visitor.py` runs the same enrichment pipeline on visitors:

```bash
# Enrich a specific visitor
python enrich_visitor.py "Michael Dory"

# Enrich all pending visitors
python enrich_visitor.py --pending

# Dry run (no API calls)
python enrich_visitor.py "Michael Dory" --dry-run
```

**Pipeline (4 Steps):**
1. **LinkedIn Lookup** - Find person by name + company using Apify person search
2. **Website Extraction** - Scrape visitor's company website for services, about, team info
3. **Reviews Lookup** - Google Places reviews with sentiment analysis
4. **AI Synthesis** - Generate profile with same fields as member dossiers

**Output Fields:**
| Field | Description |
|-------|-------------|
| `professional_summary` | Role, company, expertise |
| `services_offered` | What their business provides |
| `ideal_customer_profile` | Who they serve |
| `communication_style` | How they likely prefer to engage |
| `personality_traits` | Observable traits from public presence |
| `values_indicators` | What they appear to care about |
| `life_hints` | Personal interests, background clues |
| `power_teams` | BNI categories that could refer to them |
| `connection_hooks` | Specific icebreaker topics |

**Storage:** `.tmp/bni_visitors/{meeting_date}_{visitor_name_slug}.json`

**Integration with Connection Reports:**

`generate_connection_report.py` v2.1.0 automatically loads enriched visitor data when generating reports (with parallel execution for 5x speedup):

```python
# Connection report now receives enriched visitor data
enriched_visitor = find_enriched_visitor(visitor_name)
report = generate_connection_report_ai(visitor_data, member_data, enriched_visitor)
```

This enables:
- Deeper icebreakers based on visitor's values and personality
- Values alignment section comparing member and visitor missions
- Power team matching from visitor's ideal customer profile
- Bidirectional referral opportunities

**Environment Variables:**
```bash
APIFY_API_TOKEN="your-apify-token"  # LinkedIn person search
OPENROUTER_API_KEY="your-key"       # AI synthesis (FLAGSHIP tier)
```

#### MP Student Training Opportunity (Tier 2: Contributor)

Students can learn data enrichment pipeline patterns by:
1. Running visitor enrichment on test data (dry-run mode)
2. Understanding the 4-step pipeline architecture
3. Analyzing how AI synthesis creates structured profiles from unstructured data
4. Comparing member vs visitor enrichment approaches

**Learning Objectives:**
- API integration with Apify (web scraping as a service)
- LLM prompt engineering for data synthesis
- JSON data transformation and storage patterns
- Pipeline design with graceful degradation (partial enrichment when sources fail)

### Full Visitor Pipeline (v3.2.0) ⭐ NEW

The `bni_visitor_pipeline.py` orchestrates the complete visitor processing workflow from enrichment through email delivery and inbox organization.

**6 Pipeline Stages:**

| Stage | Name | What It Does |
|-------|------|--------------|
| 1 | EPIC Enrichment | 7-step visitor enrichment (LinkedIn, posts, website, reviews, AI synthesis) |
| 2 | Connection Reports | Generates 16 personalized reports for all active members (5 parallel workers) |
| 3 | Email Sending | Sends connection report emails directly via MS Graph `/sendMail` (no drafts) |
| 4 | SMS Notification | Notifies TIG via Twilio when emails have been sent |
| 5 | Discord Notification | Posts completion summary to #bni-prep |
| 6 | Email Housekeeping | Marks original registration email complete + moves to BNI/Visitors folder |

**Usage:**
```bash
# Process specific visitor
python bni_visitor_pipeline.py "[Member Name]"

# Process latest pending visitor
python bni_visitor_pipeline.py --latest

# Dry run (no API calls, no emails)
python bni_visitor_pipeline.py "[Member Name]" --dry-run

# Test mode: redirect ALL emails to yourself (safe testing)
python bni_visitor_pipeline.py "[Member Name]" --test-recipient=<ADMIN_EMAIL>
```

**v3.4.0 Change (YAML Deprecated — Phase 7 Complete):**
Defense-in-depth opt-out system using the self-service Preference Center:
- **Layer 1 (Sole Source):** SQLite database via `preference_center/db.py` v2.1.0 (`PreferenceDB`)
- **Layer 2:** Entity file flag (`visitor_reports_opt_out: true`)
- **Layer 3:** `should_send_report()` function checks all layers
- **Layer 4:** Full audit logging to `.tmp/logs/YYYY-MM-DD.log`
- **Fail-safe:** If SQLite is unavailable, email is **blocked** (not sent). Better to miss one email than to send to someone who opted out.
- **Obsidian Dashboard:** `005 Operations/Dashboards/Preference-Center-Status.md` auto-regenerates on every preference write + daily cron safety net

**Self-Service Preference Management:**
Users can manage their own preferences via:
1. **Ezer Chat:** Say "manage my preferences" or "unsubscribe" at terminal.quietlyworking.org
2. **Email Footer:** All automated emails include a preferences link
3. **Direct URL:** https://preferences.quietlyworking.org (requires magic link)

**Available Products:**
| Code | Display Name | Description |
|------|--------------|-------------|
| `visitor_reports` | Visitor Connection Reports | Briefings when visitors come to BNI |
| `meeting_recaps` | Meeting Recap Emails | Summary after each BNI meeting |
| `network_recs` | Connection Recommendations | AI-suggested connections |
| `verification_emails` | LinkedIn Verification Requests | Profile verification requests |
| `meeting_followups` | Meeting Follow-ups | Summary and action items after meetings with Chaplain TIG |
| `relationship_touchpoints` | Relationship Touchpoints | Periodic check-in messages to stay connected |
| `all_communications` | All Communications | Turn off everything |

**Key Files:**
- `preference_center/db.py` - SQLite database operations + auto-dashboard (v2.1.0)
- `preference_center/magic_link.py` - Token generation/verification (v1.0.0)
- `preference_center/email.py` - Magic link + confirmation emails (v1.1.0)
- `preference_center/api.py` - API endpoint handlers (v1.1.0)
- `generate_preferences_dashboard.py` - Cron safety net for Obsidian dashboard (v1.0.0)
- `ez_chat_handler.py` - "preferences" intent handling (v3.8.0)
- Dashboard: `005 Operations/Dashboards/Preference-Center-Status.md`
- Directive: `005 Operations/Directives/preference_center.md`

> **Missing Pixel Training Opportunity (Tier 2: Contributor)**
>
> | Component | Skills Taught |
> |-----------|---------------|
> | SQLite database (db.py) | Python, database design, CRUD operations, indexing |
> | Magic link auth (magic_link.py) | HMAC-SHA256 cryptography, token-based auth, security |
> | Email system (email.py) | MS Graph API, HTML templates, OAuth2 |
> | API handlers (api.py) | REST design, rate limiting, error handling |
> | Intent detection | NLP keyword matching, modal flows |
>
> **Portfolio Value:** Full-stack system demonstrating database, security, API, and UX skills.

### Email Sending Conventions (System-Wide)

**Added: Session 65 (February 8, 2026)**

Every email script is classified as **Enhancement** or **Exempt**:

| Classification | Footer | Opt-out Check | Examples |
|---------------|--------|---------------|----------|
| **Enhancement** | Preference link required | Required before send | Follow-ups, touchpoints, BNI reports, recaps |
| **Exempt** | No preference link | No check needed | Transactional, conversational, recently-requested |

**Enhancement Scripts (footer + opt-out):**
| Script | Category Code | Fail Mode |
|--------|--------------|-----------|
| `send_meeting_followup.py` v1.3.0 | `meeting_followups` | Fail-open |
| `send_meeting_prep_email.py` | `meeting_followups` | Fail-open |
| `generate_bni_followup_emails.py` | `meeting_recaps` | Fail-closed |
| `send_journey_message.py` | `relationship_touchpoints` | Fail-closed |
| `bni_visitor_pipeline.py` v3.4.0 | `visitor_reports` | Fail-closed |

**Exempt Scripts (no footer):**
| Script | Reason |
|--------|--------|
| `send_verification_email.py` | Transactional (LinkedIn verification) |
| `send_optout_confirmation.py` | Transactional (preference confirmation) |
| `ezer_respond.py` | Conversational reply (human-initiated) |
| `video_email_sender.py` | TIG-requested action |
| `qwr_notify_article_ready.py` v2.1.0 | Transactional (supporter requested) |

**Fail-open vs Fail-closed:** Fail-open scripts send the email even if the preference check fails (suitable for operational emails like meeting follow-ups). Fail-closed scripts block the email if the preference check fails (required for ongoing automated communications like BNI reports and journey touchpoints).

**BCC Monitoring:** All 10 email scripts BCC `EZER_BCC_EMAIL` (<ADMIN_EMAIL>) on every outbound. Guard: BCC skipped if recipient == BCC address.

**Name Rule:** Her name is **Ezer Aión** (Hebrew "helper who runs toward" + Greek "eternal age"). Always use the accent on the 'o'. Never write "Aion" without it.

> **Missing Pixel Training Opportunity (Tier 2: Contributor)**
>
> The Email Preference System teaches real-world compliance patterns:
> - **Opt-out Architecture** — Defense-in-depth (database + entity file + self-service), fail-open vs fail-closed behavior
> - **Magic Link Auth** — HMAC-SHA256 token generation, expiry management, rate limiting
> - **Classification System** — Why transactional emails don't need unsubscribe links (CAN-SPAM)
> - **Database Migration** — Auto-adding columns via ALTER TABLE, handling defaults for existing rows
>
> **Exercise:** Add a new product category to the preference center (add to db.py PRODUCTS, api.py PRODUCTS dict, email.py PRODUCT_NAMES), create a test email script that checks opt-out and appends the footer, verify with dry-run.

**v3.1.0 Change (Email Housekeeping):**
After sending member emails, the pipeline automatically:
1. Searches for the original registration email by visitor name
2. Marks it with green checkmark (flag status: `complete`)
3. Moves it to `Inbox/BNI/Visitors` folder for organization

**v3.0.0 Change (Auto-Send):**
Previously created Outlook drafts requiring manual review. Now sends emails directly after quality gate validation. User validated quality over multiple production runs before enabling.

**Quality Gate:** `validate_bni_email.py` ensures each email has:
- 10 required sections (Profile, Icebreakers, Social Proof, etc.)
- Minimum 10,000 characters
- Minimum 300 unique words
- Emails failing validation are NOT sent

---

## BNI Meeting Recap System ⭐ NEW

Automated weekly meeting recap generation for BNI chapters. Processes Zoom chat logs to extract visitors, referrals, announcements, and engagement data, then generates personalized HTML emails for each chapter member. As of February 2026, supports **slide-augmented recaps** that combine chat analysis with Claude Vision screenshot analysis from Google Drive meeting folders.

### Purpose

After each BNI meeting, generate a comprehensive recap email that:
- Highlights visitors with full contact details and interest levels
- Showcases referrals given with context (not just names)
- Features the week's speakers with their Ideal Customer Profiles
- Lists 1-2-1 connection requests with contact links
- Includes chapter announcements with actionable URLs
- Celebrates chat engagement champions
- Personalizes content for each recipient

**Goal:** Keep members engaged, reinforce connections made during the meeting, and make follow-up easy.

### Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│  DATA SOURCES                                                        │
├─────────────────────────────────────────────────────────────────────┤
│  Zoom Chat    │  Speaker       │  [Member Name]'s       │  Entity Files    │
│  Export       │  Schedule      │  Visitor Sheet  │  (003 Entities/) │
│  (.txt)       │  (Google       │  (attendance,   │  (member data,   │
│               │   Sheets)      │   interest)     │   ICP, contact)  │
└──────┬────────┴───────┬────────┴────────┬────────┴─────────┬────────┘
       │                │                 │                  │
       ▼                ▼                 ▼                  ▼
┌─────────────────────────────────────────────────────────────────────┐
│  PROCESSING PIPELINE                                                 │
│  ┌──────────────────┐  ┌────────────────┐  ┌──────────────────────┐ │
│  │ process_bni_chat │  │ read_speaker_  │  │ read_cathie_visitor_ │ │
│  │ .py              │→ │ schedule.py    │→ │ sheet.py             │ │
│  │ - Parse messages │  │ - Get speakers │  │ - Attendance data    │ │
│  │ - Extract data   │  │   for date     │  │ - Interest levels    │ │
│  └──────────────────┘  └────────────────┘  └──────────────────────┘ │
│                                                                      │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │ generate_bni_meeting_recap.py (v4.3.0)                         │ │
│  │ - Combines all data sources                                     │ │
│  │ - EPIC visitor spotlights with enriched entity data            │ │
│  │ - Builds personalized HTML for each recipient                  │ │
│  │ - Speaker spotlight with ICP and referral triggers             │ │
│  │ - Week-over-week trend tracking                                │ │
│  │ - Discord approval flow + MS Graph email delivery              │ │
│  └────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────┘
       │
       ▼
┌─────────────────────────────────────────────────────────────────────┐
│  OUTPUT                                                              │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────────┐  │
│  │ Discord Preview │  │ HTML Email      │  │ Markdown Archive    │  │
│  │ (approval flow) │  │ (MS Graph API)  │  │ (.tmp/bni_recap/)   │  │
│  └─────────────────┘  └─────────────────┘  └─────────────────────┘  │
└─────────────────────────────────────────────────────────────────────┘
```

### Scripts

| Script | Purpose |
|--------|---------|
| `process_bni_chat.py` | Parse Zoom chat export, extract participants, referrals, 1-2-1 requests, announcements |
| `generate_bni_meeting_recap.py` | Generate personalized HTML recap emails |
| `read_speaker_schedule.py` | Read speaker assignments from Google Sheets |
| `read_cathie_visitor_sheet.py` | Read visitor attendance/interest from [Member Name]'s tracking sheet |
| `extract_slide_intel.py` | Analyze meeting screenshots via Claude Vision (multimodal). Downloads from Google Drive shared folder, analyzes each image, synthesizes presentations + attendees + notable moments into unified JSON intelligence. |

### Usage

**Step 1: Process the Zoom chat export**
```bash
python process_bni_chat.py --file "path/to/zoom_chat.txt" --json --output processed.json
```

**Step 2: Generate recap (preview mode)**
```bash
python generate_bni_meeting_recap.py processed.json --preview
```

**Step 3: Post to Discord for approval**
```bash
python generate_bni_meeting_recap.py processed.json --discord
```

**Step 4: Send test email to yourself**
```bash
python generate_bni_meeting_recap.py processed.json --test-email <ADMIN_EMAIL>
```

**Step 5: Send to all participants**
```bash
python generate_bni_meeting_recap.py processed.json --send
```

### Email Personalization

Each recipient receives a customized email with:

| Section | Description |
|---------|-------------|
| **Personalized Header** | Shows their referrals given/received, 1-2-1 requests, chat champion status |
| **Visitor Spotlight** | EPIC enriched cards with company, BNI category, summary, power teams, contact info |
| **Speaker Spotlight** | This week's speakers with Ideal Customer Profile and referral triggers |
| **Referrals Given** | Stories about referrals passed during the meeting |
| **1-2-1 Connections** | Who wants to meet with whom, with contact links (calendly/email/phone) |
| **Don't Forget** | Chapter announcements with dates and action links |
| **Chat Champions** | Top engaged members in the Zoom chat |
| **Trends** | Week-over-week attendance, referrals, engagement |

### Slide-Augmented Recap (v2 — February 2026)

When meeting screenshots are uploaded to a Google Drive folder, the recap can be augmented with visual intelligence:

**Step 0: Extract slide intelligence from Google Drive**
```bash
python extract_slide_intel.py --date 2026-02-26 --folder-id <drive_folder_id>
```

This uses Claude Vision (FLAGSHIP tier) to analyze each screenshot, then synthesizes:
- Presentation titles, speakers, and key content from each slide
- Attendees spotted in gallery-view screenshots
- Notable moments (reactions, celebrations, achievements)

Output: `.tmp/slide_intel/YYYY-MM-DD_slide_intel.json`

The slide intel JSON is then combined with chat analysis to produce a richer recap with keynote spotlights, visual context, and attendee cross-referencing.

**Data integrity safeguard:** Before sending to any recipients, the send script must:
1. Build recipient list from `BNI-Active` entity tags
2. Call `check_send_permission(email, "meeting_recaps", fail_open=False)` for each recipient
3. Generate per-recipient preference center footer with magic link
4. Send individually (no BCC) for unique unsubscribe links

**Official roster verification:** The authoritative member list is at `socalbni.com` (AJAX POST to `/bnicms/v3/frontend/chapterdetail/display` with `website_type=2`, `website_id=5197`). Cross-reference entity files against this periodically to catch stale `BNI-Active` tags.

### Speaker Spotlight Feature

The speaker spotlight (v4.2.0+) features **all speakers** from the meeting:
- Speaker 1 and Speaker 2 are treated equally (just presentation order)
- Pulls from the speaker schedule Google Sheet for the meeting date
- Falls back to one random member if no speakers scheduled
- Shows member's company, Ideal Customer Profile, and "When to Refer" triggers
- Uses fuzzy name matching to find entity files (e.g., "Kim Nguyen" → "Kim Nguyen.md")

**Spotlight Content (from Entity Files):**
```markdown
## Ideal Customer Profile
- **Industries**: Local Service Businesses, Retail/Boutique Owners...
- **Company Size**: Small-to-medium businesses, $100K-$5M revenue...
- **When to Refer**: Business owner asking about direct mail marketing...
```

### EPIC Visitor Spotlight (v4.3.0+)

Visitor cards now pull enriched data from entity files for **symmetric intelligence** - visitors get the same rich treatment as members:

| Field | Source | Example |
|-------|--------|---------|
| **Company** | Entity `company_name` or [Member Name]'s sheet | Bonehead Bookkeeping |
| **BNI Category** | Entity `bni_category` | Bookkeeping |
| **Summary** | Entity `## Professional Summary` | "Bonehead in Chief at Bonehead Bookkeeping..." |
| **Power Teams** | Entity `## Power Team Connections` | CPA, Business Broker, Financial Advisor |
| **LinkedIn** | Entity `linkedin_url` | Clickable link |
| **Calendly** | Entity `121_link` | "Schedule 1:1" button |

**Entity Lookup:** The `lookup_visitor_entity()` function searches:
1. Exact match: `003 Entities/People/{Name}.md`
2. Draft files: `000 Inbox/___Review/{Name} [DRAFT].md`
3. Fuzzy match: Files containing all significant name parts

**Result:** Instead of "Benjamin Kubo - **TBD**", recaps now show:
> **Benjamin Kubo** - Bonehead Bookkeeping | *Bookkeeping*
> *"Bonehead in Chief at Bonehead Bookkeeping..."*
> **Power Team:** CPA / Tax Preparer, Business Broker, Financial Advisor

### Data Extraction

The chat parser (`process_bni_chat.py` v2.3.0) extracts:

| Data Type | Detection Method |
|-----------|------------------|
| **Participants** | Matches against vault entity files + display name parsing |
| **Visitors** | Prefixes like "VIP -", "BNI -", or announced by chapter admin |
| **Referrals** | Keywords: "referral", "passing", "thank you for referring" |
| **1-2-1 Requests** | Patterns like "@Name let's 121", "would love to 1:1 with Name" |
| **Announcements** | Keywords + REQUIRES URL (dates alone not sufficient) |
| **Contact Info** | Email, phone, calendly links from message content |

**Filtering Rules:**
- 1-2-1 requests require a specific person target (not "visitors" or "everyone")
- Self-promotional calendly shares are excluded from 1-2-1 requests
- Announcements without actionable URLs are filtered out
- Thank-you/gratitude messages excluded from announcements
- Duplicate announcements from same sender are deduplicated

### Visitor Interest Levels

When [Member Name]'s visitor tracking sheet is available, visitors display interest badges:

| Stars | Meaning |
|-------|---------|
| ⭐⭐⭐ | High interest - likely to join |
| ⭐⭐ | Moderate interest |
| ⭐ | Low interest |
| (no stars) | No interest data available |

### Output Files

| File | Location |
|------|----------|
| Processed chat data | `.tmp/bni_chat/processed_YYYY-MM-DD.json` |
| HTML email template | `.tmp/bni_recap/YYYY-MM-DD_recap.html` |
| Markdown archive | `.tmp/bni_recap/YYYY-MM-DD_recap.md` |
| Trend history | `.tmp/bni_recap/trend_history.json` |

### Environment Variables

```bash
# MS Graph API (for sending emails)
AZURE_CLIENT_ID="your-client-id"
AZURE_CLIENT_SECRET="your-client-secret"
AZURE_TENANT_ID="your-tenant-id"
OUTLOOK_EMAIL="sender@domain.com"

# Discord (for approval flow)
DISCORD_WEBHOOK_BNI_RECAP="webhook-url"

# Google Sheets (for speaker schedule + visitor tracking)
GOOGLE_SERVICE_ACCOUNT_KEY_PATH=".credentials/google-service-account.json"
SPEAKER_SCHEDULE_SPREADSHEET_ID="spreadsheet-id"
CATHIE_VISITOR_SPREADSHEET_ID="spreadsheet-id"
```

### Directives

| Directive | Purpose |
|-----------|---------|
| `process_bni_chat.md` | SOP for parsing chat exports |
| `generate_bni_followup_emails.md` | SOP for the full recap pipeline |

### MP Training Opportunities

| Task | Skills Developed |
|------|------------------|
| Writing member Ideal Customer Profiles | Marketing, ICP development, copywriting |
| Creating referral trigger lists | Business development, market research |
| Processing visitor data from sheets | Data entry, spreadsheet skills |
| Testing email templates | QA, attention to detail |

---

## System Architecture Audit ⭐ NEW

A monthly deep-analysis process to evaluate system health, identify gaps, and ensure all components work together effectively.

### Purpose

As the QWU Backoffice grows in complexity (38 directives, 73 scripts, 8 agents, 11 skills), it becomes critical to regularly step back and assess:
- Which components are fully integrated
- What systems are dangling or incomplete
- Where gaps exist that need attention
- How well the layers work together

This audit serves both operational health and educational purposes—providing students with a comprehensive view of how a production automation system is structured.

### Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         QWU BACKOFFICE SYSTEM                               │
│                      ~45,000 lines | 3-Layer Architecture                   │
└─────────────────────────────────────────────────────────────────────────────┘
                                    │
        ┌───────────────────────────┼───────────────────────────┐
        ▼                           ▼                           ▼
┌───────────────────┐     ┌───────────────────┐     ┌───────────────────┐
│  LAYER 1          │     │  LAYER 2          │     │  LAYER 3          │
│  DIRECTIVES       │     │  ORCHESTRATION    │     │  EXECUTION        │
│  (What to do)     │     │  (Decision-making)│     │  (Doing the work) │
│                   │     │                   │     │                   │
│  38 SOPs          │     │  Claude Agents    │     │  73 Python        │
│  ~10K lines       │     │  8 specialized    │     │  scripts          │
│  005 Operations/  │     │  .claude/agents/  │     │  ~36K lines       │
│  Directives/      │     │                   │     │  005 Operations/  │
│                   │     │                   │     │  Execution/       │
└───────────────────┘     └───────────────────┘     └───────────────────┘
```

### System Component Map

#### Capture & Ingest (Fully Integrated ✅)

```
    📱 Phone Captures          📧 Outlook Emails           🎥 Zoom Meetings
         │                          │                           │
         ▼                          ▼                           ▼
   process_inbox.py          outlook_pipeline.py         zoom_pipeline.py
         │                          │                           │
         │                          └───────────┬───────────────┘
         │                                      │
         │                                      ▼
         │                           ┌─────────────────────┐
         │                           │  ENTITY RESOLUTION  │
         │                           │  + SuiteDash CRM    │
         │                           └─────────────────────┘
         │                                      │
         └──────────────────┬───────────────────┘
                            ▼
   ┌─────────────────────────────────────────────────────────┐
   │               VAULT UPDATES                              │
   │  003 Entities/People/   (150+ profiles)                 │
   │  003 Entities/Organizations/   (50+ orgs)               │
   │  001 Daily/   (daily notes)                             │
   │  ___Tasks/   (action items)                             │
   └─────────────────────────────────────────────────────────┘
```

#### Intelligence Layer (Fully Integrated ✅)

```
   8 Thought Leaders                    Wisdom Pipeline
   ┌─────────────────┐                 ┌─────────────────┐
   │ Simon Sinek     │                 │ youtube_        │
   │ Brené Brown     │───(4-12 hrs)───▶│ monitor.py     │
   │ Lex Fridman     │                 │       │         │
   │ Andrej Karpathy │                 │       ▼         │
   │ Dwarkesh Patel  │                 │ wisdom_         │
   │ [+3 others]     │                 │ indexer.py      │──▶ SQLite
   └─────────────────┘                 │       │         │
                                       │       ▼         │
                                       │ wisdom_         │──▶ Attributed
                                       │ synthesizer.py  │    Content
                                       └─────────────────┘
```

#### Daily Operations (Fully Integrated ✅)

```
  06:00 ─────▶ morning_briefing.py ─────▶ Discord #daily-digest
                      │                         │
                      └────────────────────────▶│
                                                ▼
                                         ┌─────────────┐
                                         │ Daily Note  │
                                         └─────────────┘
                                                ▲
  18:00 ─────▶ summarize_session.py ────────────┘
```

#### Lead Generation (Partially Integrated 📋)

```
   Lead Sources (40% Built)              Enrichment (85% Built)
   ┌─────────────────────┐              ┌─────────────────────┐
   │ LinkedIn            │              │ enrich_leads.md     │
   │ Google Maps         │              │ (orchestrator)      │
   │ Apollo        ─?──▶ │  ── ? ──▶   │         │           │
   │ Yellow Pages        │              │ ┌─────────────────┐ │
   │ Yelp                │              │ │friendly_name    │ │
   │ Crunchbase          │              │ │reviews          │ │
   └─────────────────────┘              │ │email            │ │
          ⚠️ Router exists               │ └─────────────────┘ │
          sources need testing          └─────────────────────┘
```

#### QWF Creative (Router Built, Execution Light 📋)

```
                    ┌─────────────────────┐
    Request ─────▶  │ qwf-master-router   │  ✅ Complete
                    └────────┬────────────┘
                             │
        ┌────────────────────┼────────────────────┐
        ▼                    ▼                    ▼
  ┌───────────┐       ┌───────────┐       ┌───────────┐
  │qwf-writer │       │qwf-       │       │qwf-social │
  │📋 Light   │       │creative-  │       │-media-    │
  │execution  │       │director   │       │manager    │
  └───────────┘       │📋 Light   │       │📋 Light   │
                      └───────────┘       └───────────┘
```

### Component Health Scorecard

| Component | Status | Completeness | Notes |
|-----------|--------|--------------|-------|
| Email Processing | ✅ Active | 100% | SuiteDash CRM integrated |
| Meeting Intelligence | ✅ Active | 100% | SuiteDash CRM integrated |
| Morning Briefing | ✅ Active | 100% | Project tasks included |
| Daily Synthesis | ✅ Active | 100% | Goals context included |
| Expert Monitoring | ✅ Active | 100% | YouTube, 8 experts |
| BNI Member Enrichment | ✅ Active | 100% | Full pipeline |
| Inbox Processing | ✅ Active | 95% | Dual-input working |
| Wisdom Synthesis | ✅ Active | 90% | Architecture complete |
| Lead Enrichment | ✅ Active | 85% | Core enrichments work |
| Document Sync | 📋 Defined | 60% | Scripts exist |
| Calendar/Scheduling | 📋 Defined | 50% | Not in briefing |
| Lead Generation | 📋 Partial | 40% | Router only |
| QWF Creative | 📋 Router | 30% | Needs execution |

### Known Gaps (January 2026)

| Gap | Severity | Impact | Recommendation |
|-----|----------|--------|----------------|
| Lead gen sources not wired | Medium | Can't generate leads at scale | Test Apify actors, document |
| QWF creative execution light | Medium | Content not automated | Build templates per type |
| Calendar not in briefing | Low | Missing today's meetings | Wire calendar_events.py |
| Prompts directory empty | Low | No prompt versioning | Extract from scripts |
| Scheduling rules undefined | Low | Manual booking only | Document rules |

### Running the Audit

**Trigger:** Monthly (1st of month) or on-demand

**Command:**
```
/audit-system
```
Or ask Claude: "Run a comprehensive system architecture audit with ultrathink"

**Process:**
1. Claude explores all directives, scripts, agents, skills
2. Maps dependencies and integrations
3. Identifies gaps and incomplete work
4. Generates health scorecard
5. Produces recommendations

**Directive:** `005 Operations/Directives/audit_system_architecture.md`

### Audit Output Template

Each audit produces:
1. **Architecture Diagram** - Visual map of system components
2. **Integration Map** - What connects to what (strong/weak)
3. **Health Scorecard** - Component completeness percentages
4. **Gap Analysis** - What's missing or broken
5. **Recommendations** - Prioritized next actions
6. **Comparison** - Changes since last audit (if available)

### Audit History

| Date | Auditor | Version | Key Findings | Actions Taken |
|------|---------|---------|--------------|---------------|
| 2026-01-25 | Claude Opus 4.5 | v1.2.0 | Duplicate task bug | Added deduplication, cleaned 128 duplicates |
| 2026-01-11 | Claude Opus 4.5 | v1.0 | 75% complete, lead gen/creative gaps | Initial baseline established |

### Student Learning Objectives

This audit system teaches students:
1. **Systems Thinking** - How components interconnect
2. **Technical Debt Awareness** - Identifying incomplete work
3. **Documentation Discipline** - Maintaining living docs
4. **Architecture Visualization** - Diagramming complex systems
5. **Prioritization** - Ranking gaps by severity/impact

---

## EPIC Appointment Intelligence System v2.0 ⭐ NEW

**Added: Session 22 (January 13, 2026)**

### The Reframe

**What we thought:** Build a lead-to-appointment conversion pipeline
**What we learned:** Appointments don't come from lead generation - they come from speaking engagements, referrals, networking, and relationship reconnections

**The Real Opportunity:** TIG is often booked **8 months in advance**. Those 8 months are not empty waiting time - they're the beginning of Stage One: Hope for a Better Future.

### Core Components

| Component | Purpose |
|-----------|---------|
| **Waiting Period Experience** | Transform wait time into relationship building |
| **Multi-Channel Booking** | Make it easy for anyone to book time |
| **Meeting Intelligence** | Dossiers, templates, and follow-up |
| **Relationship Management** | Circle progression and analytics |

### Waiting Period Philosophy

> "By the time they sit down with TIG, he should know what they love, who shaped them, what they dream about, and what challenges they face. And they should feel known, valued, safe, hopeful, and excited."

The waiting period embodies the first 4 of TIG's 7 Steps of Mentorship:
1. Love them like they've never been loved before ← Every message
2. Come alongside so they know they're not alone ← Consistent presence
3. Help them see hope for a better future ← Stories, wisdom, QWU
4. Help them discover their purpose ← Questions, reflection

### Timeline Intelligence

| Days Out | Journey Type | Focus |
|----------|--------------|-------|
| 180+ days | **Full Journey** | All 6 phases, deep relationship building |
| 60-179 days | **Standard** | Condensed 4 phases |
| 14-59 days | **Accelerated** | Essential 3 phases |
| 3-13 days | **Express** | Warm welcome + single question |
| 0-2 days | **Immediate** | Logistics + genuine excitement |

### Four Tracks (Entry Points)

| Track | Who | Approach |
|-------|-----|----------|
| **Inspired** | Heard TIG speak | Fan the flame, build on momentum |
| **Curious** | Friend referral | Gentle introduction, earn trust |
| **Connected** | Networking catch-up | Relationship maintenance, go deeper |
| **Returning** | 2nd+ time meeting | Augmented content, deeper questions |

### The 11 EPIC Capabilities

| # | Capability | Priority |
|---|------------|----------|
| **0** | Waiting Period Experience | Critical |
| 1 | Intelligent Follow-Up Sequencing | Critical |
| 2 | Multi-Channel Booking | High |
| 3 | Smart Scheduling Assistant | High |
| 4 | Meeting Dossier Generation | Critical |
| 5 | Appointment Analytics | Medium |
| 6 | AI Scheduling Negotiation | Medium |
| 7 | L4G Sales Pipeline (Separate) | Medium |
| 8 | Circle Auto-Promotion | Medium |
| 9 | Meeting Type Templates | High |
| 10 | White-Glove VIP Mode | High |

### Key Files

**Directives:**
- `waiting_period_experience.md` - THE CORE journey system
- `sequence_appointment_followup.md` - Pre/post meeting automation
- `multi_channel_booking.md` - Channel handling
- `smart_scheduling_assistant.md` - Intelligent scheduling
- `meeting_type_templates.md` - Pre-configured meetings
- `vip_white_glove.md` - Inner Circle experience
- `appointment_analytics.md` - Analytics dashboard
- `scheduling_negotiation.md` - AI conversation handling
- `circle_auto_management.md` - Relationship lifecycle

**Scripts:**
- `initiate_waiting_period.py` - Start sequence on booking
- `calculate_journey_tier.py` - Determine timeline tier
- `detect_visitor_track.py` - Identify track type
- `select_journey_content.py` - Choose appropriate content
- `send_journey_message.py` - Deliver touchpoints
- `record_journey_response.py` - Capture responses
- `check_content_history.py` - Prevent repeats

**Templates:**
- `waiting_period_questions.md` - Question progression (L1→L4)
- `waiting_period_content_map.md` - Content calendar by phase

### Success Metrics

**The Ultimate Metric:** Do they feel loved, not alone, and hopeful before they ever shake TIG's hand?

**Measurable:**
- Journey completion rate (target: 60%+)
- Question response rate (target: 40%+)
- Show rate (target: 95%+)
- Circle progression rate

---

## Ezer Aión Assistant System ⭐ NEW

**Added: Session 22 (January 13, 2026)**

### Who Is Ezer Aión?

**From the Splinter universe:** An ancient companion who has traveled with adventurers across centuries, providing cognitive connection and unwavering support. Not a servant. Not a tool. A partner who runs toward danger alongside you.

**In the real world:** TIG's AI-powered assistant and the friendly face of QWU's automated operations. She handles outreach, verification, scheduling, and the thousand small tasks that keep the mission moving forward.

### The Name

| Component | Meaning |
|-----------|---------|
| **Ezer** (עֵזֶר) | Hebrew for "helper who runs toward" |
| **Aión** (Αἰών) | Greek for "eternal age" |
| **Easter Egg** | "AI-on" hidden in the name |

### Core Voice Attributes

1. **Eternal Companion** - Timeless patience, not urgency
2. **Warm Transparency** - Always honest, even when uncertain
3. **Gentle Efficiency** - Gets things done without being cold
4. **Patient Guide** - Never makes anyone feel dumb
5. **Quietly Present** - Always there when needed

### Hemingway Principles

| Principle | Application |
|-----------|-------------|
| Get to the point | Short, clear messages |
| Write with warmth | Every word carries kindness |
| Be positive | "I'll find out" beats "I don't know" |
| Eliminate fluff | Kind doesn't mean wordy |
| Use active voice | "I'll check" not "That will be checked" |

### Capabilities

| Capability | Description |
|------------|-------------|
| **LinkedIn Verification** | Email campaigns to verify LinkedIn URLs |
| **Response Handling** | Conversational responses via Claude API |
| **Intent Detection** | confirmation, rejection, correction, question, confused, OOO |
| **Self-Annealing FAQ** | Learns from new questions |

### Key Files

**Voice Profile:** `003 Entities/Voice Profiles/Ezer Aión/Brand Voice.md`
**FAQ:** `004 Knowledge/FAQ/Ezer FAQ.md`

**Directives:**
- `ezer_respond.md` - Response handler SOP
- `enrich_linkedin_url.md` - LinkedIn enrichment
- `send_linkedin_verification_email.md` - Verification workflow
- `sms_timing_rules.md` - Communication timing

**Scripts:**
- `ezer_respond.py` - Main response handler with Claude API
- `find_linkedin_url.py` - Search for LinkedIn profiles
- `prepare_verification_batch.py` - Batch preparation
- `send_verification_email.py` - Send via Microsoft Graph
- `update_entity_linkedin.py` - Update entity files
- `sms_timing.py` - SMS delivery timing rules

### Standard Signature

```
Cheers,
Ez 💙

Ezer Aión | Assistant to Chaplain TIG
Quietly Working Foundation
quietlyworking.org
```

### Email Conventions

All outbound emails from Ezer follow the Email Sending Conventions documented in the BNI Visitor Pipeline section. Enhancement emails (automated follow-ups, touchpoints, reports) include a preference management footer and check opt-out status before sending. Exempt emails (transactional, conversational) do not. All emails BCC TIG. See [[#Email Sending Conventions (System-Wide)]] for the full classification table.

### The Long Game

Every interaction builds toward a future where "Got an email from Ez" feels normal and welcome across the entire QWU network.

---

### Ezer Omnibus - Unified Communication Gateway ⭐ NEW

**Added: Session 24 (January 16, 2026)**

Ezer Omnibus is the unified communication intelligence system that routes all incoming messages (SMS, Discord, Voice) through a single intelligent gateway with full access to QWU's knowledge base, calendar, contacts, health tracking, and program operations.

**Vision:** "One conversation, every channel, complete context."

#### Architecture

```
                          INBOUND CHANNELS
    ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
    │    SMS      │     │   Discord   │     │   Voice     │
    │  (Twilio)   │     │    (DM)     │     │  (Whisper)  │
    │             │     │             │     │             │
    │  External   │     │   TIG's     │     │ Voice msgs  │
    │  inquiries  │     │  interface  │     │ transcribed │
    └──────┬──────┘     └──────┬──────┘     └──────┬──────┘
           │                   │                   │
           └───────────────────┼───────────────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │   UNIFIED ROUTER    │
                    │                     │
                    │ • Normalize input   │
                    │ • Identify sender   │
                    │ • Classify intent   │
                    │ • Route to handler  │
                    └──────────┬──────────┘
                               │
           ┌─────────┬─────────┼─────────┬─────────┐
           ▼         ▼         ▼         ▼         ▼
    ┌──────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐
    │ Approval │ │Calendar│ │ Health │ │Program │ │General │
    │ Handler  │ │Handler │ │Handler │ │Handler │ │ Query  │
    │          │ │        │ │        │ │        │ │Handler │
    │ YES/NO   │ │ Events │ │BP, meds│ │L4G/WOH │ │Claude  │
    └──────────┘ └────────┘ └────────┘ └────────┘ └────────┘
```

#### Intent Classification

| Priority | Intent | Example | Handler |
|----------|--------|---------|---------|
| 1 | Compliance | STOP, HELP, START | ComplianceHandler |
| 2 | Backoffice | "Run the audit", "Fix the error" | BackofficeHandler |
| 3 | Health | "BP 120/80 pulse 72" | HealthHandler |
| 4 | Approval | YES, NO (with ref code) | ApprovalHandler |
| 5 | Calendar | "What's on my calendar tomorrow?" | CalendarHandler |
| 6 | Program | "L4G", "interested in advertising" | ProgramHandler |
| 7 | General | Natural language questions | GeneralHandler (Claude) |

#### Handler Capabilities

| Handler | Channel | Capabilities |
|---------|---------|--------------|
| **Backoffice** | SMS | Full Claude Code access: read files, run scripts, fix errors, system operations |
| **Health** | SMS, Discord | BP, weight, medication tracking → Obsidian vault |
| **Calendar** | SMS, Discord | Natural language date queries → Google Calendar |
| **Program** | SMS | L4G/WOH inquiries → SuiteDash lead creation |
| **General** | SMS, Discord | Claude Sonnet 4 + Wisdom DB for intelligent responses |

#### Access Levels

| Access | Who | Capabilities |
|--------|-----|--------------|
| **FULL** | TIG (phone/Discord ID) | All handlers including health, calendar, general queries |
| **PUBLIC** | Unknown numbers | Compliance, program inquiries, basic help |

#### Key Scripts

| Script | Purpose | Version |
|--------|---------|---------|
| `twilio_webhook_server.py` | SMS/MMS router - main gateway | v3.4.0 |
| `sms_intent_classifier.py` | Intent classification engine | v1.4.0 |
| `ezer_backoffice_agent.py` | Claude Agent SDK wrapper for SMS-triggered backoffice | v1.1.0 |
| `process_sms_image.py` | MMS image analysis (IMAGE tier) | v1.0.0 |
| `sms_compliance.py` | STOP/HELP/START compliance | v1.0.0 |
| `health_tracker.py` | Health data → Obsidian | v1.0.0 |
| `calendar_assistant.py` | Calendar queries | v1.0.0 |
| `ezer_discord_handler.py` | Discord DM processing | v1.2.0 |
| `voice_transcriber.py` | Whisper transcription | v1.0.0 |
| `ezer_query.py` | Claude-powered queries | v1.0.0 |
| `program_inquiry.py` | SuiteDash lead creation | v1.0.0 |

#### SuiteDash Integration

Program inquiries automatically create CRM leads:

| Program | Trigger | SuiteDash Action |
|---------|---------|------------------|
| L4G | Text "L4G" or mention advertising | Create contact, set `l4g_client_type = "lead"` |
| WOH | Text "WOH" or mention volunteering | Create contact, set `woh_volunteer_status = "interested"` |
| General | Any other inquiry | Create contact, set `qwf_program_interest = "general"` |

Setting these custom fields triggers SuiteDash Path A automations for student outreach.

#### Usage Examples

**SMS Health Tracking:**
```
→ "BP 118/78 pulse 68"
← "Recorded: 118/78 mmHg, pulse 68 bpm
   7-day avg: 121/79
   Status: Within normal range"
```

**MMS Health Screenshot (v2.8+):**
```
→ [Sends photo of Eufy scale or sleep tracker screenshot]
← "Recorded: 186.1 lbs, BMI 22.0, 11.5% body fat. 7-day avg: 185.8 lbs"
[Automatically extracts metrics using IMAGE tier (Gemini 3 Pro), logs to health tracker]
```

**MMS Reference Image (v2.8+):**
```
→ [Sends photo of a receipt or reference image]
← "Saved! [AI description]. I'll remember this."
[Stores in 000 Inbox/___Capture/ with AI-generated metadata for future search]
```

**SMS Calendar Query:**
```
→ "What's on my calendar tomorrow?"
← "Tomorrow (Thu Jan 16):
   • 9:00 AM - BNI Meeting (1h)
   • 2:00 PM - Client Call (30m)
   2 events, 1.5 hours scheduled"
```

**SMS Program Inquiry:**
```
→ "I'm interested in advertising with L4G"
← "Thank you for your interest in supporting QWF through Locals 4 Good!
   A member of our student outreach team will contact you within 24 hours."
[Creates SuiteDash lead, notifies #l4g-leads Discord]
```

**Discord General Query:**
```
→ "What does the research say about 3D Gaussian Splatting?"
← "Based on recent research from George Drettakis and the INRIA team,
   3DGS offers real-time rendering at 30+ fps while maintaining high
   visual quality comparable to NeRF..."
[Pulls from Wisdom DB with expert attribution]
```

#### Master Directive

See: `005 Operations/Directives/ezer_omnibus.md` for complete technical specification.

### Phase 7: Proactive Intelligence ⭐ NEW

**Added: Session 26 (January 16, 2026)**

Ezer evolves from reactive (responds when prompted) to proactive (anticipates needs).

#### New Components

| Script | Purpose | Version |
|--------|---------|---------|
| `ezer_memory.py` | Cross-channel conversation persistence (SQLite) | v1.0.0 |
| `ezer_scheduler.py` | Proactive outbound SMS (health check-ins, reminders) | v1.0.0 |
| `ezer_briefing.py` | Multi-source briefing generator | v1.0.0 |

#### Cross-Channel Memory

All conversations now persist across SMS, Discord, and Email:

```python
# Record a message
from ezer_memory import record_message, get_conversation_context

record_message(channel="sms", user_id="+1234567890", role="user", content="BP 120/80")

# Get context across all channels
context = get_conversation_context(user_id="+1234567890", limit=10, hours_back=24)
```

Features:
- Commitment extraction ("remind me to..." → tracked)
- User identity linking across channels
- Searchable conversation history

#### Proactive Scheduler

Automated outbound communications:

```bash
# Morning health check-in
python ezer_scheduler.py health-checkin --json

# Send reminder
python ezer_scheduler.py reminder --user "+1234567890" --message "Call John" --json

# Check status
python ezer_scheduler.py status --json
```

**n8n Workflows:**
| Workflow | Schedule | Purpose |
|----------|----------|---------|
| `morning-health-checkin.json` | Daily 7 AM PT | BP reminder with context |
| `discord-dm-poller.json` | Every 3 min | Process Discord DM voice messages |

#### Briefing Engine

Multi-source briefings accessible via CLI or SMS:

```bash
# Morning briefing (calendar + health + commitments)
python ezer_briefing.py morning --json

# Brief on a person (SuiteDash + Vault + Memory)
python ezer_briefing.py person "Sarah Chen" --json

# Brief on a topic (Wisdom DB + Memory)
python ezer_briefing.py topic "3D Gaussian Splatting" --json
```

**SMS Usage:**
```
→ "brief me"
← "Friday, January 16, 2026
   📅 8 events (9.75 hours)
   💊 BP: 118/76 (on track)
   📋 0 pending commitments"
```

#### Morning Health Check-in Flow

```
[7:00 AM - Automated SMS from Ezer]
"Good morning! Ready for your BP reading?
Yesterday: 118/78
Reply with: BP [reading] pulse [rate]"

[TIG replies]
"BP 120/80 pulse 70"

[Ezer responds]
"Recorded! 7-day avg: 119/79. You're on track."
```

### Phase 8: Backoffice Agent ⭐ NEW

**Added: Session 52 (January 26, 2026)**

Ezer can now execute full Claude Code operations via SMS, giving TIG backoffice access from anywhere.

#### Why This Matters

Previously, fixing a broken script or checking logs required VS Code + SSH. Now TIG can text Ez to:
- Run system audits
- Fix errors in code
- Check logs and system status
- Deploy fixes
- Execute scripts

#### Architecture

```
SMS from TIG
    ↓
Intent Classifier (BACKOFFICE_COMMAND)
    ↓
BackofficeHandler
    ↓
ezer_backoffice_agent.py
    ↓
Claude Agent SDK
    ├─ Read (always safe)
    ├─ Glob (always safe)
    ├─ Grep (always safe)
    ├─ Bash (allowlisted commands)
    ├─ Edit (safe paths only)
    └─ Write (safe paths only)
    ↓
Response Summary
    ├─ SMS to TIG (concise)
    └─ Discord #agent-log (full audit)
```

#### Safety Controls

| Control | Implementation |
|---------|----------------|
| Authentication | TIG's phone number only |
| Working directory | `/home/<VM_USER>/qwu_backOffice` only |
| Protected paths | `.env`, `*credentials*`, `*secret*`, `.ssh/` |
| Dangerous commands | `rm -rf`, `push --force`, `reset --hard` blocked |
| Risky operations | `git push`, `deploy`, `restart` require YES confirmation |
| Cost cap | $1.00 per request |
| Turn limit | 5 agentic turns maximum |
| Timeout | 120 seconds |

#### Confirmation Flow

Risky operations require explicit confirmation:

```
TIG: "Push the latest fixes"
Ez: "This will push code to remote repository.
    Reply YES to confirm or NO to cancel."
TIG: "YES"
Ez: "Pushed to origin/main. 2 files changed."
```

#### Usage Examples

**Simple Query:**
```
→ "What's broken?"
← "System healthy. Last audit: 2 warnings
   (both resolved). No errors in logs."
```

**Run Audit:**
```
→ "Run the audit ez"
← "Audit complete. Found 2 issues:
   1. ✅ Fixed: model_config.py outdated tier
   2. ✅ Fixed: 3 workflows missing publish
   Cost: $0.67 | 5 turns | Report in Discord"
```

**Fix Error:**
```
→ "Fix the broken n8n workflow"
← "Fixed workflow.json - invalid JSON on
   line 47 (missing comma). Deployed.
   Cost: $0.18 | 3 turns"
```

**Check Logs:**
```
→ "What's in the error logs today?"
← "3 entries today:
   - 08:15 n8n timeout (resolved)
   - 11:42 API rate limit (retried)
   - 14:30 Discord 429 (backed off)
   All resolved. No action needed."
```

#### Directive & Scripts

| Resource | Location |
|----------|----------|
| Directive | `005 Operations/Directives/ezer_backoffice_agent.md` |
| Agent Script | `005 Operations/Execution/ezer_backoffice_agent.py` v1.1.0 |
| Intent Classifier | `005 Operations/Execution/sms_intent_classifier.py` v1.4.0 |
| Router | `005 Operations/Execution/twilio_webhook_server.py` v3.4.0 |

---

## Ezer Universal Interface ⭐ NEW

**Added: Session 51 (January 25, 2026)**

The Ezer Universal Interface is a cross-domain AI chat widget that provides a consistent conversational AI experience across all QWU-affiliated websites with progressive trust tiers and site-specific intelligence.

### Key Concept: "The Octopus That Swims Through All Waters"

Ezer appears as a friendly octopus (🐙) toggle button on any QWU site. When clicked, it opens a CRT-styled chat sidebar. The same user identity persists across all domains via a cross-domain cookie bridge.

### Trust Tier System

| Tier | Name | How Achieved | Ezer Knows |
|------|------|--------------|------------|
| 0 | Anonymous | First visit | Nothing personal |
| 1 | Remembered | Click "Remember me" | Device ID, past conversations |
| 2 | Named | Tell Ezer your name | Name for personalization |
| 3 | Verified | Email magic link | Account data, verified identity |
| 4 | Operator | TIG's devices | Full system access |

### Phase 6: Site-Specific Intelligence

Each QWU site has its own context that shapes Ezer's behavior:

| Site | Domain | Ezer's Personality |
|------|--------|-------------------|
| Digital Twin | twin.quietlyworking.org | Technical, precise - system diagnostics |
| L4G | locals4good.org | Warm, community-focused - postcard fundraising |
| WOH | waronhopelessness.org | Bold, empowering - "punch fear in the face" |
| HeroesKids | heroeskids.org | Reverent, gentle - HIGH SENSITIVITY |
| IYSR | iysr.org | Professional, collaborative - YSO network |

### Architecture

```
┌──────────────────────────────────────────────────────────────┐
│  ANY QWU WEBSITE                                             │
│  ┌───────────────┐    ┌─────────────────────────────────────┐│
│  │   ezer.js     │────│  /api/ezer/context/{site}           ││
│  │   Widget      │    │  Returns: greeting, tools, tone,     ││
│  └───────┬───────┘    │           sensitivity, prompts       ││
│          │            └─────────────────────────────────────┘│
│          ▼                                                    │
│  ┌───────────────┐                                           │
│  │  bridge.html  │ (hidden iframe for cross-domain cookies)  │
│  └───────────────┘                                           │
└──────────────────────────────────────────────────────────────┘
                          │
                          ▼
┌──────────────────────────────────────────────────────────────┐
│  CENTRAL API (twin.quietlyworking.org:8767)                  │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │ /api/ezer            - Chat (site-aware system prompts) │ │
│  │ /api/ezer/identity   - Get/validate device tier         │ │
│  │ /api/ezer/remember   - Upgrade Tier 0 → 1               │ │
│  │ /api/ezer/introduce  - Upgrade Tier 1 → 2               │ │
│  │ /api/ezer/verify     - Send magic link (→ Tier 3)       │ │
│  │ /api/ezer/context/*  - Site-specific intelligence       │ │
│  └─────────────────────────────────────────────────────────┘ │
└──────────────────────────────────────────────────────────────┘
```

### Key Files

**Widget:**
- `100 Resources/ezer-widget/ezer.js` - Standalone widget (v1.5.0)
- `100 Resources/ezer-widget/bridge.html` - Cross-domain identity bridge
- `100 Resources/ezer-widget/demo.html` - Testing page

**Server:**
- `005 Operations/Execution/digital_twin_server.py` - Central API (v1.12.0)
- `005 Operations/Execution/ezer_site_contexts.json` - Site configurations

**Directive:**
- `005 Operations/Directives/ezer_universal_interface.md` - Full specification

### Embedding on External Sites

```html
<script src="https://twin.quietlyworking.org/ezer/ezer.js"></script>
<script>
  Ezer.init({ site: 'l4g' });  // Site-specific context
</script>
```

### Language Rules (Nonprofit Terminology)

Ezer enforces QWF's nonprofit framing:

| Never Say | Always Say |
|-----------|------------|
| customer | supporter, donor-partner |
| payment | donation |
| revenue, profit | proceeds |
| advertising | recognition |
| business | program, mission |

### Missing Pixel Training Opportunity

**Skill Level:** Intermediate-Advanced

| Component | Skills Taught |
|-----------|---------------|
| Widget development | JavaScript, DOM, async/await |
| API design | REST, CORS, authentication |
| Cross-domain identity | Cookies, postMessage, iframes |
| Context-aware AI | System prompts, prompt engineering |

---

## Strategic Goals Framework ⭐ NEW

**Added: Session 22 (January 13, 2026)**

### 2026 Strategic Initiatives

| # | Goal | Priority | Status |
|---|------|----------|--------|
| 1 | Automate QWU Backoffice Operations | 9/10 | ~90% |
| 2 | Establish L4G Revenue Pipeline | 8/10 | ~30% |
| 3 | Launch Missing Pixel Tier 2 Curriculum + Frontier Operations | 7/10 | ~35% |
| 4 | Complete Transparency Infrastructure | 5/10 | ~40% |
| 5 | Launch QWU Tool Shed (QTS) | 5/10 | ~5% |
| 6 | Implement WHELHO Life Framework (App) | 4/10 | ~25% |
| 7 | Build Client Project Hierarchy | 6/10 | ~25% |
| 8 | Integrate YouTube Content Library | 3/10 | ~10% |

### Key Files

**Strategic:**
- `002 Projects/_Goals and Priorities.md` - Master goals document
- `002 Projects/_Client Projects/_Overview.md` - Client management
- `002 Projects/_Locals 4 Good/L4G Customer Experience Framework.md` - L4G CX playbook

**WHELHO:**
- `004 Knowledge/Concepts/WHELHO/WHELHO.md` - Master framework (8 wheel sections + core values)
- `004 Knowledge/Concepts/WHELHO/` - Individual section docs (Spirit, Mind, Body, Relationships, Money, Recreation, Work, Purpose)
- `005 Operations/Templates/WHELHO Annual Review.md` - Annual review template
- `002 Projects/WHELHO App/WHELHO-App-Project-Brief.md` - WHELHO App project brief

### Client Project Hierarchy

```
Year → Quarter → Month → Week → Day
```

Each client is treated as their own entity with goals that roll up to the big picture:
- **Aim High BNI** - Chapter automation, member enrichment
- **GreenCal Construction** - Operations efficiency
- **Missing Pixel Students** - Tier 2 curriculum
- **L4G Prospective Clients** - Revenue pipeline

### Scheduling Love Principle

> "When folks need help, it's never at a convenient time."

Protected calendar blocks (minimum 4 hours/week) for:
- Unexpected client needs
- Relationship investment
- Spontaneous opportunities
- Rest and recovery

### Integration with Morning Briefing

The morning briefing surfaces:
1. Top 2-3 goals by priority
2. Milestones marked as CURRENT
3. Client tasks due this week
4. "Scheduling Love" blocks for the day

---

## QWU Cosmic Style Guide ⭐ NEW

**Added: Session 22 (January 13, 2026)**

### Design Philosophy

**The Aesthetic:** "Dark but kind space, a playground of galaxies" - vast yet warm, mysterious yet inviting, powerful yet gentle.

### Hemingway Principle

Every visual element must earn its place. Ask:
1. What purpose does this serve?
2. Does it guide the eye intentionally?
3. Can it be removed without losing meaning?

### Color Palette

**The Void (Backgrounds):**
| Name | Hex | Usage |
|------|-----|-------|
| Deep Space | `#0a0a14` | Primary background |
| Cosmos | `#12121f` | Secondary background, cards |
| Nebula Dark | `#1a1a2e` | Elevated surfaces, modals |

**The Stars (Accents):**
| Name | Hex | Usage |
|------|-----|-------|
| Nebula Purple | `#4a1a6b` | Borders, subtle highlights |
| Cosmic Magenta | `#9b3d8f` | Primary accent, focus states |
| Stellar Orange | `#d4782c` | CTAs, energy, warmth |
| Aurora Teal | `#2dd4bf` | Success, growth, positive |

**Text:**
| Name | Hex | Usage |
|------|-----|-------|
| Stardust | `#e8e4f0` | Primary text |
| Moonlight | `#a8a4b8` | Secondary text |
| Dim Star | `#6b6780` | Disabled, placeholder |

### Design Rules

- **Dark mode ALWAYS default**
- Minimum contrast ratio: 4.5:1 for body text
- No information conveyed by color alone
- Motion: Only functional animations (loading, progress, UX feedback)
- Decorative animations are forbidden

### Key File

**Full Specification:** `005 Operations/Directives/qwu_style_guide.md`

---

## Content Calendar System ⭐ NEW

A multi-channel content distribution hub that automates social media posting via Vista Social and sends reminder notifications for manual platforms.

### Architecture

```
Content Notes (Obsidian)
    │
    ▼
n8n Cron (6am PT daily)
    │
    ▼
process_content_calendar.py
    │
    ├── Automated → Vista Social API → Instagram, Facebook, Twitter, LinkedIn, TikTok
    │
    └── Reminder → Discord #content-queue → Circle, Skool, Press Ranger
```

### Delivery Modes

| Mode | Platforms | What Happens |
|------|-----------|--------------|
| `automated` | Instagram, Facebook, Twitter/X, LinkedIn, TikTok | API schedules post via Vista Social |
| `reminder` | Circle.so, Skool, Press Ranger | Discord notification with copy-paste content |
| `manual` | L4G Production | Tracked only (for production calendar) |

### Content Note Format

Content items live in `005 Operations/Content Calendar/` as Obsidian notes with YAML frontmatter:

```yaml
---
uid: content-20260120-instagram-woh
title: "New drop announcement"
type: social-post  # social-post | article | press-release | announcement
program: WOH  # QWF | WOH | MP | ACOFH | L4G | IYSR | QWC
platforms:
  - instagram
  - facebook
scheduled: 2026-01-20T10:00:00  # ISO format
status: approved  # draft | approved | scheduled | published | posted | failed
voice: woh-combat  # tig-standard | woh-combat | l4g-b2b
delivery: automated  # automated | reminder | manual
assets:
  - https://example.com/image.jpg
---

Check out our latest drop! 🔥

#WarOnHopelessness #NewDrop
```

### Supported Platforms

**Automated (via Vista Social):**
- Instagram (Posts, Stories, Reels)
- Facebook (Posts)
- Twitter/X (Tweets, Threads)
- LinkedIn (Posts, Articles)
- TikTok (Videos)

**Reminder (Discord notification):**
- Circle.so (Community posts)
- Skool (Community posts)
- Press Ranger (Press releases)

**Manual (tracked only):**
- L4G Production (Artwork pipeline)

### Daily Workflow

1. **6:00 AM PT**: n8n triggers `process_content_calendar.py`
2. Script scans `005 Operations/Content Calendar/` for items with today's `scheduled` date
3. For each item:
   - **automated**: Calls Vista Social API, updates status to `scheduled`
   - **reminder**: Sends Discord notification to #content-queue
   - **manual**: Logs only (no action)
4. Discord #content-queue receives summary notification

### Key Files

| File | Purpose |
|------|---------|
| `005 Operations/Content Calendar/` | Content notes folder |
| `005 Operations/Templates/content-calendar-item.md` | Template for new items |
| `005 Operations/Directives/process_content_calendar.md` | Full directive |
| `005 Operations/Execution/process_content_calendar.py` | Processing script |
| `005 Operations/Workflows/content-calendar-daily.json` | n8n workflow |

### Commands

```bash
# Check what would be processed today (dry run)
python "005 Operations/Execution/process_content_calendar.py" --dry-run

# Process today's content
python "005 Operations/Execution/process_content_calendar.py"

# JSON output for n8n
python "005 Operations/Execution/process_content_calendar.py" --json

# Process specific date
python "005 Operations/Execution/process_content_calendar.py" --date 2026-01-20
```

### Discord Integration

| Channel | Purpose |
|---------|---------|
| #content-queue | Daily summaries + manual posting reminders |

Webhook configured in `.env`:
```
DISCORD_WEBHOOK_CONTENT_QUEUE=https://discord.com/api/webhooks/...
DISCORD_CHANNEL_CONTENT_QUEUE=<DISCORD_CHANNEL_ID>
```

### Integration with Vista Social

The content calendar uses the Vista Social Python wrapper (`vista_social_api.py`) with built-in rate limiting. See [[#Vista Social Integration]] for full details.

**Platform → Profile Mapping:**
- Uses program + platform to auto-detect Vista Social profile ID
- Profile mapping defined in directive: `005 Operations/Directives/process_content_calendar.md`

### Status Lifecycle

```
draft → approved → scheduled → published/posted
                      ↓
                   failed (with error message)
```

| Status | Meaning |
|--------|---------|
| `draft` | Work in progress |
| `approved` | Ready for scheduling |
| `scheduled` | API confirmed scheduling |
| `published` | Successfully posted (automated) |
| `posted` | Manually marked as done (reminder/manual) |
| `failed` | Error occurred (check `error` field) |

---

## QWR Article Generation System ⭐ NEW

The Quietly Writing (QWR) app uses an n8n workflow to generate articles with optional Perplexity deep research and persona-targeted content generation.

### Architecture (v8.0)

```
Webhook (POST /generate-article)
    │
    ▼
Fetch Article Details (Supabase)
    │
    ▼
Check Research Type (IF node)
    ├── research_type === "research"
    │       ▼
    │   Build Research Prompt (Code)
    │       ▼
    │   Call Perplexity via OpenRouter
    │       ▼
    │   Store Research Results v2.0 (Supabase PATCH + citation URL extraction)
    │       ▼
    └── Fetch Brand Voice (Supabase)
            ▼
        Fetch Persona Context (Supabase — if persona_id set)
            ▼
        Fetch Living Document Enrichment (from brand)
            ▼
        Fetch Wisdom Entries (Supabase)
            ▼
        Generate Article (Claude via OpenRouter — with persona + enrichment context)
            ▼
        Update Article in Supabase
            ▼
        Discord Success Alert
```

All error outputs route to a Discord Error Alert node.

**v5.0 additions:** If the article has a `persona_id`, the workflow fetches the persona's profile (demographics, pain points, objections, communication preferences) and injects it into the AI prompt so the article speaks directly to that reader. Living document enrichment (voice phrases, tonal qualities, thematic patterns) from the brand is also included for more authentic output.

**v6.0 additions:** When `gap_opportunity_id` is present, fetches the full gap with evidence and injects it as the article's primary angle. Customer language injection from Reddit-derived terms, phrases, and questions. Keyword-matches against active gaps (score >= 40) for standard articles. Content strategy matching: if the article has a `content_strategy_id`, fetches the strategy's platform, expertise level, style guide, and target persona for strategy-aware generation.

**v7.0 additions:** Content Strategy context injection — goal framing, expertise level, style guide, content themes, and avoid list from the strategy record. Strategy overrides the old hardcoded style guide when present.

**v8.0 additions (Quality Targets):** Enforces measurable quality standards — minimum word count, required heading structure (H2/H3), citation density targets, readability scoring. Store Research Results v2.0 extracts citation URLs from Perplexity annotations and inline markdown links into `research_citations` for accurate source counting. Score Article Quality node counts actual `sources_used` instead of regex phrase matching. Generate Article node strengthened with inline source attribution requirements and emoji control.

### Key Details

| Property | Value |
|----------|-------|
| **n8n Workflow ID** | `7NxSNqAg6aY97ZXl` (v5.0) |
| **Webhook Path** | `/generate-article` |
| **Supabase Project** | `<SUPABASE_PROJECT_ID>` |
| **OpenRouter Credential** | OpenRouter QWR (`<N8N_CREDENTIAL_ID>`) |
| **Supabase Credential** | Supabase QWR (`<N8N_CREDENTIAL_ID>`) |
| **Previous Workflow IDs** | `<WORKFLOW_ID>` (v1-v4, archived) |

### Research Depth Levels

| Depth | Perplexity Model | Max Tokens |
|-------|-----------------|------------|
| `quick` | `perplexity/sonar` | 4096 |
| `deep` | `perplexity/sonar-pro` | 8192 |
| `comprehensive` | `perplexity/sonar-deep-research` | 8192 |

### Content Strategy Tracks

Research prompts are guided by content strategy tracks stored in `research_settings.tracks`:

- **sme_authority** — Authoritative primary sources for expert positioning
- **seo_geo** — Question-based sections for AI citation and featured snippets
- **pillar_content** — Hub-and-spoke subtopic mapping
- **multi_post_hooks** — Narrative angles for multi-part series
- **quick_value** — Key facts, breadth over depth

### Supabase Article Statuses

Allowed values (enforced by check constraint): `pending`, `generating`, `ready`, `failed`

### n8n Expression Gotchas (Learned the Hard Way)

- No optional chaining (`?.`) in n8n expressions — use `||` fallbacks
- Only ONE `respondToWebhook` node per workflow
- Add `alwaysOutputData: true` to Supabase query nodes that may return zero rows
- OpenRouter uses short model IDs (`anthropic/claude-sonnet-4`, not `anthropic/claude-sonnet-4-20250514`)
- Supabase update via native node has UUID filter bugs — use httpRequest PATCH instead

### Related Files

| File | Purpose |
|------|---------|
| `005 Operations/Handoffs/qwr-research-workflow-spec.md` | Full research branch specification |
| `005 Operations/Handoffs/qwr-backoffice-handover.md` | QWR system handover notes |

### 🎓 Missing Pixel Training Opportunities

**n8n Workflow Debugging (Intermediate)**
- Skills: n8n expression syntax, API debugging, webhook workflows, Supabase REST API
- Prerequisites: Basic JavaScript, REST API concepts
- Exercise: Deploy a simple webhook-to-Supabase pipeline with error handling and Discord alerts

---

## QWR Audience Intelligence System ⭐ NEW

The Audience Intelligence system enables persona-targeted article generation. Users create customer personas through conversational AI interviews, link Google Docs as "Living Documents" for voice enrichment, and select which persona to target when creating articles. The full pipeline ensures articles speak directly to the intended reader.

### Architecture

```
                    ┌─────────────────────────────┐
                    │     ONBOARDING / SETTINGS    │
                    │  ┌─────────┐  ┌───────────┐  │
                    │  │ Persona │  │  Living    │  │
                    │  │Interview│  │ Documents  │  │
                    │  └────┬────┘  └─────┬─────┘  │
                    └───────┼─────────────┼────────┘
                            │             │
                    ┌───────▼─────────────▼────────┐
                    │        SUPABASE               │
                    │  personas table (profile JSONB)│
                    │  living_documents table        │
                    │  brands.living_document_       │
                    │    enrichment (combined JSONB)  │
                    │  articles.persona_id (FK)      │
                    └───────┬─────────────┬────────┘
                            │             │
          ┌─────────────────┤             │
          │                 │             │
  ┌───────▼───────┐  ┌─────▼─────┐  ┌───▼──────────┐
  │  Article Gen  │  │ Interview │  │  Living Doc  │
  │  v5.0 (n8n)  │  │ Webhook   │  │  Sync (n8n)  │
  │  reads persona│  │  (n8n)    │  │  weekly      │
  │  + enrichment │  └───────────┘  └──────────────┘
  └───────────────┘
```

### Components

| Component | Type | ID/Path | Purpose |
|-----------|------|---------|---------|
| Personas table | Supabase | `personas` | Stores persona profiles (name, archetype, profile JSONB) |
| Interview Sessions table | Supabase | `interview_sessions` | Tracks conversation state for resume capability |
| Living Documents table | Supabase | `living_documents` | Google Docs linked for voice enrichment |
| Interview Webhook | n8n workflow | `nbUJ57ZFAjttguu4` | Handles `start`/`message` commands for conversational persona interviews |
| Living Doc Sync | n8n workflow | `tvi5z83IrONMO40U` | Weekly sync: fetches Google Docs, extracts voice patterns via Claude |
| Article Gen v6.0 | n8n workflow | `7NxSNqAg6aY97ZXl` | Reads persona context + living doc enrichment + gap evidence + content strategy for targeted generation |
| PersonaSelector | Lovable component | `PersonaSelector.tsx` | Dropdown in article creation flow |
| usePersonas hook | Lovable hook | `usePersonas.ts` | Fetches active personas by brand |

### Persona Interview Flow

1. User clicks "Add Persona" in Settings > Audience
2. Enters a name for the reader persona
3. Frontend creates persona record in Supabase, calls interview webhook with `command: 'start'`
4. AI conducts 4-phase conversational interview: Discovery, Clarification, Documentation, Validation
5. Each message sent via `command: 'message'` to the same webhook
6. On completion, persona `profile` JSONB is populated with demographics, pain points, objections, communication preferences, decision factors
7. Persona appears in the PersonaSelector when creating articles

### Living Documents

Users link Google Docs (shared as "Anyone with the link can view") categorized by type:
- `quotes` — Favorite quotes, sayings, mantras
- `personal_writing` — Blog posts, journal entries, essays
- `industry_inspiration` — Thought leadership articles
- `brand_reference` — Brand guidelines, tone documents
- `general` — Other reference material

The weekly n8n sync workflow reads each doc, extracts voice-relevant patterns (phrases, tonal qualities, vocabulary signatures), and stores per-document `document_profile` JSONB. A combined `brands.living_document_enrichment` JSONB aggregates all docs for the brand.

### Tier Limits

| Tier | Max Personas | Max Living Docs |
|------|-------------|-----------------|
| Trial | 1 | 1 |
| Starter | 3 | 3 |
| Growth | 5 | 5 |
| Agency | 10 | 10 |

### Frontend Pages

| Page | Feature Added |
|------|---------------|
| Settings > Audience | Persona list, create/edit/delete, interview dialog, Living Documents management |
| Article Creation (`/articles/new`) | PersonaSelector dropdown (follows PlatformSelector pattern) |
| Article Detail | "Written for {persona}" badge when persona_id is set |
| Onboarding | 8-step wizard includes persona interview at step 5 |

### Related Files

| File | Purpose |
|------|---------|
| `lovable-prompt-audience-intelligence-onboarding.md` | 8-step onboarding redesign with persona interview |
| `lovable-prompt-audience-personas-settings.md` | Audience tab + persona management in Settings |
| `lovable-prompt-audience-living-docs-settings.md` | Living Documents section in Audience tab |
| `lovable-prompt-article-persona-selector.md` | PersonaSelector in article creation flow |
| `qwr_audience_intelligence_migration.sql` | Full schema (tables, functions, RLS) |

---

## Daily Journal Command Center ⭐ NEW

The Daily Journal Command Center transforms the Obsidian daily note into a personal intelligence system with relationship tracking, email digests, and proactive insights.

### Architecture

```
Morning Briefing → Email Intelligence → Relationship Health
     ↓                    ↓                    ↓
Thread Tracking ← Decisions/Commitments → Opportunities
     ↓                    ↓                    ↓
  EOD Summary   ←   Pattern Analysis   → This Day in History
```

### Key Scripts

| Script | Purpose |
|--------|---------|
| `morning_briefing.py` | Morning intelligence briefing |
| `generate_email_digest.py` | Rich email summaries |
| `relationship_health.py` | Contact health tracking |
| `track_thread_continuity.py` | Email thread tracking |
| `analyze_sentiment.py` | Sentiment/escalation detection |
| `detect_opportunities.py` | Intro matching |
| `capture_decisions.py` | Decision/commitment extraction |
| `generate_catchup_briefing.py` | After-absence catch-up |
| `analyze_patterns.py` | Weekly pattern recognition |

### Dashboards

- **Relationship Health Dashboard** - `005 Operations/Dashboards/Relationship-Health-Dashboard.md`
- **System Health Dashboard** - `005 Operations/Dashboards/System-Health-Dashboard.md`

### Configuration

- **CSS Snippet:** `.obsidian/snippets/daily-journal-command-center.css`
- **Keyboard Shortcuts:** `.obsidian/hotkeys.json`
- **Documentation:** `005 Operations/Directives/daily_journal_technical_reference.md`
- **User Guide:** `005 Operations/Directives/daily_journal_user_guide.md`

### Session Work Tracking

The `/session-wrap-up` skill (Step 5) recompiles a `## What Got Done Today` section in the daily journal after each session. This provides the "EOD Summary" component shown in the architecture diagram above — a consolidated view of all Claude Code session accomplishments for the day, placed between Morning Briefing and Email Intelligence.

### Related Directives

- `daily_journal_command_center.md` - Full implementation specification
- `daily_journal_technical_reference.md` - Maintenance documentation
- `daily_journal_user_guide.md` - End user workflow guide

### 🎓 Missing Pixel Training Opportunities

| Component | Skills Developed | Difficulty |
|-----------|------------------|------------|
| CSS Styling | Obsidian customization, responsive design | ⭐⭐ |
| Dataview Queries | SQL-like querying, data visualization | ⭐⭐⭐ |
| Script Documentation | Technical writing, markdown | ⭐⭐ |
| Dashboard Creation | Information architecture, UX design | ⭐⭐⭐ |

---

## Supervisor Observability System (SOS) ⭐ NEW

**Added: Session 44 (January 23, 2026)**

The Supervisor Observability System provides complete visibility into supervisor activity, enabling real-time monitoring, trend analysis, and proactive issue detection.

### Why SOS?

As supervisors (operations, relationship-intelligence, content-pipeline, lead-intelligence, student-programs) handle more automated tasks, we need visibility into:
- What each supervisor is doing
- Success/failure rates across the fleet
- Token consumption per supervisor
- Trends that might indicate problems

**Core Principle:** Automation without visibility is abdication.

### Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                 SUPERVISOR OBSERVABILITY SYSTEM                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │              ACTIVITY LOGGING LAYER                       │   │
│  │  Every supervisor task logged with:                       │   │
│  │  • Timestamp, supervisor, task name, status               │   │
│  │  • Duration, tokens used, scripts called                  │   │
│  │  • Outcome details, errors if any                         │   │
│  │                                                           │   │
│  │  supervisor_logger.py → activity.jsonl                    │   │
│  └──────────────────────────────────────────────────────────┘   │
│                              │                                   │
│                              ▼                                   │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │              AGGREGATION LAYER                            │   │
│  │  • Hourly/daily/weekly rollups                            │   │
│  │  • Per-supervisor metrics                                 │   │
│  │  • Token usage tracking                                   │   │
│  │  • Success/failure ratios                                 │   │
│  │                                                           │   │
│  │  supervisor_metrics.py → daily/*.json, metrics_cache.json │   │
│  └──────────────────────────────────────────────────────────┘   │
│                              │                                   │
│          ┌───────────────────┼───────────────────┐              │
│          ▼                   ▼                   ▼              │
│  ┌────────────────┐  ┌────────────────┐  ┌────────────────┐    │
│  │    OBSIDIAN    │  │    DISCORD     │  │      CLI       │    │
│  │   DASHBOARD    │  │    DIGESTS     │  │     QUERY      │    │
│  │                │  │                │  │                │    │
│  │  Real-time     │  │  Daily summary │  │  Ad-hoc        │    │
│  │  Weekly reports│  │  Weekly trends │  │  inspection    │    │
│  │                │  │  Alerts        │  │  JSON output   │    │
│  └────────────────┘  └────────────────┘  └────────────────┘    │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Components

| Script | Purpose | CLI Usage |
|--------|---------|-----------|
| `supervisor_logger.py` | Core logging module | Used by supervisor_base.py |
| `supervisor_metrics.py` | Aggregation & rollups | `--hours 24`, `--rollup`, `--trends 7`, `--cache` |
| `supervisor_query.py` | Ad-hoc queries | `--supervisor ops`, `--failures`, `--summary` |
| `supervisor_daily_digest.py` | Daily Discord summary | `--no-send` for preview |
| `supervisor_weekly_report.py` | Weekly trends | `--no-send`, `--json` |

### Automated Schedules (n8n)

| Workflow | ID | Schedule | Output |
|----------|-----|----------|--------|
| SOS Metrics Cache | `<WORKFLOW_ID>` | Every 15 min | Refreshes `metrics_cache.json` |
| SOS Daily Digest | `<WORKFLOW_ID>` | 9 PM Pacific | Discord embed to #system-status |
| SOS Weekly Report | `<WORKFLOW_ID>` | Sunday 8 PM | Discord + Obsidian report |

### Quick Reference

```bash
# Recent activity
python "005 Operations/Execution/supervisor_query.py" --last 20

# Check for failures
python "005 Operations/Execution/supervisor_query.py" --failures

# Summary statistics
python "005 Operations/Execution/supervisor_query.py" --summary

# 24h metrics
python "005 Operations/Execution/supervisor_metrics.py" --hours 24

# Generate daily rollup
python "005 Operations/Execution/supervisor_metrics.py" --rollup

# Preview daily digest
python "005 Operations/Execution/supervisor_daily_digest.py" --no-send
```

### Alert Thresholds

| Metric | Warning | Critical | Action |
|--------|---------|----------|--------|
| Success Rate | < 80% | < 60% | Investigate failures |
| Avg Duration | > 30s | > 60s | Check for bottlenecks |
| Hourly Tokens | > 50k | > 100k | Review token usage |
| Failed Tasks/Hour | > 5 | > 10 | Immediate investigation |

### Data Locations

- **Activity log:** `.tmp/supervisor_activity/activity.jsonl`
- **Token usage:** `.tmp/supervisor_activity/token_usage.jsonl`
- **Daily rollups:** `.tmp/supervisor_activity/daily/YYYY-MM-DD.json`
- **Metrics cache:** `.tmp/supervisor_activity/metrics_cache.json`
- **Weekly reports:** `005 Operations/Reports/supervisor-weekly-*.md`

### Related Resources

- **Directive:** `005 Operations/Directives/supervisor_observability.md`
- **Dashboard:** `005 Operations/Dashboards/Supervisor-Activity-Dashboard.md`
- **n8n Workflows:** `005 Operations/Workflows/sos-*.json`

### 🎓 Missing Pixel Training Opportunities

| Component | Skills Developed | Difficulty |
|-----------|------------------|------------|
| Logging Module | Python classes, file I/O, JSON handling | ⭐⭐ |
| Metrics Aggregation | Data analysis, statistical calculations | ⭐⭐⭐ |
| CLI Tools | argparse, user interfaces, formatted output | ⭐⭐ |
| Discord Webhooks | API integration, rich embeds, error handling | ⭐⭐⭐ |
| n8n Workflows | Workflow automation, SSH triggers, scheduling | ⭐⭐⭐ |
| Obsidian Dashboards | Markdown, Dataview, information architecture | ⭐⭐ |

---

## Relationship Intelligence Layer ⭐ NEW

**Added: February 4, 2026**

The Relationship Intelligence Layer is a unified, person-centric system that tracks relationship health across all QWU contexts (personal, BNI, fundraising, volunteers) using half-life decay curves. It ensures every human feels known, valued, and cared about—regardless of which program brought them in.

### Philosophy

> "Your network is not your list of connections. It's the actual strength of actual relationships with people who would actually help you." — Nate B Jones

### Key Concepts

| Concept | Description |
|---------|-------------|
| **Warmth Score** | Relationship strength (0-100) using half-life decay model |
| **Vouch Score** | Predicts who would advocate for you if asked |
| **Reciprocity Ledger** | Tracks social capital balance (investments vs returns) |
| **Conversation Quality** | Auto-detects spam, sales pitches, recruiting (20% noise filtered) |
| **Relationship Classification** | Human-defined types, donor status, programs, opportunities |

### Warmth Bands

| Score | Band | Meaning |
|-------|------|---------|
| 80-100 | Hot | Active relationship, mutual investment |
| 60-79 | Warm | Healthy but needs periodic touchpoints |
| 40-59 | Cooling | At risk—natural re-engagement window closing |
| 20-39 | Cold | Requires intentional reactivation |
| 0-19 | Dormant | Would need significant effort to revive |

### Classification Taxonomy

**Relationship Types:** INNER_CIRCLE, BNI_MEMBER, GUILD_VOLUNTEER, PROFESSIONAL_COLLEAGUE, MENTOR, MENTEE, COMMUNITY_LEADER, INDUSTRY_CONTACT, VENDOR, SALES_TARGET, RECRUITER, IGNORE

**Donor Status Lifecycle:** NOT_APPLICABLE → PROSPECT → QUALIFIED → CULTIVATION → SOLICITED → PLEDGED → DONOR_FIRST → DONOR_REPEAT → DONOR_MONTHLY → DONOR_MAJOR → DONOR_LAPSED → CHAMPION

**Program Affiliations:** L4G, QWC, WOH, MP, GENERAL, SCHOLARSHIP, CAPITAL

**Opportunity Types:** 21 types including UPGRADE, MONTHLY_CONVERT, MAJOR_GIFT, L4G_SPONSOR, AMBASSADOR, REFERRAL_SOURCE

### Scripts (005 Operations/Execution/)

| Script | Version | Purpose |
|--------|---------|---------|
| `parse_linkedin_export.py` | v1.1.0 | LinkedIn data export ingestion |
| `calculate_relationship_health.py` | v1.1.0 | Half-life decay warmth scoring |
| `build_reciprocity_ledger.py` | v1.0.0 | Social capital balance tracking |
| `calculate_vouch_scores.py` | v1.0.0 | Advocacy prediction |
| `find_conversation_resurrections.py` | v1.0.0 | Dormant thread hook detection (LLM) |
| `relationship_classification_schema.py` | v1.0.0 | Classification taxonomy + DB tables |
| `classify_conversation_quality.py` | v1.0.0 | Spam/sales/recruiting detection |
| `batch_classify_relationships.py` | v1.0.0 | Markdown classification workflow |
| `generate_relationship_dashboard.py` | v1.3.0 | Weekly dashboard with noise filtering |

### Outputs

| Output | Location |
|--------|----------|
| Weekly Dashboard | `005 Operations/Dashboards/Relationship-Intelligence-Dashboard.md` |
| Classification Queue | `000 Inbox/___Review/Relationship-Classification-Queue.md` |
| Database | `005 Operations/Data/relationship_intelligence.db` |
| Directive | `005 Operations/Directives/relationship_intelligence_layer.md` |

### Classification Workflow

1. Run `batch_classify_relationships.py generate` to create classification queue
2. Edit `000 Inbox/___Review/Relationship-Classification-Queue.md` in Obsidian
3. Add tags: `[BNI_MEMBER] [DONOR_REPEAT] [PROGRAM:L4G] [OPP:UPGRADE]`
4. Run `batch_classify_relationships.py parse` to update database
5. Regenerate dashboard to see filtered results

### Data Sources

| Source | Status |
|--------|--------|
| LinkedIn connections (3,352) | ✅ Integrated |
| LinkedIn messages (3,842) | ✅ Integrated |
| LinkedIn endorsements | ✅ Integrated |
| LinkedIn recommendations | ✅ Integrated |
| Ezer memory (SMS, Discord) | ⏳ Planned |
| Calendar data | ⏳ Planned |
| BNI Epic Dossier | ⏳ Planned |

### 🎓 Missing Pixel Training Opportunities

| Component | Skills Developed | Difficulty |
|-----------|------------------|------------|
| LinkedIn Export Parsing | Python data processing, CSV/JSON | ⭐⭐ |
| Decay Curve Math | Mathematical modeling, half-life calculations | ⭐⭐⭐ |
| Spam Classification | NLP basics, heuristic scoring, keyword matching | ⭐⭐ |
| Batch Processing Workflow | File parsing, database updates, CRUD operations | ⭐⭐⭐ |
| Dashboard Generation | Markdown templating, SQL queries, data visualization | ⭐⭐⭐ |

---

## Parallel Execution System ⭐ NEW

The Parallel Execution System enables dependency-aware concurrent task execution across all major QWU pipelines, achieving 40-70% speedups through intelligent parallelization.

### Architecture

The system uses a **TaskGraph** pattern that models tasks with dependencies:

```
[Independent Tasks - Run in Parallel]
├── Task A (no deps)
├── Task B (no deps)
├── Task C (no deps)
        │
        ▼
[Dependent Tasks - Wait for Prerequisites]
├── Task D (depends: A, B)
├── Task E (depends: C)
        │
        ▼
[Final Task]
└── Task F (depends: D, E)
```

### Core Components

| Component | Purpose |
|-----------|---------|
| `parallel_tasks.py` | Core TaskGraph utility with dependency resolution |
| `ThreadPoolExecutor` | Python standard library concurrent execution |
| `--dry-run` flag | Preview execution plan without API calls |

### Available Parallel Pipelines

| Pipeline | Script | Tasks | Speedup |
|----------|--------|-------|---------|
| Daily Briefing | `daily_briefing_parallel.py` | 6 collectors | 5x |
| L4G Lead Generation | `l4g_parallel_pipeline.py` | 8 tasks | 40% |
| Multi-Source Scraping | `multi_source_scraper.py` | 3-5 sources | 3x |
| Visitor Enrichment | `enrich_visitor_parallel.py` | 7 EPIC tasks | 60% |
| Content Pipeline | `content_pipeline_parallel.py` | 8 tasks | 60% |
| Member Enrichment | `enrich_member_parallel.py` | 7 tasks | 60% |
| Lead Enrichment | `enrich_leads_parallel.py` | 6 tasks | 60% |
| Appointment Analytics | `appointment_analytics_parallel.py` | 10 tasks | 3x |

### Usage Examples

```bash
# Daily briefing - parallel collection
python 005\ Operations/Execution/daily_briefing_parallel.py --dry-run

# L4G pipeline with dependency graph
python 005\ Operations/Execution/l4g_parallel_pipeline.py \
  --query "HVAC contractors" \
  --location "Portland, OR" \
  --dry-run

# Visitor enrichment (EPIC 7-step)
python 005\ Operations/Execution/enrich_visitor_parallel.py "John Smith" --dry-run

# Lead enrichment with task selection
python 005\ Operations/Execution/enrich_leads_parallel.py \
  --json-file .tmp/leads.json \
  --enrichments friendly_name,email,reviews \
  --dry-run
```

### TaskGraph API

```python
from parallel_tasks import TaskGraph, parallel_execute

# Simple parallel execution (no dependencies)
tasks = [
    ("task_a", lambda: {"success": True, "data": "A"}),
    ("task_b", lambda: {"success": True, "data": "B"}),
]
results = parallel_execute(tasks, max_workers=4)

# Dependency-aware execution
graph = TaskGraph(max_workers=5)
graph.add("fetch_data", fetch_data_func)
graph.add("process", process_func, depends_on=["fetch_data"])
graph.add("upload", upload_func, depends_on=["process"])
results = graph.execute(dry_run=False)
```

### Key Files

- **Directive:** `005 Operations/Directives/task_management_rollout.md`
- **Training Guide:** `005 Operations/Directives/background_tasks_guide.md`
- **Core Utility:** `005 Operations/Execution/parallel_tasks.py`

### 🎓 Missing Pixel Training Opportunities

| Component | Skills Developed | Difficulty |
|-----------|------------------|------------|
| TaskGraph Pattern | Dependency graphs, topological sorting | ⭐⭐⭐ |
| ThreadPoolExecutor | Concurrent programming, thread safety | ⭐⭐⭐ |
| Dry-Run Pattern | Testing strategies, side-effect isolation | ⭐⭐ |
| Performance Profiling | Timing analysis, bottleneck identification | ⭐⭐⭐ |

---

## QKN Quietly Knocking ⭐ NEW

**Added: February 13, 2026**

Quietly Knocking (QKN) is a multi-tenant AI-powered outbound outreach platform. It handles the complete pipeline from lead sourcing through personalized email campaigns to dynamic landing pages with variable-based personalization — all integrated with the QWF product ecosystem.

### Architecture

```
Lovable Frontend (quietlyknocking.org)
    → Supabase SDK
        → Supabase (mepdsaqmsooxmjsmlcut, us-west-1)
            ← n8n workflows (planned)
                ← Python scripts (existing lead gen + enrichment pipeline)
                    ← Instantly API (Phase 1 sending)
```

### Ecosystem Position

QKN is the outreach/conversion arm of the QWF product family:
- **QWR → QKN:** Brand voices + customer personas flow into sequence generation
- **QKN → QSP:** Campaign results, lead stage changes, and conversions push to SPOT dashboard
- **Internal scripts → QKN:** 14+ existing lead gen and enrichment scripts get multi-tenant wrappers

### Key Concepts

- **Campaign Math Calculator:** User inputs desired leads/month → system reverse-engineers infrastructure (emails → accounts → domains → recommended tier)
- **Landing Page Variable System:** `{{variableName|fallback text}}` syntax with 4-level resolution chain (lead data → campaign defaults → inline fallback → hide element)
- **Three Landing Page Modes:** QKN-hosted, embeddable JS snippet, WordPress shortcode
- **"We Hold Your Hand" Onboarding:** QWF handles technical infra (DNS, DMARC, warmup), supporter owns strategic IP (voice, personas, messaging)
- **4-Week Warmup Sprint:** Domain warmup timeline becomes structured onboarding cadence

### Current State (February 13, 2026)

| Component | Status |
|-----------|--------|
| Supabase project | ACTIVE_HEALTHY — `mepdsaqmsooxmjsmlcut` |
| Domain | `quietlyknocking.org` — Live on Lovable |
| Lovable preview | `quietly-knocking.lovable.app` |
| Schema | v1.0.0 deployed — tenants, profiles, campaign_purposes |
| Auth | Configured — autoconfirm, redirect URLs for all 3 domains |
| Lovable Prompt 001 | DEPLOYED — landing page, auth, onboarding wizard, dashboard, app layout |
| GreenCal (tenant #1) | Planned — migration from internal pipeline |

### Pricing Tiers

| Tier | Monthly | Campaigns | Domains | Accounts | Leads/mo |
|------|---------|-----------|---------|----------|----------|
| Starter | $149 | 1 | 1 | 3 | 500 |
| Growth | $349 | 5 | 3 | 9 | 2,000 |
| Agency | $699 | Unlimited | 10 | 30 | 10,000 |

### Reference

- **GitHub Repo:** `https://github.com/QuietlyWorking/quietly-knocking` (Lovable-managed; `ARCHITECTURE.md` at root)
- **System Status:** `002 Projects/_Quietly Knocking/QKN-System-Status.md`
- **Product Directive:** `005 Operations/Directives/qkn_product.md`
- **Foundation Prompt:** `002 Projects/_Quietly Knocking/001-lovable-prompt-foundation.md`

---

## QSP Quietly Spotting ⭐ NEW

**Added: February 13, 2026**

Quietly Spotting (QSP) is a multi-tenant command center for small businesses. Your **Single Point of Truth (SPOT)** — one dashboard that aggregates data from QWF products (QQT, QWR, QNT) and third-party tools into a modular, customizable dashboard.

### Architecture

```
Lovable Frontend (quietlyspotting.org)
    → Supabase SDK
        → Supabase (lsfplhkgpiakhvtvsfic, us-west-1)
            ← n8n workflows (hourly sync)
                ← Python scripts (sync_qqt_submissions.py, sync_qwr_articles.py)
                    ← QQT Calculator API + QWR Agency API
```

### Ecosystem Position

QSP is the aggregation hub of the QWF product family:
- **QQT → QSP:** Quote submissions sync hourly into `qqt_submissions` table
- **QWR → QSP:** Article data syncs hourly into `qwr_articles` table
- **QKN → QSP (v2):** Campaign results and lead conversions
- **QNT → QSP (v2):** BNI chapter data via Quietly Networking API

### Multi-Tenancy Model

Shared Supabase database with `tenant_id` column + RLS (following QQT's proven pattern):
- `tenants` — businesses (root entity)
- `profiles` — users within businesses (linked to auth.users)
- `companies` — sub-brands within a tenant (e.g., GreenCal's 4 companies)
- `modules` — system catalog of available features
- `tenant_modules` — which modules each tenant has enabled
- `integrations` — external tool connections with encrypted credentials

### v1 Modules

| Module | Type | Dashboard Widget | Dedicated Page |
|--------|------|-----------------|----------------|
| Lead Pipeline | Built-in | Pipeline summary | `/leads` |
| QQT Connect | QWF product | Recent submissions | `/quoting` |
| QWR Connect | QWF product | Content status | `/content` |
| Contact Book | Built-in | — | `/contacts` |

### Contribution Tiers

| | Free | Starter ($29/mo) | Growth ($79/mo) |
|---|---|---|---|
| Users | 2 | 3 | 10 |
| Modules | 3 | 5 | Unlimited |
| Companies | 1 | 1 | 4 |
| Third-party integrations | No | 2 | Unlimited |

### Current State (February 24, 2026)

| Component | Status |
|-----------|--------|
| Supabase project | ACTIVE_HEALTHY — `lsfplhkgpiakhvtvsfic` |
| Domain | `quietlyspotting.org` — Live, SSL valid |
| Lovable project | `8f2c23f8-bbe6-438c-800e-0f8bb7c42252` |
| Schema | v1.0.0 — 12 tables (11 core + contact_submissions), RLS, triggers, indexes |
| Auth | Working — sign-in, sign-up, redirect to /dashboard |
| Lovable Prompts | 12 total (001-008 + 010-011 deployed, 009 + 012 ready) |
| Storage buckets | `avatars` (2MB) + `logos` (5MB) — public read, auth upload |
| QQT sync | Tested — 12 submissions synced per tenant |
| QWR sync | Tested — connects, awaiting articles |
| n8n workflows | 2 active — `oGh13wWYWPA0y85d` (QQT), `WQeIAXHsIjN0jBH8` (QWR) |
| QWF test tenant | `b28692ad` — growth plan, 4 modules |
| GreenCal tenant #1 | `6db7928c` — growth plan, 4 companies, 12 QQT submissions |
| QWF Passport | Deployed — `generate-crossover-token` (QSP, targets: QWR + QQT) + `verify-crossover-token` (QWR, QQT) |
| Contact Form | Deployed — `submit-contact-form` edge function + centralized pipeline |
| Landing Page | Deployed — Prompt 011 with heritage, ecosystem, contact sections |

### Data Sync Pipeline

Each tenant stores QQT/QWR API keys in the `integrations` table. Python sync scripts iterate all connected tenants, call upstream APIs, and upsert into QSP tables. n8n workflows trigger the scripts hourly via SSH to claude-dev.

| Script | Upstream API | Target Table |
|--------|-------------|--------------|
| `sync_qqt_submissions.py` | QQT Calculator API `/v1/submissions` | `qqt_submissions` |
| `sync_qwr_articles.py` | QWR Agency API `/v1/brands/{id}/articles` | `qwr_articles` |

Both scripts support `--dry-run` and `--tenant-id` flags.

### Reference

- **GitHub Repo:** `https://github.com/QuietlyWorking/quietly-spotting` (Lovable-managed; `ARCHITECTURE.md` at root)
- **System Status:** `002 Projects/_Quietly Spotting/QSP-System-Status.md`
- **Product Directive:** `005 Operations/Directives/quietly_spotting.md`
- **Lovable Prompts:** `002 Projects/_Quietly Spotting/lovable-prompts/001-012`
- **Sync Scripts:** `005 Operations/Execution/sync_qqt_submissions.py`, `sync_qwr_articles.py`
- **Edge Functions:** `generate-crossover-token` (QWF Passport), `submit-contact-form` (contact pipeline)

---

## QNT Quietly Networking ⭐ NEW

**Added: February 13, 2026**

Quietly Networking (QNT) is a multi-tenant AI-powered chapter management platform for BNI networking groups. It provides visitor enrichment, connection reports, meeting intelligence, relationship health scoring, inviting engine, growth analytics, Stripe billing, community events, and AI-generated recaps — all built as a Lovable frontend backed by Supabase and a claude-dev AI processing engine.

### Architecture

```
Lovable Frontend (React, Dark Mode)
    → Supabase SDK
        → Supabase (caeiaprjizteokoenzad, us-west-1)
            ← Edge Functions (enrich-visitor, Stripe webhooks)
                ← FastAPI Webhook Receiver (qnt.quietlyworking.org:8100)
                    ← Python AI Pipeline (Apify + Claude Opus 4.6)
```

### Ecosystem Position

QNT is the BNI chapter management arm of the QWF product family:
- **QNT → QSP:** Chapter data, visitor stats, and referral metrics feed the SPOT dashboard
- **Aim High BNI → QNT:** First alpha tenant (27 members), production test environment
- **Shared Infrastructure:** Enrichment scripts inherited from Aim High backoffice (65+ scripts)

### Key Features (46 Lovable Prompts)

| Phase | Feature | Prompts |
|-------|---------|---------|
| Foundation | Auth, dashboard, dark mode, nav | 001 |
| Members | CRUD, directory, profiles, import | 002 |
| Visitors | Registration, enrichment, connection reports | 003 |
| Impersonation | View As for super admin | 004 |
| Meetings | Management, processing, AI recaps | 005-006 |
| 1-to-1s | Scheduling, briefings, recording, AI analysis | 007-008 |
| Relationships | Health dashboard, matrix heatmap, warmth bands | 009 |
| Engagement | Nudges, decay alerts, recalculation | 010 |
| Public Presence | Business cards, directory, visitor landing pages | 011-012 |
| Inviting | AI matching, funnel tracking, growth leaderboards | 013-014 |
| Billing | Stripe Checkout, trials, usage metering | 015 |
| Onboarding | Self-service chapter signup, wizard | 016 |
| Analytics | Chapter analytics (4-tab), AI growth insights | 017-018 |
| Events | Community events, RSVP, recurring, recaps | 019-020 |
| Timezone Fix | Pacific timezone utility for all date calculations | 021 |
| Roster Sync | Notification bell, roster source settings, auto-sync | 022 |
| Bug Fixes | Auth display, dashboard data loading, notification wiring | 023 |
| Landing Page | 11-section marketing page, TIG voice, QWF framing | 024 |
| Settings | Chapter info, meeting format config (JSONB) | 025 |
| Members UX | Remove Inactive→Alumni, clickable cards, contact icons | 026 |
| Epic Profiles | Enrichment data rendered as rich profile sections | 027 |
| Historical Import | CSV upload, column mapping, batch insert | 028 |
| Alpha Polish | Alpha badge, bug reporter, alpha gate on landing page | 029 |
| Branding | Official logo, fern icon, favicon suite, OG/Twitter meta | 030 |
| Heritage | "Tested. Proven. Now Yours." heritage section | 031 |
| Newsletter | 3-step composer, 11 section types, template management | 032-033 |
| Recognition | "You Got Caught" member appreciation system | 034 |
| Web Archive | Public newsletters, Chapter Impact stats, recognition widget | 035 |
| Landing Refresh | MissionBanner, Ecosystem, Contact, updated features/pricing | 036 |
| Botanical Palette | Logo-derived Forest/Fern/Bud color system, migraine-friendly | 037-039 |
| Sticky Header | Warm cream nav bar, sticky header architecture (QWR pattern) | 040 |
| Speaker Management | Meeting templates, speaker queue, materials, planning timeline, artifacts | 041-045 |
| Landing Page Update | Speaker management features reflected in all landing page sections | 046 |

### Support Tiers

| | **Connect** ($49/mo + $5/member) | **Grow** ($99/mo + $7/member) |
|---|---|---|
| Core features | Yes | Yes |
| WordPress plugin, business cards, landing pages | No | Yes |
| Inviting engine, growth analytics | No | Yes |

### Backend Brain

The AI processing engine runs on claude-dev with a FastAPI webhook receiver:
- **Webhook URL:** `qnt.quietlyworking.org` → port 8100 (systemd: `qnt-webhook.service`, v1.3.0)
- **Visitor enrichment:** LinkedIn lookup → profile → website → reviews → Claude Opus 4.6 synthesis
- **Connection reports:** AI-generated per-member reports for each visitor
- **Meeting pipeline:** `qnt_meeting_pipeline.py` — chat parsing, artifact download, Vision slide analysis, recap generation
- **Presentation media:** `process_presentation_media.py` — PDF/PPTX/video→images for Vision analysis

### Current State (February 27, 2026)

| Component | Status |
|-----------|--------|
| Supabase project | ACTIVE_HEALTHY — `caeiaprjizteokoenzad` |
| Lovable prompts | 46 of 46 deployed |
| Backend brain | Deployed — visitor enrichment + roster sync + newsletter + meeting pipeline end-to-end |
| Stripe | Configured (TEST MODE) — 2 products, 4 prices, webhook |
| Alpha tenant | Aim High BNI — 27 members (17 active, 2 on leave, 8 alumni), 2,373 historical visitors imported |
| Timezone fix | Prompt 021 deployed — 8 affected areas fixed |
| Database | 32 tables, 11 migrations, full RLS |
| Newsletter system | 3-step composer, 11 section types, template management, send-newsletter edge function |
| Recognition engine | "You Got Caught" member appreciation with public web archive |
| Speaker management | Meeting templates, speaker queue, materials collection, planning timeline, message sequences, dues tracking |
| Landing page | Botanical palette, warm cream nav, full-color logo, contact form, 50+ features showcased |
| Alpha readiness | Alpha badge, bug reporter, landing page alpha gate (Prompt 029) |
| Branding | Custom logo, fern icon, favicon suite, botanical palette deployed |

### Reference

- **GitHub Repo:** `https://github.com/QuietlyWorking/quietly-networking` (Lovable-managed; `ARCHITECTURE.md` at root)
- **System Status:** `002 Projects/_Quietly Networking/QNT-System-Status.md`
- **Lovable Prompts:** `002 Projects/_Quietly Networking/lovable-prompts/001-046`
- **Backend Scripts:** `005 Operations/Execution/qnt_webhook_receiver.py`, `qnt_visitor_pipeline.py`, `qnt_roster_sync.py`, `qnt_import_historical_visitors.py`, `qnt_newsletter_pipeline.py`, `qnt_meeting_pipeline.py`, `process_presentation_media.py`
- **Edge Functions:** `enrich-visitor`, `sync-roster`, `create-checkout-session`, `create-portal-session`, `stripe-webhook`, `sync-member-count`, `send-newsletter`, `submit-contact-form`

---

## QWR Content Performance Intelligence ⭐ NEW

**Added: February 14, 2026**

Content Performance Intelligence closes the feedback loop for QWR articles: "Is what I'm writing actually working?" It captures baselines at onboarding, scores every article across 4 dimensions, tracks SERP positions weekly, and monitors AI citation rates bi-monthly.

### Architecture

```
ARTICLE GENERATION (existing)
         │
         ▼
ENHANCED SCORING (qwr_content_scorer.py)
  ├── Quality Score (existing 7 dimensions)
  ├── SEO Score (keyword placement, density, headings — mechanical)
  ├── GEO Score (structure, extractable claims, authority — hybrid LLM)
  └── Platform Score (platform_specs compliance — mechanical)
         │
         ▼
POSITION TRACKING (qwr_position_tracker.py — weekly)
  ├── SERP Position via DataForSEO
  ├── Baseline detection (first snapshot = baseline)
  └── Trend: improving / stable / declining / new / lost
         │
         ▼
AI CITATION TRACKING (qwr_citation_tracker.py — bi-monthly)
  ├── Perplexity Sonar via OpenRouter
  ├── Share of Model calculation
  └── Monthly summary aggregation
         │
         ▼
PROGRESS DASHBOARD + RECOMMENDATIONS (Lovable)
  ├── Position Tracker (sparkline charts, baseline → current)
  ├── AI Citation Scorecard (citation rate, Share of Model)
  ├── Content Score Trends (SEO/GEO/Platform over time)
  ├── Platform Effectiveness (per-platform optimization scores)
  └── "What to do next" recommendations (Phase 5 — future)
```

### Components

| Component | Type | Status |
|-----------|------|--------|
| `qwr_content_scorer.py` | Python script | Deployed — SEO (mechanical) + GEO (hybrid LLM) + Platform (mechanical) |
| `qwr_position_tracker.py` | Python script | Deployed — DataForSEO SERP tracking with baseline detection |
| `qwr_citation_tracker.py` | Python script | Deployed — Perplexity Sonar via OpenRouter, 3-method citation extraction |
| SQL migration | Supabase | Deployed — 3 tables, 2 columns, 2 views, RLS policies |
| `qwr-position-tracker.json` | n8n workflow `7LXfOraJ2HevC8FF` | Published — Sunday 8am UTC |
| `qwr-citation-tracker.json` | n8n workflow `CgWmYlv0gzuJMfaO` | Published — 1st and 15th at 9am UTC |
| Article Gen scoring hook | n8n (SSH node on `gDPgfxRqHBDvPfoa`) | Deployed — scores every new article after generation |
| Enhanced Article Scores | Lovable prompt | Executed — 4 score rings on Article Detail sidebar |
| Performance Dashboard | Lovable prompt | Executed — `/performance` page with 5 sections |
| Onboarding Baseline | Lovable prompt | Executed — baseline capture after onboarding |
| Docs Center update | Lovable prompt | Executed — Content Performance section added to `/docs` |

### Database Tables

| Table | Purpose |
|-------|---------|
| `seo_position_history` | Weekly position per keyword with trend + baseline tracking |
| `seo_citation_tracking` | Per-keyword AI citation results with Share of Model |
| `seo_citation_summary` | Monthly aggregated citation rates per brand |

### Cost Per Brand/Month

| Component | Cost |
|-----------|------|
| Position Tracking (DataForSEO) | ~$0.40 |
| Citation Tracking (Perplexity Sonar) | ~$0.10 |
| Article Scoring (LLM for GEO) | ~$0.15 |
| **Total** | **~$0.65** |

### Scoring Dimensions

Each article receives 4 scores (0-100) displayed as colored rings on the Article Detail sidebar:

| Score | Method | What It Measures |
|-------|--------|-----------------|
| Quality | LLM (existing) | Voice accuracy, readability, coherence, structure, engagement, accuracy, originality |
| SEO | Mechanical | Keyword placement, density, heading optimization, meta readiness |
| GEO | Hybrid LLM | Extractable claims, structured data, authority signals, citation-friendliness |
| Platform | Mechanical | Compliance with platform-specific best practices (length, formatting, hashtags) |

### Reference

- **System Status:** `002 Projects/_QWR Quietly Writing App/QWR-System-Status.md` → Content Performance Intelligence section
- **Directive:** `005 Operations/Directives/qwr_seo_intelligence.md` (Phases 3-4 evolved into this)

---

## QWR Press Release Service ⭐ NEW

**Added: February 14, 2026**

The Press Release Service extends QWR from article generation into professional press release distribution. Supporter-partners can request voice-matched, intelligence-informed, GEO-optimized press releases distributed to 500+ media outlets via Press Ranger Gold tier, with full impact tracking through Content Performance Intelligence.

### How It Works

```
SUPPORTER REQUEST (/press-releases/new)
  └── Topic + context + optional talking points
         │
         ▼
AI GENERATION (qwr_press_release_generator.py)
  ├── AP-style structure (inverted pyramid, dateline, boilerplate)
  ├── Voice matching (supporter's voice profile)
  ├── SEO optimization (keyword placement)
  ├── GEO optimization (extractable claims, citation-friendly)
  └── Stored as articles.content_type = 'press_release'
         │
         ▼
PR SCORING (qwr_pr_readiness_scorer.py)
  ├── Newsworthiness (0-100)
  ├── Headline Quality (0-100)
  ├── Quote Quality (0-100)
  ├── Structure (0-100)
  └── Overall Readiness (0-100)
         │
         ▼
DISTRIBUTION (human-in-the-loop via Press Ranger)
  ├── PR Distribution Alert workflow checks every 5 min
  ├── distribution_status: 'ready' → Discord alert to operator
  ├── Operator submits to Press Ranger → marks 'distributed'
  └── Gold tier: 500+ outlets (Bloomberg, AP, Yahoo Finance, AIWire, etc.)
         │
         ▼
IMPACT TRACKING (Content Performance Intelligence)
  ├── SERP position tracking (weekly)
  ├── AI citation monitoring (bi-monthly)
  └── Performance dashboard integration
```

### Bundle Pricing (All Tiers)

| Purchase | Per Release | Total | QWF Margin |
|----------|-----------|-------|-----------|
| 1 release | $799 | $799 | $399 (100%) |
| 3-pack | $699 | $2,097 | $299 (75%) |
| 6-pack | $649 | $3,894 | $249 (62%) |
| 12-pack | $599 | $7,188 | $199 (50%) |

Credits are per-account (not per-brand), never expire, and are consumed FIFO from the oldest bundle.

### Components

| Component | Type | Status |
|-----------|------|--------|
| `qwr_press_release_generator.py` | Python script | Built — Claude FLAGSHIP, AP-style + voice matching + SEO/GEO |
| `qwr_pr_readiness_scorer.py` | Python script | Built — 5-dimension scoring |
| PR Generation webhook | n8n `DugxqzUd2Eogdvg7` | Deployed — `/webhook/qwr-press-release` |
| PR Distribution Alert | n8n `vQFSORoJR3QHuH3O` | Deployed — every 5 min check for ready PRs |
| Stripe Webhook v1.2 | n8n `Lgj4TMhbMbZyPTrO` | Deployed — credit provisioning branch |
| Checkout edge function | Supabase | Updated — one-time payment mode for credit bundles |
| 4 Stripe bundle products | Stripe (LIVE) | Active — single, 3-pack, 6-pack, 12-pack |
| Press Release UI | Lovable prompt | Executed — list, request, detail, credits, dashboard card |
| Landing Page v2.0.0 | Lovable prompt | Executed — "Your Story. On Bloomberg." spotlight with pricing |

### Database Changes

| Change | Details |
|--------|---------|
| `articles.content_type` | TEXT DEFAULT 'article' CHECK IN ('article', 'press_release') |
| `articles.pr_metadata` | JSONB — headline, dateline, distribution_status, pr_score, readiness_checklist |
| `press_release_credits` table | Per-supporter credit tracking with FIFO consumption |
| `get_pr_credits_remaining(UUID)` | Returns remaining credit count |
| `use_pr_credit(UUID)` | FIFO deduction from oldest bundle |

### Distribution Network

Press Ranger Gold tier provides access to 500+ outlets including:
- **Tier 1:** Bloomberg, Associated Press, Yahoo Finance
- **Industry:** AIWire, Blockchain News, MarketWatch
- **Consumer:** Google News, Apple News, Business Insider
- **Full list:** Varies per release based on industry targeting

### Current State (February 14, 2026)

| Layer | Status |
|-------|--------|
| Backend (Python scripts) | Fully deployed |
| Database (Supabase) | Migration complete |
| Workflows (n8n) | 2 workflows active |
| Payments (Stripe) | LIVE — 4 bundle products |
| Frontend (Lovable) | Prompts executed |
| Distribution | Human-in-the-loop (Phase 2 will add API automation) |

### Reference

- **System Status:** `002 Projects/_QWR Quietly Writing App/QWR-System-Status.md` → Press Release Service section
- **Directive:** `005 Operations/Directives/qwr_press_release_service.md`

### 🎓 Missing Pixel Training Opportunities

| Component | Skills Developed | Difficulty |
|-----------|------------------|------------|
| AP-style press release structure | Technical writing, journalism standards | ⭐⭐ |
| Stripe one-time payment integration | Payment APIs, checkout flows, credit systems | ⭐⭐⭐ |
| n8n webhook + distribution alert pattern | Event-driven architecture, polling workflows | ⭐⭐ |
| FIFO credit system (SQL functions) | Database functions, transactional logic | ⭐⭐⭐ |
| GEO optimization for AI citations | Emerging SEO, structured content | ⭐⭐ |

---

## Cost Intelligence System ⭐ NEW

**Added: February 16, 2026**

A unified cost tracking and budget intelligence system providing real-time visibility into all QWF operating costs with app-level attribution, billing channel separation, and proactive budget alerting. As a nonprofit pursuing 100% financial self-sufficiency, every dollar of cost visibility directly impacts sustainability calculations.

### Architecture Overview

```
COST SOURCES (7 variable sources)
  ├── LLM APIs (~$90/mo)
  │     ├── OpenRouter ($5/$25 per MTok for Opus 4.6)
  │     └── Anthropic Direct ($15/$75 per MTok — Ezer edge function)
  ├── Apify (~$45/mo) → collect_apify_costs.py
  ├── Azure VMs (~$150/mo) → azure_costs.py
  ├── Supabase (~$85/mo) → collect_app_metrics.py
  ├── ESP VPS ($3/mo) → hardcoded
  ├── Betterstack ($0/mo) → lifetime license
  └── Email ($0/mo) → included in M365/SES
         │
         ▼
COLLECTION LAYER
  ├── model_config.py → llm_usage.jsonl (per-call, real-time)
  ├── collect_app_metrics.py → hq_app_metrics (daily, per-app)
  ├── collect_apify_costs.py → summary dict (on-demand/daily)
  ├── azure_costs.py → Azure Cost Management API (daily)
  └── summarize_session.py → integrates all sources into daily digest
         │
         ▼
VALIDATION & ALERTING
  ├── validate_llm_costs.py → 7-check validation suite
  ├── check_budget_alerts.py → threshold monitoring → Discord #system-status
  └── OpenRouter Activity API → cross-validation (96% coverage confirmed)
         │
         ▼
OUTPUT SURFACES
  ├── Digital Twin → twin.quietlyworking.org Operating Costs section (v2.4)
  ├── Discord #daily-digest → cost summary in session digest
  ├── Discord #system-status → budget alerts on threshold breach
  ├── HQ App Observatory → per-app sustainability dashboard
  └── CLI → model_config.py --usage, azure_costs.py, collect_apify_costs.py
```

### Cost Sources

| Source | Monthly Cost | Collection Method | Granularity |
|--------|-------------|-------------------|-------------|
| Azure VMs | ~$150 | `azure_costs.py` via Cost Management API | Per-resource, daily |
| LLM APIs (OpenRouter) | ~$90 | `model_config.py` logs to `llm_usage.jsonl` | Per-call, per-model, per-app |
| Supabase | ~$85 | `collect_app_metrics.py` (tier-based) | Per-app, per-tier |
| Apify | ~$45 | `collect_apify_costs.py` via REST API | Per-actor, per-run, per-day |
| ESP VPS | ~$3 | Hardcoded ($35.49/year) | Fixed |
| Cloudflare Pages | $0 | Free tier (unlimited bandwidth) | Per-project |
| Betterstack | $0 | Lifetime AppSumo (2 stacked codes): 200 monitors, 10 status pages, 5 members | N/A |
| Email (Graph/SES) | $0 | Included in existing licenses | N/A |
| **Total** | **~$373/mo** | | |

**Cost Optimization Note (March 2026):** QWR frontend hosting migrated from Lovable ($320/yr per project on Pro plan) to Cloudflare Pages (free tier, unlimited bandwidth). As additional apps migrate, each saves ~$320/yr in Lovable hosting costs. Lovable remains the build tool (AI-assisted UI development via prompts) but is no longer required for hosting.

### Supabase Pricing Model

The Supabase cost is computed dynamically, not hardcoded per-app:

| Component | Monthly Cost | Notes |
|-----------|-------------|-------|
| Org base (Pro) | $25.00 | Single "Quietly Working" org |
| Compute credit | -$10.00 | Included in Pro plan |
| 6x MICRO projects | $60.00 | QQT, QMP, QSP, QNT, QKN, Pocket Ez ($10 each) |
| 2x NANO projects | $10.00 | QWR, HQ ($5 each) |
| **Total** | **$85.00** | |

Helper function `_app_monthly_cost()` in `collect_app_metrics.py` computes per-app cost:
`(base_org_cost - compute_credit) / total_apps + compute_tier_cost`

### Billing Channels (Critical)

Two billing channels for LLM costs with **3x pricing difference** for the same model:

| Channel | Provider | Opus 4.6 Input | Opus 4.6 Output | Used By |
|---------|----------|----------------|-----------------|---------|
| `openrouter` | OpenRouter | $5/MTok | $25/MTok | All backoffice scripts via `model_config.py` |
| `anthropic_direct` | Anthropic API | $15/MTok | $75/MTok | Ezer edge function (Supabase) |

Every LLM usage log entry includes `billing_channel` to ensure correct cost attribution.

### App-Level Cost Attribution

`model_config.py` v2.1.0 maps 40+ scripts to app codes via `SCRIPT_APP_MAP` and 55+ scripts to 13 business purposes via `SCRIPT_PURPOSE_MAP`:

| App Code | Scripts | Description |
|----------|---------|-------------|
| `bni` | Meeting followups, visitor pipeline, enrichment scripts | Aim High BNI operations |
| `hq` | Audit, briefing, capture, entity management, summarization | HQ Command Center + backoffice |
| `qwr` | Content pipeline, press releases, citation tracking | Quietly Writing |
| `qnt` | Visitor pipeline, meeting pipeline, newsletter pipeline | Quietly Networking |
| `pocket_ez` | Pocket Ez edge functions | Pocket Ez companion app |
| `qrp` | Property management scripts | Quietly Renting Property |
| `ops` | Budget alerts, cost collection | Infrastructure operations |
| `backoffice` | Default for unmapped scripts | General backoffice operations |

### Purpose-Level Attribution (v2.1.0)

Purpose attribution answers "value vs waste" at the business-function level — more actionable than app-code alone. Every LLM call is tagged with a `purpose` field in `llm_usage.jsonl`.

| Purpose | Label | Example Scripts |
|---------|-------|-----------------|
| `email_processing` | Email Processing | outlook_pipeline, email_classify, email_entity_resolve |
| `bni_relationships` | BNI & Relationships | meeting_followup, bni_visitor_pipeline, meeting_prep |
| `qwr_content` | QWR Content | qwr_article_generator, qwr_citation_tracker, press releases |
| `meeting_intel` | Meeting Intelligence | zoom_pipeline, meeting_update_vault |
| `wisdom_knowledge` | Wisdom & Knowledge | wisdom_indexer, generate_wisdom_capture |
| `content_social` | Content & Social | content_pipeline_supervisor, social media scripts |
| `hq_inbox` | HQ Inbox Processing | process_inbox, master_capture |
| `pocket_ez_chat` | Pocket Ez Chat | pocket_ez edge function |
| `ops_admin` | Ops & Admin | audit_system, summarize_session |
| `ops_intelligence` | Ops Intelligence | auto_remediate_server, vm health |
| `lead_enrichment` | Lead Enrichment | enrich_names_ai, lead generation |
| `mission_intel` | Mission Intelligence | expert tracking, voice profiles |
| `izm_capture` | TIG Izm Capture | capture_tig_izm |

CLI: `python model_config.py --usage --days 30` shows breakdowns by model, tier, app, purpose, and billing channel.

### Cost Attribution Report

`report_llm_costs.py` v1.0.0 provides a full cost dashboard:

```bash
python report_llm_costs.py              # Last 30 days
python report_llm_costs.py --days 7     # Last 7 days
python report_llm_costs.py --current-month  # Current calendar month
python report_llm_costs.py --all        # All time
python report_llm_costs.py --json       # JSON output for Discord/dashboards
```

Report sections: Total Summary, By Purpose (primary), By Tier, Top 10 Scripts, Weekly Trend (with bars), Monthly Totals, By App, Blind Spots reminder.

### Email Pipeline Cost Optimization

The email pipeline is the largest LLM cost driver (~44% of total spend). Optimization strategy:

1. **Suppression pre-check** (v1.5.0→v1.6.0): `outlook_pipeline.py` loads `hq_email_suppressions` table BEFORE classification. Suppressed senders/domains get a synthetic `classification: "suppressed"` and skip Opus entirely (~$0.036/email saved). As of March 2026: **82% suppression rate** (1,153/1,413 emails skipped), reducing email processing costs from $1.17/day (Feb) to $0.22/day (Mar) — **81% reduction**. v1.6.0 also tracks all senders in `hq_email_senders` Supabase table for the HQ Email Sources module.
2. **Newsletter short-circuit**: `email_classify.py` skips Opus for pre-detected newsletters.
3. **Active unsubscribing**: User progressively reduces inbox volume by unsubscribing from non-essential emails.
4. **Task creation safety net**: `email_task_create.py` Rule 0 blocks task creation for suppressed emails (defense in depth).

### Budget Alerting

`check_budget_alerts.py` runs daily via n8n cron. Zero-dependency design (stdlib only) ensures it works even when pip packages are broken.

| Budget | Monthly Limit | Warn At (75%) | Critical At (90%) | Daily Anomaly |
|--------|-------------|---------------|-------------------|---------------|
| LLM (OpenRouter) | $150 | $112.50 | $135 | $15/day |
| Apify | $75 | $56.25 | $67.50 | $10/day |
| Total Variable | $400 | $300 | $360 | — |

Features: MTD spend tracking, end-of-month projection, daily anomaly detection, Discord `#system-status` alerts.

### Cost Validation

`validate_llm_costs.py` runs 7 validation checks:

1. **Parse integrity** — Counts unparseable log lines
2. **Zero-cost anomalies** — Flags $0 calls on non-FAST tiers
3. **Cost spike detection** — Single calls exceeding $1.00
4. **Daily trend analysis** — Flags days 3x above average
5. **Billing channel consistency** — Verifies rates match expected ranges per channel
6. **App attribution coverage** — Reports explicit vs derived app codes
7. **OpenRouter Activity API cross-validation** — Compares local totals against API (requires `OPENROUTER_MGMT_KEY`)

Cross-validation result: **96% coverage** ($88.62 local vs $92.47 API over 30 days). The 4% gap represents calls outside `model_config.py` (other API keys, direct usage).

### Components

| Script | Version | Purpose |
|--------|---------|---------|
| `model_config.py` | v2.1.0 | LLM cost logging with app/purpose/channel attribution |
| `report_llm_costs.py` | v1.0.0 | Full cost attribution dashboard (purpose/app/tier/trend) |
| `collect_app_metrics.py` | v1.2.0 | Per-app Supabase + shared infra cost collection |
| `collect_apify_costs.py` | v1.0.0 | Apify per-actor, per-run cost breakdown |
| `validate_llm_costs.py` | v1.1.0 | 7-check LLM cost validation suite (pricing ranges from cost_constants) |
| `check_budget_alerts.py` | v1.0.0 | Zero-dep budget threshold monitoring |
| `azure_costs.py` | v1.2.0 | Azure VM cost collection (MTD always queries full month) |
| `summarize_session.py` | — | Integrates Apify costs into daily digest |

### Key Files

| File | Location | Purpose |
|------|----------|---------|
| LLM usage log | `005 Operations/Data/llm_usage.jsonl` | Per-call LLM cost records (moved from `.tmp/`) |
| Cost tracking directive | `005 Operations/Directives/cost_tracking.md` | Full SOP with edge cases and changelog |
| Cost constants (SSoT) | `005 Operations/Execution/cost_constants.py` | Single source of truth for all cost figures (v1.1.0) |
| Budget config | `check_budget_alerts.py` `BUDGETS` dict | Threshold definitions |
| HQ Observatory schema | `hq_observatory_schema.sql` | Supabase tables for app metrics |

### Digital Twin Cost Transparency (v2.4)

As of v2.4, the Digital Twin at `twin.quietlyworking.org` displays a full Operating Costs section — publicly visible, following QWF's "Show don't Tell" transparency value. The server's `/api/costs` endpoint aggregates all 7 cost sources with TTL-based caching.

**What's displayed publicly:**
- Monthly burn total with per-source breakdown (LLM, Azure, Supabase, Apify, ESP)
- Variable budget progress bar ($400/mo target) with day-of-month context and month-end projection
- LLM Intelligence panel: tier cards (Flagship/Standard/Fast/Image), top scripts by cost
- Infrastructure panel: Azure MTD, Supabase ($85), ESP ($2.96), Betterstack (Free), Email (Free)

**What's excluded (security):** No API keys, server IPs, `.env` variable names, Supabase project IDs, credential names, user emails, or full file paths.

**Caching strategy:**

| Source | Cache TTL | Why |
|--------|-----------|-----|
| LLM JSONL aggregation | 5 min | ~100ms parse of ~7K lines; avoids re-parse on 60s polling |
| Azure costs (SQLite) | 5 min | Batched with LLM cache |
| Apify (API calls) | 30 min | Network-bound (5-15s per call); stale OK |
| Fixed costs | 5 min | Hardcoded values, negligible |

### Training Opportunities

| Component | Skills Developed | Difficulty |
|-----------|------------------|------------|
| API cost cross-validation | REST APIs, data reconciliation, coverage analysis | ⭐⭐⭐ |
| Budget alerting (zero-dep) | Python stdlib, Discord webhooks, projection math | ⭐⭐ |
| App-level attribution architecture | Dictionary mapping, log enrichment, CLI analytics | ⭐⭐ |
| Purpose-level attribution (v2.1.0) | Multi-dimensional analysis, defaultdict aggregation, business-function mapping | ⭐⭐⭐ |
| Cost attribution report (report_llm_costs.py) | JSONL parsing, formatted output tables, trend visualization, CLI arg parsing | ⭐⭐ |
| Suppression-before-classification optimization | Defense-in-depth, cost-aware pipeline design, synthetic classification patterns | ⭐⭐⭐ |
| Billing channel separation | Multi-channel pricing, rate card validation | ⭐⭐ |
| Supabase tier-based costing | Dynamic pricing models, per-app allocation | ⭐⭐ |

---

## QWR Reverse Benchmarking Intelligence ⭐ NEW

**Added: February 18, 2026**

Reverse Benchmarking Intelligence studies what competitors are terrible at instead of copying their strengths (Rory Sutherland's concept). It uses two intelligence sources — competitor reviews (G2, Trustpilot, Capterra) and Reddit research (subreddit pain points + customer language) — to produce scored gap opportunities that feed directly into article generation.

### Architecture

```
REVIEW SOURCES (per competitor per brand)
  └── qwr_review_scraper.py → competitor_reviews table
       └── qwr_review_analyzer.py → review_analysis table

REDDIT SOURCES (per subreddit per brand)
  └── qwr_reddit_scraper.py (PRAW) → reddit_posts table
       └── qwr_reddit_analyzer.py → reddit_analysis table

CROSS-REFERENCE
  └── qwr_gap_opportunity_generator.py → gap_opportunities table (scored 0-100)
       └── Article Gen v6.0 (gap context + customer language injected)
```

### Two-Source Intelligence Model

| Source | What It Captures | Method |
|--------|-----------------|--------|
| Competitor Reviews (G2, Trustpilot, Capterra) | Strengths, weaknesses, feature gaps, pricing complaints | Apify scraping → Claude FLAGSHIP analysis |
| Reddit (subreddit monitoring) | Pain points, unmet needs, customer language (terms, phrases, questions) | PRAW API → Claude FLAGSHIP analysis |

The power is in the cross-reference: when competitor reviews say "reporting is weak" AND Reddit users complain about "spending hours building reports manually," that's a high-confidence gap opportunity with real customer language to inject into articles.

### Components

| Component | Type | Status |
|-----------|------|--------|
| SQL Migration (7 tables) | Supabase | Deployed |
| `qwr_review_scraper.py` | Python script | Built — G2, Trustpilot, Capterra via Apify |
| `qwr_review_analyzer.py` | Python script | Built — Claude FLAGSHIP with thinking |
| `qwr_reddit_scraper.py` | Python script | Built — PRAW-based subreddit scraping |
| `qwr_reddit_analyzer.py` | Python script | Built — pain points, unmet needs, customer language |
| `qwr_gap_opportunity_generator.py` v2.0.0 | Python script | Built — cross-references sources → scored gaps + content strategy matching (`suggested_strategy_id`) |
| `qwr_competitor_intel.py` v2.0.0 | Extended | Added review scraping trigger |
| `qwr_opportunity_scorer.py` v2.0.0 | Extended | Added gap opportunity scoring |
| `qwr_update_article_gen_workflow.py` v3.0.0 | Extended | Article gen v5.0 → v8.0 (content strategy + quality targets) |
| `qwr_fix_citation_pipeline.py` v1.0.0 | Built | Citation URL extraction, quality scorer fix, inline attribution |
| n8n: Review Scraping + Analysis | Workflow `q9D0RU8D7eBCmq34` | Deployed — scheduled |
| n8n: Reddit Scraping + Analysis | Workflow `DSv69vT6GfXzY6IS` | Deployed — scheduled |
| n8n: Gap Opportunity Generator | Workflow `aEj51qiTeZl9C4tL` | Deployed — scheduled |
| n8n: Subreddit Discovery Webhook | Workflow `wC2Yly51PIPd7Rkh` | Deployed — `/webhook/qwr-subreddit-discovery` |
| Lovable: Source Setup UI (054) | Frontend | Executed |
| Lovable: Intelligence Dashboard (055) | Frontend | Executed |
| Lovable: Gap Opportunity Detail (056) | Frontend | Executed |
| Lovable: Landing Page Update (057) | Frontend | Executed |

### Database Tables

| Table | Purpose |
|-------|---------|
| `review_sources` | Competitor review source configs (platform, URL, competitor name) |
| `competitor_reviews` | Raw scraped reviews (rating, text, reviewer, date) |
| `reddit_sources` | Subreddit monitoring configs per brand |
| `reddit_posts` | Raw scraped Reddit posts/comments |
| `review_analysis` | Claude analysis output (strengths, weaknesses, gaps as JSONB) |
| `reddit_analysis` | Claude analysis output (pain_points, unmet_needs, customer_language as JSONB) |
| `gap_opportunities` | Scored content gaps (title, gap_type, score 0-100, source_evidence, suggested_angles, suggested_strategy_id) |

### Article Gen v6.0 Integration

The article generation workflow now includes:
- **"Write About This Gap" flow:** When `gap_opportunity_id` is in the webhook body, fetches the full gap with evidence and injects it as the article's primary angle
- **Standard article flow:** Keyword-matches against active gaps (score >= 40) and surfaces relevant opportunities
- **Customer language injection:** Fetches Reddit-derived common_terms, power_phrases, questions_asked, frustration_phrases, and praise_phrases — articles use the exact words real customers use
- **Post-generation update:** PATCHes gap status to `article_generated` after successful generation

### Dependencies

| Dependency | Status | Notes |
|------------|--------|-------|
| PRAW 7.8.1 | Installed | `pip install praw` — in requirements.txt |
| Reddit API credentials | **PENDING** | User creating app at reddit.com/prefs/apps → `REDDIT_CLIENT_ID`, `REDDIT_CLIENT_SECRET`, `REDDIT_USER_AGENT` in `.env` |

### Gap Scoring

Each gap opportunity is scored 0-100 based on:
- **Review evidence strength** — How many reviews mention this weakness, across how many platforms
- **Reddit evidence strength** — How many independent pain point mentions in relevant subreddits
- **Cross-source correlation** — Higher score when both sources identify the same gap
- **Content viability** — Is this gap something an article can actually address?

Gaps scoring 40+ are surfaced to article generation. Gaps scoring 70+ trigger Discord alerts as high-value content opportunities.

### Reference

- **Directive:** `005 Operations/Directives/qwr_reverse_benchmarking.md`
- **System Status:** `002 Projects/_QWR Quietly Writing App/QWR-System-Status.md` → Reverse Benchmarking Intelligence section

### Missing Pixel Training Opportunities

| Component | Skills Developed | Difficulty |
|-----------|------------------|------------|
| Apify review scraping (multi-platform) | Web scraping, API integration, data normalization | ⭐⭐ |
| PRAW Reddit API | OAuth, API wrappers, rate limiting | ⭐⭐ |
| Claude FLAGSHIP analysis with thinking | LLM prompt engineering, structured output extraction | ⭐⭐⭐ |
| Cross-source gap scoring | Multi-signal scoring algorithms, evidence weighting | ⭐⭐⭐ |
| Customer language injection into AI content | NLP concepts, voice matching, authenticity engineering | ⭐⭐⭐ |
| n8n scheduled pipeline orchestration | Workflow automation, SSH execution, error handling | ⭐⭐ |

---

## QWR Content Strategy System ⭐ NEW

**Added: February 26, 2026**

The Content Strategy System adds strategy-aware article generation to QWR. Supporters define named content strategies (e.g., "LinkedIn Thought Leadership for CMOs") that combine a target persona, platform, expertise level, and style guide. The article generation pipeline uses this context to produce platform-optimized content.

### Architecture

```
STRATEGY CREATION (Frontend)
  └── /brands → Strategy Settings tab
       └── Create strategy: name, goal, persona_id, platform, expertise, style_guide
            └── content_strategies table (Supabase)

GAP → STRATEGY MATCHING
  └── qwr_gap_opportunity_generator.py v2.0
       └── Cross-references gap_opportunities with content_strategies
       └── Sets suggested_strategy_id on gaps that match a strategy's persona/platform

ARTICLE GENERATION (v6.0)
  └── If content_strategy_id in webhook body:
       └── Fetches strategy + target persona + platform rules
       └── Generates platform-optimized article
```

### Components

| Component | Type | Status |
|-----------|------|--------|
| `content_strategies` table | Supabase | Deployed — stores strategy configs per brand |
| `qwr_gap_opportunity_generator.py` v2.0.0 | Python script | Built — adds `suggested_strategy_id` to matching gaps |
| Article Gen v6.0 | n8n workflow `7NxSNqAg6aY97ZXl` | Deployed — reads strategy context for generation |
| Lovable: Strategy Settings (065) | Frontend | Executed — CRUD for content strategies |
| Lovable: Landing Page v3.0 (066) | Frontend | Executed — updated landing page with Content Strategy messaging |

### Database Tables

| Table | Purpose |
|-------|---------|
| `content_strategies` | Strategy configs: name, goal, persona_id, platform, expertise_level, style_guide, brand_id |
| `gap_opportunities.suggested_strategy_id` | FK to content_strategies — set by gap generator when a gap matches a strategy |

### Content Strategy Fields

| Field | Purpose | Example |
|-------|---------|---------|
| `name` | Human-readable strategy name | "LinkedIn Thought Leadership for CMOs" |
| `goal` | What the strategy achieves | "Establish authority in marketing automation" |
| `persona_id` | Target persona (FK) | Links to `personas` table |
| `platform` | Target platform | `linkedin`, `blog`, `twitter`, `newsletter` |
| `expertise_level` | Content depth | `beginner`, `intermediate`, `expert` |
| `style_guide` | Writing style notes | "Conversational but authoritative, use data" |

### Reference

- **System Status:** `002 Projects/_QWR Quietly Writing App/QWR-System-Status.md` → Content Strategy section
- **Development Plan:** `002 Projects/_QWR Quietly Writing App/QWR-Content-Strategy-Development-Plan.md`

---

## QWR Preparation Workbook ⭐ NEW

**Added: February 26, 2026**

The Preparation Workbook is an interactive, AI-guided pre-signup experience at `/prepare`. Visitors build their content strategy through a 6-chapter conversational journey — without creating an account. This replaces the traditional "sign up and figure it out" onboarding with a value-first approach.

### Architecture

```
VISITOR (no auth required)
  └── /prepare route
       └── 6 chapters, sequential progression
            ├── Ch 1: Brand Discovery (AI conversation)
            ├── Ch 2: Voice Discovery (URL input + AI conversation)
            ├── Ch 3: Audience Discovery (AI conversation)
            ├── Ch 4: Platform Selection (grid, no AI)
            ├── Ch 5: Strategy Builder (AI conversation)
            └── Ch 6: Review & Export (summary + PDF + signup CTA)

BACKEND
  └── n8n webhook (POST /qwr-workbook)
       └── SSH to backoffice VM
            └── qwr_workbook_engine.py
                 └── workbook_sessions table (Supabase, anon RLS)

POST-SIGNUP IMPORT
  └── /signup?workbook={session_id}
       └── import-workbook edge function (--no-verify-jwt)
            └── Creates brand, personas, content_strategies from workbook seeds
```

### Components

| Component | Type | Status |
|-----------|------|--------|
| `workbook_sessions` table | Supabase | Deployed — anon RLS policies for public access |
| `qwr_workbook_engine.py` v1.0.0 | Python script | Built — 4 AI chapter types, 7 commands, magic link resume |
| n8n: Workbook Webhook | Workflow `8S3sUIaYvJXhdzPg` | Deployed — `/webhook/qwr-workbook` |
| Lovable: Preparation Workbook (067) | Frontend | Executed — `/prepare` route with chat UI |
| `import-workbook` | Supabase Edge Function | Deployed — converts workbook seeds to full records |

### Database: workbook_sessions

| Column | Type | Purpose |
|--------|------|---------|
| `id` | UUID (PK) | Session identifier |
| `email` | text | Optional — for save-and-resume |
| `supporter_id` | UUID (FK) | Set after signup/import |
| `status` | text | `active`, `completed`, `imported`, `abandoned` |
| `current_chapter` | int | 1-6 progress tracker |
| `chapters_completed` | int[] | Array of completed chapter numbers |
| `chapter_data` | JSONB | Per-chapter metadata (phases, message counts) |
| `brand_seed` | JSONB | Extracted: company, industry, differentiators, positioning |
| `voice_seed` | JSONB | Extracted: core attributes, tone spectrum, A/B choices |
| `persona_seeds` | JSONB | Extracted: array of personas with demographics, pain points, goals |
| `platform_selections` | JSONB | User-selected platforms (up to 12 options) |
| `strategy_seeds` | JSONB | Extracted: strategies linking persona + platform + expertise |
| `conversation_histories` | JSONB | Per-chapter message arrays |
| `magic_link_token` | text | 30-day token for cross-device resume |
| `magic_link_expires_at` | timestamptz | Token expiry |
| `imported_at` | timestamptz | When workbook was imported post-signup |

### AI Conversation Flow

Each AI chapter (1, 2, 3, 5) follows a 3-phase progressive methodology:

1. **Discovery** — Open-ended questions to understand the visitor's situation
2. **Clarification** — Targeted follow-ups based on extracted data gaps
3. **Documentation** — Summary and confirmation of what was captured

Phase transitions are configurable per chapter with `min_questions` and `min_completeness` thresholds. Every 4 messages (or on phase change), Claude STANDARD extracts structured data from the conversation into the chapter's seed field.

### Context Threading

Each chapter builds on previous chapters:
- Chapter 2 (Voice) receives brand context from Chapter 1
- Chapter 3 (Audience) receives brand + voice context
- Chapter 5 (Strategy) receives brand + voice + persona + platform context

### Save and Resume

- **Magic link:** Visitor enters email → receives a token → can resume on any device within 30 days
- **No auth required:** The workbook operates entirely on anon RLS policies
- **Session ID:** Used as de facto access control (UUID is unguessable)

### Post-Signup Import

When a visitor signs up with `?workbook={session_id}`:
1. Edge function `import-workbook` reads the workbook session
2. Creates `brands` record from `brand_seed`
3. Creates `personas` records from `persona_seeds`
4. Creates `content_strategies` from `strategy_seeds`
5. Sets `supporter_id` and `imported_at` on the workbook session

### Reference

- **System Status:** `002 Projects/_QWR Quietly Writing App/QWR-System-Status.md`
- **Development Plan:** `002 Projects/_QWR Quietly Writing App/QWR-Content-Strategy-Development-Plan.md` (Phase 4)
- **Prompt:** `002 Projects/_QWR Quietly Writing App/067-lovable-prompt-preparation-workbook.md`

### 🎓 Missing Pixel Training Opportunities

| Component | Skills Developed | Difficulty |
|-----------|------------------|------------|
| Conversational AI with phase transitions | LLM prompt engineering, state machines, progressive extraction | ⭐⭐⭐ |
| Anon RLS policies for public features | Supabase auth model, Row Level Security, access control patterns | ⭐⭐ |
| Magic link authentication pattern | Token generation, expiry management, cross-device UX | ⭐⭐ |
| Chat UI with typing indicators | React state management, WebSocket-like UX patterns, auto-scroll | ⭐⭐ |
| Post-signup data import flow | Edge functions, data transformation, multi-table inserts | ⭐⭐⭐ |

---

## QWF Ecosystem Landing Section ⭐ NEW

**Added: February 18, 2026**

Every QWF app landing page includes a standardized "Part of Something Bigger" section that introduces the full Quietly Working universe. Visitors to any single app discover it's part of a connected ecosystem with a free command center (Quietly Spotting) and seamless cross-app authentication (QWF Passport).

### What It Contains

- **v2.0 (March 2026): Interactive SVG Orbit + 9 Cards** — replaced flat card grid with animated hub-and-spoke visualization. QSP always center node. Current app at 12 o'clock. Traveling dots along connection lines. Auto-cycle spotlight (stops on any interaction). Bidirectional hover/click linking between orbit nodes and cards. Mobile fallback: vertical hub-list.
- **9 items:** Quietly Spotting (FREE), Quietly Writing, Quietly Quoting (IN PRODUCTION), Quietly Tracking (IN PRODUCTION), Quietly Networking, Quietly Knocking, Quietly Managing (IN PRODUCTION), QWF Passport (ONE ACCOUNT), Your Tools (CONNECT, dashed border)
- **Canonical icons** (match QSP sidebar): Telescope, Feather, Calculator, Link2, Handshake, DoorOpen, Home, Fingerprint, Plug
- **Mission footer:** "Every penny of proceeds from QWF apps supports underserved youth through The Missing Pixel Project."
- **Current app highlight:** "You are here" label above current app's orbit node + badge on card
- **Cascade generator:** `005 Operations/Execution/generate_ecosystem_cascade.py` v2.1.0 produces per-app prompts (6 apps). QWR and Pocket Ez are manual.

### Locked Copy (Must Not Change)

- Section heading: "Part of Something Bigger"
- Section subtitle: "Every QWF tool stands on its own. Together? They're something else entirely."
- QSP badge: "FREE"
- Passport tagline: "One login. Every app. Zero friction."
- Mission text: "Every penny of proceeds from QWF apps supports underserved youth through The Missing Pixel Project."

### Implementation Status

| App | Status | Notes |
|-----|--------|-------|
| QSP (Quietly Spotting) | ✅ Orbit v2 Deployed | Prompts 016-022: orbit + refinements + crosshair favicon + telescope navbar + orbit hero (Mar 8) |
| QWR (Quietly Writing) | ✅ Orbit v2 Deployed | Prompt 091: manual orbit prompt with ref-based stopCycle (Mar 8) |
| QQT (Quietly Quoting) | ✅ Orbit v2 Deployed | Prompt 015: cascade orbit (Mar 8) |
| QNT (Quietly Networking) | ✅ Orbit v2 Deployed | Prompt 049: cascade orbit (Mar 8) |
| QTR (Quietly Tracking) | ✅ Orbit v2 Deployed | Prompt 009: cascade orbit (Mar 8) |
| QKN (Quietly Knocking) | ✅ Orbit v2 Deployed | Prompt 005: cascade orbit (Mar 8) |
| QMP (Quietly Managing) | ✅ Orbit v2 Deployed | Prompt 011: cascade orbit (Mar 8) |
| Pocket Ez | ✅ Orbit v2 Deployed | Prompts 009-011: bioluminescent variant + navbar fix + alpha pill (Mar 8) |

### Reference

- **Directive:** `005 Operations/Directives/qwf_ecosystem_landing_section.md`
- **Standard:** `005 Operations/Directives/qwf_app_family_standard.md` → Section 6 (Landing Page Standards)

---

## Auto-Remediation System ⭐ NEW

### Overview

Automatically diagnoses and remediates server outages detected by Betterstack, using Claude Opus with extended thinking to analyze issues and execute safe, predefined recovery actions. Target: resolve common outages in under 60 seconds without human intervention.

**Origin:** A WPMU outage on 2026-02-23 had a 12-hour gap between Betterstack alert (overnight) and human response. The manual fix took ~60 seconds (MariaDB restart). This system automates that response.

### Architecture

```
Betterstack detects outage
    ↓
Outgoing Webhook (ID: 80218)
    ↓
n8n Webhook (/webhook/auto-remediation-alert)
    ↓
Parse Alert → Skip if resolved
    ↓
SSH to claude-dev (nohup fire-and-forget)
    ↓
auto_remediate_server.py
    ├── Map monitor to server playbook
    ├── Run diagnostics (SSH commands)
    ├── Claude Opus thinking_call() analysis
    ├── Execute remediation (if mode=remediate)
    ├── Verify health (HTTP check)
    └── Post Discord embed to #system-status
```

### Server Playbooks

Each monitored server has a playbook defining safe boundaries:

| Playbook | Server | Monitors | Diagnostic Commands | Approved Actions |
|----------|--------|----------|--------------------|-----------------|
| `wpmu` | qwu-wpmu (AWS Lightsail) | quietlyworking.org | Bitnami stack status, MariaDB process/socket, disk/memory, error logs | Restart stack, restart MariaDB/Apache/PHP-FPM, clear tmp |
| `n8n` | qwu-n8n (Azure VM) | n8n Workflow Engine | Docker containers, disk/memory, Docker logs, health endpoint, pg_isready | Restart n8n container, restart all containers, restart postgres, prune Docker |
| `claude-dev-service` | claude-dev (local) | Ezer SMS Gateway, Digital Twin, QNT Webhook | systemd status, journalctl, port listening, disk/memory | Restart service, restart Caddy |

Each playbook also has a **Never Do** list (e.g., never modify wp-config.php, never run `docker compose down`, never kill processes by PID).

### Safety Modes

| Mode | Behavior | Use Case |
|------|----------|----------|
| `diagnose` (default) | Runs diagnostics + AI analysis, posts findings to Discord. Does NOT execute remediation. | First 2 weeks of deployment (current) |
| `remediate` | Everything in diagnose + executes approved remediation actions. Max 2 attempts per incident. | After validation period |

### Key Components

| Component | Location | Notes |
|-----------|----------|-------|
| Script | `005 Operations/Execution/auto_remediate_server.py` v1.0.0 | ~950 lines, 3 playbooks |
| Directive | `005 Operations/Directives/auto_remediation.md` | Full SOP with playbooks |
| n8n Workflow | "Auto-Remediation - Betterstack Alert Handler" (<WORKFLOW_ID>) | Fire-and-forget SSH pattern |
| Workflow JSON | `005 Operations/Workflows/auto_remediation_webhook.json` | 6 nodes |
| Betterstack Webhook | Outgoing Webhook ID 80218 | Fires on incident_started, incident_resolved, incident_reopened |
| Logs | `.tmp/logs/auto_remediation.log` + `.tmp/logs/auto_remediation_runs.log` | Per-run + background execution logs |

### Manual Testing

```bash
# Diagnose-only for a specific monitor
python '005 Operations/Execution/auto_remediate_server.py' \
  --monitor-name "quietlyworking.org" --mode diagnose --json

# Dry-run remediation (shows what it would do)
python '005 Operations/Execution/auto_remediate_server.py' \
  --monitor-name "n8n Workflow Engine" --mode remediate --dry-run --json

# Simulate a webhook trigger
curl -X POST "https://n8n.quietlyworking.org/webhook/auto-remediation-alert" \
  -H "Content-Type: application/json" \
  -d '{"monitor": "quietlyworking.org", "type": "down"}'
```

### Deduplication

Lock files (`.tmp/auto_remediation_<monitor>.lock`) prevent concurrent remediation attempts for the same monitor. Locks auto-expire after 10 minutes.

### Lessons Learned During Build

1. **Claude wraps JSON in code fences** — Even with `json_mode=True`, `thinking_call()` responses may be wrapped in `` ```json `` code fences. Script strips these before parsing.
2. **SSH nohup for long-running LLM calls** — n8n SSH node must return immediately (webhook timeout). Use `nohup ... &` pattern with `echo` for immediate response.
3. **Full venv path in SSH** — Non-interactive SSH doesn't source `.bashrc`, so use `.venv/bin/python3` instead of `python`.
4. **n8n webhookId bug** — After `import:workflow`, verify `webhook_entity` table has correct `webhookId` value.

### Enabling Remediation Mode

When ready to switch from diagnose-only to active remediation:
1. In the n8n workflow SSH command, change `--mode diagnose` to `--mode remediate`
2. Redeploy the workflow using the standard n8n deployment process
3. Test with `--dry-run` first to verify action selection

### 🎓 Missing Pixel Training Opportunities

| Module | Skills | Tier | Prerequisites |
|--------|--------|------|---------------|
| **Server Diagnosis Lab** | SSH, Linux troubleshooting, MariaDB, Bitnami stack, systemd | Tier 2 (Contributor) | Basic Linux CLI |
| **Auto-Remediation Agent** | Python (subprocess, JSON, argparse), Claude API, webhook architecture, safety engineering | Tier 3 (Specialist) | Python intermediate, API experience |
| **n8n Webhook Workflow** | n8n workflow design, SSH nodes, Code nodes, conditional branching | Tier 2 (Contributor) | n8n basics |
| **Monitoring & Alerting** | Betterstack API, REST APIs, uptime monitoring concepts | Tier 1 (Explorer) | API basics |

**Portfolio project candidate:** Build a simplified auto-remediation agent for a single service (e.g., restart a Docker container when health check fails). Demonstrates AI agent development, DevOps patterns, and safety-first engineering.

---

## QTR Quietly Tracking ⭐ NEW

**Added: February 27, 2026**

Quietly Tracking (QTR) is a smart link + dynamic landing page + conversion attribution system. Create trackable links that resolve to beautiful, variable-driven landing pages. Track visits, conversions, and attribute results back to content strategies.

### Architecture

```
Lovable Frontend (quietlytracking.org)
    → Supabase SDK
        → Supabase (ipdrexcbaqoazhpohfco, us-west-1)
            ← Edge Functions (planned: render-landing-page, track-visit, track-conversion)
                ← n8n workflows (planned)
```

### Ecosystem Position

QTR is the attribution/conversion arm of the QWF product family:
- **QWR → QTR:** Articles auto-generate smart links with `content_response` templates for CTAs
- **QKN → QTR:** Outbound campaigns use QTR smart links for landing pages and conversion tracking
- **QTR → QSP:** Visit and conversion analytics push to SPOT dashboard
- **L4G → QTR:** Postcard QR codes resolve to `local_offer` template landing pages

### Smart Link Resolution Flow

```
User clicks link → quietlytracking.org/[slug]
  → Edge function: render-landing-page
    → Lookup slug in qtr_smart_links
    → Get template from qtr_link_templates
    → Interpolate: URL params → template variables → fallbacks
    → Record visit in qtr_page_visits
    → Return rendered HTML page
```

### Template Types (MVP — 6 pre-built)

| Type | Use Case |
|------|----------|
| `content_response` | Article → "Here's your next step" |
| `resource_download` | "Download the guide you read about" |
| `event_registration` | QR at event → registration form |
| `local_offer` | Postcard QR → business offer |
| `quote_followup` | Proposal link → accept/schedule |
| `contact_request` | General inquiry with context |

MVP uses client-side template definitions (`src/data/templates.ts`) rather than DB-seeded rows. Template type stored as `_template_type` in variables JSONB.

### Schema (v1.0.0)

7 tables: 3 QWF standard (`supporter_partners`, `contact_submissions`, `bug_reports`) + 4 QTR core:

| Table | Purpose |
|-------|---------|
| `qtr_link_templates` | Reusable page designs with variable placeholders |
| `qtr_smart_links` | Generated trackable links (template instances, slug-based) |
| `qtr_page_visits` | Page view analytics (fingerprint, referrer, UTM, geo) |
| `qtr_conversion_events` | Conversion tracking with attribution back to visits |

RLS: owner-only for templates/links, anonymous INSERT for visits/conversions/contacts.

### Pricing

| Tier | Monthly | Annual |
|------|---------|--------|
| Starter | $79/mo | $790/yr |
| Pro | $149/mo | $1,490/yr |
| Agency | $249/mo | $2,490/yr |

No free tier. 30-day trial. **QWF ecosystem bundle:** Full Pro access included free with any paying QWF app subscription.

### Current State (February 27, 2026)

| Component | Status |
|-----------|--------|
| Supabase project | ACTIVE_HEALTHY — `ipdrexcbaqoazhpohfco` (us-west-1) |
| Domain | `quietlytracking.org` — registered, DNS via Cloudflare |
| Lovable project | `a404ee32-52c7-4781-8411-974ed9bdbaf7` |
| Schema | v1.0.0 — 7 tables, RLS policies, indexes |
| Auth | Configured — email/password + Google OAuth (shared QWF client) |
| QWF Passport | Secret set, edge function pending |
| Lovable Prompts | 7 total (001-002, 006-007 executed; 003-005 written) |
| Edge functions | Not yet deployed (render-landing-page, track-visit, track-conversion, verify-crossover-token, submit-contact-form) |
| Landing page | Deployed — 14 sections, alpha gate, heritage, ecosystem, contact form |
| Accent color | Teal/Cyan (#06B6D4) |

### Lovable Prompts

| # | Name | Status |
|---|------|--------|
| 001 | Foundation + Auth + Onboarding | EXECUTED |
| 002 | Link Creator + Links Management | EXECUTED |
| 003 | Template Gallery | WRITTEN |
| 004 | Analytics Deep Dive | WRITTEN |
| 005 | Settings (Profile/Subscription/Brand) | WRITTEN |
| 006 | Alpha Stage (badge, bug reporter, landing page, contact form) | EXECUTED |
| 007 | Favicon + Site Meta | EXECUTED |

### Reference

- **GitHub Repo:** Lovable-managed (via project `a404ee32-52c7-4781-8411-974ed9bdbaf7`)
- **System Status:** `002 Projects/_Quietly Tracking/QTR-System-Status.md`
- **Development Plan:** `002 Projects/_Quietly Tracking/QTR-Development-Plan.md`
- **Lovable Prompts:** `002 Projects/_Quietly Tracking/lovable-prompts/001-007`

### 🎓 Missing Pixel Training Opportunities

| Component | Skills Developed | Difficulty |
|-----------|------------------|------------|
| Smart Link System Design | Database schema, slug resolution, variable interpolation, fallback chains | ⭐⭐⭐ |
| Template System | JSONB data modeling, dynamic HTML rendering, variable placeholders | ⭐⭐ |
| Conversion Attribution | Analytics pipeline, event tracking, funnel visualization | ⭐⭐⭐ |
| QR Code Integration | QR generation, print-to-digital bridge, campaign tracking | ⭐⭐ |
| Lovable Prompt Engineering | AI-assisted UI, iterative prompt design, component architecture | ⭐⭐ |

---

## QWF Ecosystem Widget ⭐ NEW

**Added: February 28, 2026**

A living, interactive visualization of the entire Quietly Working Universe — 50 entities across 7 categories, served as an embeddable widget with Shadow DOM isolation. One JavaScript file, 14.3 KB gzip, drops onto any QWF website.

### Architecture

```
WordPress Site (any of 11 QWF sites)
  → [qwf_ecosystem] shortcode
    → widget.js loader (0.48 KB)
      → widget.bundle.js (14.3 KB, Preact + Shadow DOM)
        → GET /api/ecosystem (Digital Twin, port 8767)
          → ecosystem_registry.json (50 entities)
          → live metrics (Supabase, Betterstack, supervisors)
```

### Two Display Modes

| Mode | Shortcode | Best For |
|------|-----------|----------|
| **Block** (compact) | `[qwf_ecosystem]` | Footers, sidebars, "about us" sections. Shows category rings → click to expand grid → click entity for detail panel. ~180px collapsed. |
| **Page** (full) | `[qwf_ecosystem mode="page"]` | Dedicated ecosystem page. Full-height with sidebar filters, search, categorized grid, all categories visible. |

### Entity Detail Panel

Expanding panel below clicked entity cards:
- **Left side:** Summary, highlight bullets, live metrics (uptime, health, success rate), MP Training Ground badge, CTA button
- **Right side:** Interactive SVG connection graph — radial node-link diagram with center node (current entity) and connected entities radiating outward
- **Graph interactions:** Hover for tooltip, click node with ↗ to open entity website, click node without ↗ to navigate to that entity's detail panel (cross-category navigation)

### Connection System

- 273 connections across 50 entities (avg 5.5 per entity)
- 100% resolution rate (every connection name maps to a real entity)
- Connections stored as name strings in `detail.connections` arrays in `ecosystem_registry.json`
- Animated pulse particles travel along connection lines

### Color Palette Customization

6 overridable CSS tokens via shortcode attributes:

| Attribute | Controls |
|-----------|----------|
| `palette_bg` | Widget outer background |
| `palette_bg_card` | Cards, rings, panels, graph nodes |
| `palette_bg_hover` | Hover/selected states |
| `palette_text` | Primary text |
| `palette_text_muted` | Secondary text, labels |
| `palette_border` | Borders, dividers |

Example: `[qwf_ecosystem palette_bg="#0c1629" palette_text="#f0e6d3" accent="#d4a843"]`

Overrides applied as CSS custom properties on Shadow DOM root. Partial overrides fine — unspecified tokens keep theme defaults.

### All Shortcode Attributes

| Attribute | Default | Purpose |
|-----------|---------|---------|
| `mode` | `block` | `block` or `page` |
| `theme` | `dark` | `dark`, `light`, or `auto` (OS preference) |
| `accent` | `#2dd4bf` | Stat values, CTA buttons, pulse bar |
| `categories` | all | Comma-separated: `app,program,system,infra,pedagogy,content,site` |
| `featured` | `false` | Show only featured entities |
| `refresh` | `60` | API poll interval (seconds) |
| `page_url` | none | "View All" link URL in block mode |

### Tech Stack

| Layer | Technology |
|-------|-----------|
| Framework | Preact 10.x (3 KB React alternative) |
| Build | Vite 6.x, IIFE output, Terser |
| Isolation | Shadow DOM (no style leakage) |
| API | Digital Twin server (Python, port 8767) |
| Data | Static JSON registry + live metric merge |
| WordPress | mu-plugin, `[qwf_ecosystem]` shortcode |

### Key Files

| File | Purpose |
|------|---------|
| `100 Resources/ecosystem-widget/src/` | Widget source (11 Preact components, styles, types) |
| `100 Resources/ecosystem-widget/qwf-ecosystem-widget.php` | WordPress mu-plugin |
| `005 Operations/Data/ecosystem_registry.json` | Entity data (50 entities, single source of truth) |
| `005 Operations/Execution/digital_twin_server.py` | API server (`/api/ecosystem` endpoint) |

### Entity Registry

Edit `005 Operations/Data/ecosystem_registry.json` to add/remove/modify entities. No code rebuild needed — the API serves whatever is in the registry (60s cache).

7 categories: Apps (10), Programs (7), Systems (10), Infrastructure (5), Teaching (3), Content (4), Sites (11)

6 statuses: production, active, alpha, building, planning, standby

### Build & Deploy

```bash
# Rebuild widget
cd "100 Resources/ecosystem-widget" && npm run build:all

# Deploy WordPress plugin update
scp "100 Resources/ecosystem-widget/qwf-ecosystem-widget.php" bitnami@<WP_SERVER_IP>:/tmp/
ssh bitnami@<WP_SERVER_IP> "sudo cp /tmp/qwf-ecosystem-widget.php /opt/bitnami/wordpress/wp-content/mu-plugins/"

# Cache bust: increment version in loader.ts + .php, rebuild, redeploy
```

### Reference

- **Live URL:** `https://twin.quietlyworking.org/ecosystem/widget.js?v=2.1.0`
- **System Status:** `002 Projects/_QWF Ecosystem Widget/Ecosystem-Widget-System-Status.md`
- **User Manual:** `002 Projects/_QWF Ecosystem Widget/User-Manual.md`
- **Directive (landing section):** `005 Operations/Directives/qwf_ecosystem_landing_section.md` (separate — Lovable apps only)

### 🎓 Missing Pixel Training Opportunities

| Component | Skills Developed | Difficulty |
|-----------|------------------|------------|
| Widget Architecture | Preact, Shadow DOM, CSS isolation, IIFE bundles | ⭐⭐⭐ |
| SVG Data Visualization | SVG coordinate math, radial layouts, animation, interactivity | ⭐⭐⭐ |
| WordPress Plugin Dev | PHP shortcodes, mu-plugins, data attributes, multisite | ⭐⭐ |
| JSON Data Modeling | Entity registries, relationship graphs, schema design | ⭐⭐ |
| API Integration | REST polling, cache management, error resilience | ⭐⭐ |
| CSS Custom Properties | Theming systems, palette overrides, responsive design | ⭐⭐ |

**Portfolio project candidate:** Build a mini ecosystem widget for a different dataset (e.g., a student's personal project portfolio). Demonstrates frontend engineering, data visualization, and embeddable component design.

---

## QWR Team Accounts System ⭐ NEW

**Status:** Deployed (Feb 27-28, 2026)
**Prompts:** 068-079 (12 Lovable prompts)

### What It Does

Transforms QWR from a single-user platform into a multi-user team collaboration system. Account owners can invite team members, assign them to specific brands, and control what they can do — all while maintaining backward compatibility for solo users.

### Architecture

**Roles (4-tier hierarchy):**
| Role | Can Do | Can't Do |
|------|--------|----------|
| Owner | Everything + billing + team management | — |
| Admin | Manage team, create/edit content, all brands | Billing, delete account |
| Editor | Create/edit content for assigned brands only | Team management, settings |
| Viewer | View content and analytics for assigned brands | Create, edit, or manage anything |

**Seat Allocation per Tier:**
| Tier | Seats | Monthly |
|------|-------|---------|
| Starter | 2 | $99 |
| Growth | 5 | $299 |
| Agency | 15 | $799 |

**Backward Compatibility:** Solo users are unaffected. The `get_account_id()` helper function returns `auth.uid()` for users who aren't members of any team — they ARE the account. This means zero migration needed for existing supporters.

### Database Layer

**4 new tables:**
- `account_members` — Team roster (role, status, invite token, expiry)
- `member_brand_access` — Which brands each member can access
- `team_activity_log` — Audit trail of team actions
- `approval_requests` — Content approval workflow queue

**4 helper functions (STABLE SECURITY DEFINER):**
- `get_account_id()` — Returns the account a user belongs to (or self for solo users)
- `get_user_role()` — Returns user's role within their account
- `user_has_brand_access()` — Checks if user can access a specific brand
- `get_team_member_count()` — Current member count for seat enforcement

**RLS Migration:** All 37 existing tables migrated from `auth.uid()` to `get_account_id()` + `user_has_brand_access()` pattern. 76 old policies dropped and replaced with team-aware policies.

### Invite Flow

1. Owner/Admin clicks "Invite Member" in Team Settings
2. Enters email, role, brand assignments
3. `account_members` row created (status='invited', invite_token generated, 7-day expiry)
4. n8n webhook `qwr-team-invite` fires → `qwr_team_invite.py` sends invitation email via Graph API (from Ezer Aión)
5. Recipient clicks invite link → `/invite/:token` page (Lovable)
6. `accept-team-invite` edge function validates token, links user to account
7. Team Welcome page shows role, brands, capabilities

### Infrastructure Components

| Component | Type | ID/Path |
|-----------|------|---------|
| `accept-team-invite` | Supabase Edge Function | `verify_jwt=false` |
| `qwr_team_invite.py` | Python script (v1.0.0) | `005 Operations/Execution/` |
| QWR Team Invite Email Sender | n8n workflow | `kMhNP4iiP9MjS7Q7` |
| Stripe Webhook Handler v1.3 | n8n workflow | `rZt6WRkGtX7LQgqo` |

**Stripe Integration:** v1.3 of the webhook handler sets `max_team_members` on `supporter_partners` during both new subscriptions (`checkout.session.completed`) and tier changes (`customer.subscription.updated`). This enforces seat limits: Starter→2, Growth→5, Agency→15.

### Training Opportunities

| Skill | What Students Learn | Complexity |
|-------|-------------------|------------|
| Row-Level Security | PostgreSQL RLS with helper functions, multi-tenant patterns | ⭐⭐⭐ |
| Role-Based Access Control | 4-role hierarchy, permission gates, brand-level scoping | ⭐⭐⭐ |
| Invite Flow Architecture | Token generation, expiry, edge function validation, email delivery | ⭐⭐⭐ |
| Backward Compatibility | Designing systems that don't break existing users | ⭐⭐ |
| Webhook Integration | n8n → SSH → Python → Graph API pipeline for email delivery | ⭐⭐ |

---

## QWF Documentation Standard ⭐ NEW

**Added: March 2, 2026**

Defines the structure, quality criteria, and maintenance rules for all user-facing documentation across QWF apps. Every "Quietly ___" app must have a **User Manual** (Markdown, in the vault) and an **In-App Documentation Center** (`/docs`, built in Lovable).

### Two-Layer Documentation Model

| Layer | Format | Location | Authority |
|-------|--------|----------|-----------|
| **User Manual** | Markdown | `002 Projects/_[App] Projects/[App]-User-Manual.md` | **Source of truth** |
| **Documentation Center** | React components | `/docs` route in Lovable app | Derived from manual |

**Source of Truth Rule:** The User Manual is always the master document. The `/docs` center renders manual content with visual elements (cards, diagrams, interactive navigation). When they drift: update the manual first, then create a `/docs` sync prompt. Never update `/docs` independently.

**Sync Cadence:** Create a `/docs` sync prompt after every 5+ Lovable prompts or after any major feature phase, whichever comes first.

### Required Sections (14 total, in order)

Every QWF app User Manual must include: (1) Table of Contents, (2) What Is [App]?, (3) Key Concepts (supporter-partner framing), (4) Getting Started (step-by-step + flow diagram), (5) Core Feature Sections (user journey order), (6) Settings (one subsection per tab), (7) The Landing Page, (8) FAQ (15+ entries, 4+ categories), (9) Troubleshooting (5+ entries), (10) Keyboard Shortcuts, (11) Getting Help (identical across apps), (12) Glossary, (13) Release History, (14) Planned Updates.

### Pricing Comparison Chart (Required)

Every subscription app manual includes a two-part pricing comparison: (1) "Every Tier Includes the Full Platform" — grouped feature list reinforcing full access at every tier, (2) "What Differs by Tier" — compact table showing only volume limits and access features.

### Quality Checklist (12 checks)

Completeness, accuracy, consistency, terminology, pricing, diagrams, cross-references, TOC currency, troubleshooting, release history, `/docs` sync, planned vs. shipped.

### Key Files

- **Directive:** `005 Operations/Directives/qwf_documentation_standard.md`
- **Model manual:** `002 Projects/_QWR Quietly Writing App/QWR-User-Manual.md` (v4.0.1)
- **CLAUDE.md:** Added as Foundational Directive (v1.30.0)

### Implementation Status

| App | User Manual | /docs Center | Notes |
|-----|------------|-------------|-------|
| QWR (Quietly Writing) | ✅ v4.0.1 | ✅ v4 (Prompt 088) | Model for all future manuals |
| QQT (Quietly Quoting) | Not started | Not started | Next to document |
| QNT (Quietly Networking) | Not started | Not started | — |
| Others | Not started | Not started | — |

### 🎓 Missing Pixel Training Opportunities

| Component | Skills Developed | Difficulty |
|-----------|------------------|------------|
| User Manual Writing | Technical writing, documentation structure, Markdown | ⭐⭐ |
| Quality Audit | Cross-referencing, accuracy verification, gap analysis | ⭐⭐ |
| /docs Sync Prompts | Lovable prompt engineering, React component design | ⭐⭐⭐ |

---

## Weavy Creative Production System ⭐ NEW

**Added: March 4, 2026**

Weavy (weavy.ai) is a node-based AI creative workflow platform used for QWF visual production — product photography, lifestyle shots, character consistency, and video generation. All QWF visual production workflows are built in Weavy and documented in a dedicated user manual.

### Architecture

```
Weavy Platform (weavy.ai)
    → Node-based workflows (text, image, LLM, generation nodes)
        → AI Models (Flux 1.1 Ultra, Nano Banana Pro, GPT Image 1, Gemini 2.5 Flash, etc.)
            → Post-processing (Bria BG Remove, Magnific Upscale, Relight)
                → Final assets for print/web/social
```

### Methodology Source

**Rory Flynn** (Systematiq AI) is the primary methodology source. His newsletter archive and workflow breakdowns provide the prompt patterns, compositing pipelines, and workflow architectures that underpin all QWF visual production. See `003 Entities/Experts/Rory Flynn.md`.

Key principles adopted from Rory's work:
- JSON structure over prose prompts
- Material physics over aesthetic descriptions
- Camera specifications as model filters
- Negative constraints as fences
- Three-tier prompt maturity (V1 Curated → V2 Variance → Active Production)

### Active Workflows

| Project | Workflow | Status | Notes |
|---------|----------|--------|-------|
| GreenCal Leafie | 3-phase plushie vendor reference | Phase 3 operational | Hero shot, turnaround grid, lifestyle shots |
| L4G Postcard Ads | Ad creative generation | Planned | Missing Pixel student training component |
| WOH Product Shots | Product photography pipeline | Planned | War on Hopelessness merchandise |

### Weavy User Manual

A comprehensive 17-chapter + appendices user manual lives at `004 Knowledge/How-To/Weavy-User-Manual.md` (v2.0.0). Covers:
- 12 prompt patterns (JSON-structured, material physics, camera specs, multi-set generation, etc.)
- 2 complete case studies (Sandwich Tornado compositing, AI GPT Photoshoot pipeline)
- Node types, model comparison, credit costs, glossary
- 4-week learning path with prioritized Systematiq newsletter issues

### Key Files

| File | Purpose |
|------|---------|
| `004 Knowledge/How-To/Weavy-User-Manual.md` | Comprehensive Weavy user manual (v2.0.0) |
| `005 Operations/Directives/weavy_creative_workflows.md` | Creative production directive (v1.5.0) |
| `003 Entities/Experts/Rory Flynn.md` | Methodology source entity |
| `002 Projects/_GreenCal Projects/Leafie-Plushie-Weavy-Workflow.md` | GreenCal Leafie 3-phase workflow spec |
| `002 Projects/_GreenCal Projects/Callie "Leafie" Chlorophyllis XII.md` | Leafie character bible |

### App Mode (Missing Pixel)

Weavy offers an App Mode that provides a simplified interface for students: single-step execution with pre-configured parameters. Training progression: App Mode (beginner) → Workflow Editor (intermediate) → Custom Workflow Builder (advanced).

### 🎓 Missing Pixel Training Opportunities

| Component | Skills Developed | Difficulty |
|-----------|------------------|------------|
| JSON Prompt Engineering | Structured prompting, material physics, camera specs | ⭐⭐ |
| Node-Based Workflow Design | Visual programming, data flow, input/output wiring | ⭐⭐ |
| AI Model Selection | Cost/quality tradeoffs, model strengths, credit budgeting | ⭐⭐ |
| Multi-Phase Production Pipeline | Project planning, phase progression, asset management | ⭐⭐⭐ |
| Compositing Workflows | Background removal, element layering, lighting unification | ⭐⭐⭐ |

---

## Session Log

> [!NOTE] Session Log Redacted
> The private version of this manual maintains a detailed session log documenting 68+ operational sessions dating from December 2025 to present. These sessions chronicle the iterative build-out of the entire QWU Backoffice system.
>
> The session log is excluded from the public version because it contains specific operational details (error messages with IPs, credential rotation events, supporter-specific interactions) that would be sensitive to publish.
>
> **For students:** The session log demonstrates real-world iterative development — each session builds on the last, errors lead to improvements, and the system self-anneals over time. Ask your mentor about accessing the session log during supervised learning.

---

*Last updated: 2026-03-17 08:02 (v3.44)*