---
{"dg-publish":true,"permalink":"/quietly-working-universe-public-transparency-project/sop/qwu-backoffice-user-manual/","noteIcon":""}
---

# QWU Backoffice User Manual

**Version: 2.0 | Started: 251223 | Updated: 251230**

A comprehensive guide to the QWU Backoffice agent workspace, covering architecture, daily operations, automation, and development workflows. These notes serve both as operational documentation and educational curriculum for Missing Pixel students.

---

## Table of Contents

1. [Environment Overview](#environment-overview)
2. [Getting Started](#getting-started)
3. [Daily Operations](#daily-operations)
4. [One-Tap Mobile VM Control](#one-tap-mobile-vm-control-via-n8n)
5. [Running Agent Jobs](#running-agent-jobs)
6. [Overnight/Long-Running Jobs](#overnightlong-running-jobs)
7. [Mobile Access via Termux](#mobile-access-via-termux-android)
8. [Obsidian + GitHub Integration](#obsidian--github-integration-unified-workspace)
9. [Sparse Checkout](#sparse-checkout-filtering-files-on-azure-vm)
10. [Syncing Workflow](#syncing-workflow)
11. [Claude Code](#claude-code-modes-and-commands)
12. [DOE Architecture & Skills](#doe-architecture--skills-system)
13. [Communications Architecture](#communications-architecture)
14. [Data Architecture](#data-architecture)
15. [YAML Frontmatter Standards](#yaml-frontmatter-standards)
16. [Docker Fundamentals](#docker-fundamentals-running-isolated-tasks)
17. [Docker Sandbox Security](#docker-sandbox-security)
18. [Transcript Extraction System](#transcript-extraction-system-planned)
19. [Ez/Ezer Mascot](#ezezer-mascot)
20. [Troubleshooting](#troubleshooting)
21. [Resources](#resources)
22. [Session Log](#session-log)

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
│  │  │  (isolated      │  │  ├── .claude/skills/        │   │    │
│  │  │   containers)   │  │  ├── directives/            │   │    │
│  │  └─────────────────┘  │  ├── execution/             │   │    │
│  │                       │  └── [obsidian vault]       │   │    │
│  │  ┌─────────────────┐  └─────────────────────────────┘   │    │
│  │  │  Claude Code    │                                    │    │
│  │  │  (AI agent)     │                                    │    │
│  │  └─────────────────┘                                    │    │
│  └─────────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────────┘
```

### VM Details

| Property | Value |
|----------|-------|
| Name | claude-dev-vm |
| Resource Group | claude-dev-rg |
| Region | West US 2 |
| Size | Standard B2ms (2 vCPUs, 8 GB RAM) |
| IP | 4.155.237.137 (may change if stopped/started) |
| Image | Ubuntu Server 24.04 LTS |
| Auto-shutdown | 7 PM Pacific (safety net) |

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
    HostName 4.155.237.137
    User azureuser
    IdentityFile ~/.ssh/your-key.pem
```

### Understanding the Dev Container

The `.devcontainer/` folder contains configuration for isolated development:
- `Dockerfile` - Container image definition
- `devcontainer.json` - VS Code settings
- `init-firewall.sh` - Network security rules

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
2. Filter by resource group: `claude-dev-rg`
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
  --scopes "/subscriptions/{sub-id}/resourceGroups/CLAUDE-DEV-RG/providers/Microsoft.Compute/virtualMachines/claude-dev-vm"
```

| Field | Value |
|-------|-------|
| Client ID | `dcb9ba9d-ef7e-40f9-b544-cd610b47989e` |
| Client Secret | Stored in n8n Variables |
| Tenant ID | `0145880a-4b4c-4a79-8109-06cc5af8f7b5` |
| Subscription ID | `cbeeb5c9-bf67-42d6-94cf-6282ef26f001` |
| Resource Group | `CLAUDE-DEV-RG` |
| VM Name | `claude-dev-vm` |

### n8n Webhook Endpoints

| Action | URL |
|--------|-----|
| Start | `https://quietlyworking.app.n8n.cloud/webhook/vm-control?action=start` |
| Stop | `https://quietlyworking.app.n8n.cloud/webhook/vm-control?action=stop` |
| Status | `https://quietlyworking.app.n8n.cloud/webhook/vm-control?action=status` |

### Termux Scripts

**~/.shortcuts/qwu-start.sh** - Start VM + wait + connect:

```bash
#!/data/data/com.termux/files/usr/bin/bash
# Version: 1.0.0
# QWU Start + Connect

WEBHOOK_URL="https://quietlyworking.app.n8n.cloud/webhook/vm-control?action=start"
VM_IP="4.155.237.137"
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

WEBHOOK_URL="https://quietlyworking.app.n8n.cloud/webhook/vm-control?action=stop"

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
4. Disable auto-shutdown in Azure Portal (or extend the time)
5. Go to sleep 😴
6. Reconnect next day: `tmux attach -s lead-scraper`

---

## Overnight/Long-Running Jobs

### Disabling Auto-Shutdown Temporarily

**Via Azure Portal:**

1. Azure Portal → VM → Operations → Auto-shutdown
2. Toggle to Off
3. Save
4. **Remember to re-enable!**

**Via Azure CLI:**

```bash
# Disable
az vm auto-shutdown --resource-group claude-dev-rg --name claude-dev-vm --off

# Re-enable (7 PM Pacific)
az vm auto-shutdown --resource-group claude-dev-rg --name claude-dev-vm --time 1900 --timezone "Pacific Standard Time"
```

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
    HostName 4.155.237.137
    User azureuser
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
- VM is probably stopped (auto-shutdown). Start it from Azure Portal or use qwu-start.sh.

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
C:\Users\Chaplain TIG\qwu_backOffice
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
# Obsidian workspace cache
.obsidian/workspace.json
.obsidian/workspace-mobile.json
.obsidian/plugins/obsidian-git/data.json
.trash/
.tmp.driveupload/
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

---

## DOE Architecture & Skills System

The QWU Backoffice uses a 3-layer DOE (Directive-Orchestration-Execution) architecture.

### Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│  LAYER 1: DIRECTIVE (What to do)                                │
│  Natural language instructions in Markdown                      │
│  Location: directives/                                          │
├─────────────────────────────────────────────────────────────────┤
│  LAYER 2: ORCHESTRATION (Decision making)                       │
│  AI agent reads directives, makes routing decisions             │
│  Handles errors, asks for clarification, updates directives     │
├─────────────────────────────────────────────────────────────────┤
│  LAYER 3: EXECUTION (Doing the work)                            │
│  Deterministic Python scripts                                   │
│  Location: execution/                                           │
└─────────────────────────────────────────────────────────────────┘
```

| Layer | Location | Purpose |
|-------|----------|---------|
| Directive | `directives/` | SOPs in Markdown defining goals, inputs, tools, outputs |
| Orchestration | AI Agent | Intelligent routing, error handling, learning |
| Execution | `execution/` | Deterministic Python scripts for API calls, data processing |

### Key Principles

- **Check for tools first** - Before writing a script, check if one exists
- **Self-anneal when things break** - Fix, test, update directive
- **Update directives as you learn** - Directives are living documents
- **Deliverables in cloud** - Use Google Sheets, Slides, etc. for outputs
- **Local files for processing only** - Everything in `.tmp/` is temporary

### Skills System

Skills provide domain-specific knowledge that agents reference:

```
.claude/skills/
├── qwf-brand-voice/          # Voice profiles
│   ├── SKILL.md              # Overview + when to use each
│   ├── tig-standard.md       # Full TIG voice profile
│   ├── woh-combat.md         # WOH combat voice
│   └── l4g-b2b.md            # L4G business voice
│
├── qwf-programs/             # Program context
│   ├── SKILL.md
│   ├── acofh.md              # Mission, audience, sensitivities
│   ├── mp.md                 # Missing Pixel details
│   ├── iysr.md
│   ├── woh.md
│   ├── qwc.md
│   └── l4g.md
│
└── qwf-print-specs/          # Production specs
    ├── l4g-postcard.md
    └── apparel.md
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

The workspace uses MCP (Model Context Protocol) servers for tool access:

**File:** `.claude/mcp.json`

```json
{
  "mcpServers": {
    "vista-social": {
      "url": "https://vistasocial.com/api/integration/mcp?api_key=YOUR_KEY"
    }
  }
}
```

**Important:** For Docker environments, add MCP domains to firewall allowlist:
- `vistasocial.com`
- `quietlyworking.app.n8n.cloud`

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

### What to Store in Tool Notes (003 Humans, Orgs and Tools/)

| Store in Obsidian | Let Agents Search Online |
|-------------------|--------------------------|
| Your account tier/plan | General "how to" docs |
| Your specific configurations | API reference details |
| API key location (not the key) | Troubleshooting generic issues |
| Workflows YOU actually use | Feature changelogs |
| Gotchas you've discovered | Best practices guides |
| Integration notes | |

### Mobile-to-Obsidian Workflow

```
1. You dump content → 000 Inbox/___Capture/
2. Agent detects new file
3. Agent moves to → 000 Inbox/___Processing/
4. Agent enriches (YAML, tags, links)
5. Agent moves to → 000 Inbox/___Review/
6. You review (or auto-file based on confidence)
7. Final destination in appropriate folder
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
digital-garden: publish
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

Notes with `digital-garden: publish` become eligible for transparency.quietlyworking.org.

**To publish:**
1. Ensure note is in appropriate folder
2. Add `digital-garden: publish` to frontmatter
3. Sync runs automatically

**To keep private:**
- Omit the field, or
- Set `digital-garden: private`

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
    "quietlyworking.app.n8n.cloud"
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

## Troubleshooting

### Can't Connect to VM

1. **Check if VM is running** - Azure Portal → VM should show "Running"
2. **Check IP address** - It may have changed after restart
3. **Try status webhook** - `curl "https://quietlyworking.app.n8n.cloud/webhook/vm-control?action=status"`

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

---

## Resources

### Key URLs

| Resource | URL |
|----------|-----|
| Azure Portal | https://portal.azure.com |
| VS Code Remote SSH Docs | https://code.visualstudio.com/docs/remote/ssh |
| Anthropic API Docs | https://docs.anthropic.com |
| n8n Dashboard | https://quietlyworking.app.n8n.cloud |

### Tips & Gotchas

1. **SSH Key is critical** - Cannot be re-downloaded. Back it up immediately.

2. **VM IP can change** - If VM is stopped and started, IP might change. Check Azure Portal and update SSH config if connection fails.

3. **Auto-shutdown is a safety net** - You can always stop early or disable for overnight jobs.

4. **No auto-start** - VM only runs when you manually start it. This is good (no surprise bills).

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
- Build inbox processing automation
- Complete Discord server setup

---

## Session Log

### Session 1 - December 24, 2025
**Completed:**
- ✅ Created Azure nonprofit account
- ✅ Deployed Ubuntu 24.04 VM (B2ms, 8GB RAM)
- ✅ Configured auto-shutdown (7 PM Pacific)
- ✅ Cloud-init installed Docker 29.1.3 and tmux 3.4
- ✅ Set up SSH key on Windows (learned: must be on local drive, not network drive)
- ✅ Connected via VS Code Remote SSH
- ✅ Verified Docker and tmux working

**VM Details:**
- Name: claude-dev-vm
- Resource Group: claude-dev-rg
- Region: West US 2
- Size: Standard B2ms (2 vCPUs, 8 GB RAM)
- IP: 4.155.237.137 (may change if VM stopped/started)
- Image: Ubuntu Server 24.04 LTS (Canonical)

---

### Session 2 - December 25, 2025
**Completed:**
- ✅ Started VM and reconnected via VS Code Remote SSH
- ✅ Cloned qwu_backOffice repo from GitHub
- ✅ Created .env file with API keys
- ✅ Tested Claude API connection (working!)
- ✅ Learned Docker fundamentals:
  - Running simple commands in containers
  - Interactive container sessions
  - Running Python without installing it
  - Mounting folders into containers
  - Reading repo files from inside containers
- ✅ Installed Claude Code on Azure VM
- ✅ Set up unified Obsidian + GitHub workspace:
  - Installed obsidian-git plugin
  - Merged Obsidian vault into qwu_backOffice repo
  - Configured auto-sync (10 min intervals)
  - Set up sparse checkout on VM (excludes images, canvas, etc.)
- ✅ Learned PowerShell vs Command Prompt differences

**Key Learnings:** 
- Docker containers are isolated mini-computers. Mount your code with `-v $(pwd):/app`, run your task, container disappears. VM stays clean.
- Unified workspace: One repo serves as both Obsidian vault AND agent codebase.
- Sparse checkout filters what the VM downloads from GitHub (agents only get text files).
- GitHub has 100MB file limit - use .gitignore for large/temp files.
- Network drives (Y:) can cause git permission issues - use local C: drive for repos.

**Repository Structure:**
```
C:\Users\Chaplain TIG\qwu_backOffice\    (Windows/Obsidian)
~/qwu_backOffice/                         (Azure VM)
├── .claude/           ← Agent skills
├── .obsidian/         ← Obsidian config
├── directives/        ← Agent SOPs (editable in Obsidian!)
├── execution/         ← Python scripts (editable in Obsidian!)
├── prompts/
├── 002 Projects/
├── 003 Humans, Orgs and Tools/
├── Resources/
└── [your notes].md
```

---

### Session 3 - December 25, 2025 (Evening)
**Completed:**
- ✅ Set up mobile SSH access via Termux on Android
- ✅ Installed Termux + API + Widget + Styling from F-Droid
- ✅ Generated ED25519 SSH key on phone
- ✅ Added mobile key to VM authorized_keys
- ✅ Created SSH config shortcut (`ssh qwu`)
- ✅ Successfully connected to Azure VM from phone!

**Why This Matters:**
- Can check on overnight agent runs from bed 📱
- Don't need laptop to verify tmux sessions are still running
- Full terminal access from anywhere with cell/wifi

**Termux Key Details:**
- SSH Key: `~/.ssh/id_ed25519` (ED25519, labeled "termux-mobile")
- SSH Config: `~/.ssh/config` with `Host qwu` shortcut
- ServerAliveInterval: 60 seconds (keeps mobile connections stable)

**Quick Reference:**
```bash
ssh qwu           # Connect from phone
tmux ls           # Check running sessions
tmux attach       # Jump into session
Ctrl+B, D         # Detach (leave running)
exit              # Disconnect
```

---

### Session 4 - December 21-23, 2025
**Completed:**
- ✅ Created Docker sandbox security configuration
  - Dockerfile with all required packages
  - devcontainer.json for VS Code
  - init-firewall.sh with domain allowlists
- ✅ Added MCP server domain support (n8n, Vista Social)
- ✅ Built DOE architecture skill system
  - Brand voice profiles (TIG, WOH, L4G)
  - Program context files (all 6 programs)
  - Agent templates
- ✅ Integrated Vista Social MCP for social media automation
- ✅ Developed Ez/Ezer mascot character bible
- ✅ Learned MCP troubleshooting for Docker environments

**Key Learnings:**
- MCP servers require domain allowlisting in Docker firewalls
- SSE connections need special handling in containerized environments
- Skills provide consistent knowledge across all agents
- Character development connects to organizational mission

---

### Session 5 - December 29, 2025
**Completed:**
- ✅ Designed comprehensive Discord server architecture
  - Role hierarchy with colors and permissions
  - Channel structure for all programs
  - Webhook configuration for agent automation
- ✅ Created Communications Architecture framework
  - Telegram for personal capture
  - Discord for team/community hub
  - Azure VM for power tools
- ✅ Designed mobile-to-Obsidian workflow
  - Capture → Process → Route → Act pattern
  - Agent confidence thresholds
  - Auto-filing based on type
- ✅ Established YAML frontmatter standards for SOPs
- ✅ Defined data architecture boundaries (SuiteDash vs Obsidian)

**Key Learnings:**
- Discord aligns with gamer/VFX/creative demographic
- "Students Help BUILD" framework applies to all system design
- Automation channels should be read-only for humans
- Document history sections support version tracking

---

### Session 6 - December 30, 2025
**Completed:**
- ✅ Explored Claude Code transcript extraction system
  - Analyzed Simon Willison's approach
  - Planned Obsidian markdown adaptation
  - Mapped to transparency publishing workflow
- ✅ Built One-Tap Mobile VM Control (MAJOR!)
  - Created Azure Service Principal
  - Built n8n workflow with start/stop/status
  - Created Termux widget scripts
  - Tested full end-to-end flow
- ✅ Documented credential rotation process
- ✅ Consolidated all scattered work into comprehensive manual update

**Key Learnings:**
- Azure Service Principal scopes to specific resources for security
- n8n webhooks enable external triggers when VM is off
- Termux polling handles variable VM boot times gracefully
- Comprehensive documentation prevents context loss

---

## Document History

*Do not use content below this line for operations.*

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 2.0 | 251230 | TIG + Claude | Major update: Added One-Tap VM Control, DOE Architecture, Communications Architecture, Data Architecture, YAML Standards, Docker Security, Ez/Ezer Mascot, Sessions 4-6 |
| 1.1 | 251225 | TIG + Claude | Added Termux mobile access, Session 3 |
| 1.0 | 251223 | TIG + Claude | Initial release |

---

*Last updated: December 30, 2025*
