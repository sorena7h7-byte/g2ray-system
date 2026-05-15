# MRH-G2Ray Complete Guide (English)

<p align="center">
  <img src="https://img.shields.io/badge/Version-2.0.0-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/Platform-Codespaces-181717?style=flat-square&logo=github"/>
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=flat-square"/>
</p>

---

## 📖 Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [System Requirements & Limitations](#system-requirements--limitations)
- [Step-by-Step Guide for Beginners](#step-by-step-guide-for-beginners)
  - [1. Create a GitHub Account](#1-create-a-github-account)
  - [2. Fork the Repository](#2-fork-the-repository)
  - [3. Create a Codespace](#3-create-a-codespace)
  - [4. Obtain Your VLESS Link (Two Methods)](#4-obtain-your-vless-link-two-methods)
  - [5. Connect to the Internet](#5-connect-to-the-internet)
- [Quota Management: Stop vs Delete](#quota-management-stop-vs-delete)
- [Advanced Configuration (Pro Section)](#advanced-configuration-pro-section)
  - [Changing Machine Type (CPU/RAM)](#changing-machine-type-cpuram)
  - [Securing the Admin Panel (Change Password)](#securing-the-admin-panel-change-password)
  - [Syncing with Upstream](#syncing-with-upstream)
  - [Manual Setup for Developers](#manual-setup-for-developers)
- [Troubleshooting & FAQ](#troubleshooting--faq)
- [Credits & Support](#credits--support)

---

## 🚀 Project Overview

**MRH-G2Ray** is an enterprise-grade wrapper around the `g2ray` project. It leverages **GitHub Codespaces** (free cloud development environments) to run a **VLESS proxy** on GitHub's global infrastructure.

- All traffic routes through **GitHub servers** (no personal VPS required).
- Works seamlessly in restricted regions as long as GitHub is accessible.
- Production-ready architecture with **modular scripts** and **web-based management**.

---

## ✨ Features

| Category | Feature |
|:---|:---|
| **Performance** | Optimized VLESS protocol with TLS encryption |
| **Security** | Unique UUID per Codespace + HTTP Basic Auth for Admin Panel |
| **Usability** | Web Admin Panel (port 8080) – no terminal needed |
| **Reliability** | Modular startup scripts with automatic retry logic |
| **Cost** | 100% free up to 60 hours/month (2-core machines) |
| **Compatibility** | Works with V2rayNG, Hiddify, Streisand, Nekobox, and any VLESS client |

---

## ⚙️ System Requirements & Limitations

| Item | Specification |
|:---|:---|
| **Free monthly quota** | 60 hours (2-core) / 30 hours (4-core) |
| **Free storage** | 15 GB |
| **Minimum machine** | 2 cores (1-core **not** available) |
| **Auto-stop (idle)** | 30 minutes (configurable up to 4 hours) |
| **Supported clients** | Any VLESS-compatible application |

---

## 📝 Step-by-Step Guide for Beginners

### 1. Create a GitHub Account

| Step | Action |
|:---|:---|
| 1 | Go to [GitHub.com](https://github.com) |
| 2 | Click **Sign up** |
| 3 | Enter email, strong password, and username |
| 4 | Enter the 6-digit verification code |

> ⚠️ **Security Advisory:** Use a **secondary (burner) GitHub account** to protect your primary account from potential restrictions.

### 2. Fork the Repository

1. Navigate to: `https://github.com/mrh000mrh/MRH-G2Ray-2`
2. Click the **Fork** button (top-right corner)
3. (Optional) Rename the repository (e.g., `My-Proxy`)
4. Click **Create fork**

### 3. Create a Codespace

1. In your forked repository, click the green **`Code`** button
2. Select the **`Codespaces`** tab
3. Click **`Create codespace on main`**
4. Wait 2–3 minutes for the environment to initialize

### 4. Obtain Your VLESS Link (Two Methods)

#### Method A: Via Admin Panel (Recommended)

| Step | Action |
|:---|:---|
| 1 | After the Codespace loads, a new tab should **automatically open** with the Admin Panel |
| 2 | If not, go to the terminal → **Ports** tab → click the **globe icon (🌐)** next to port `8080` |
| 3 | Log in with default credentials: `admin` / `Sample@Sample` |
| 4 | Click **`Copy VLESS Link`** |

#### Method B: Via Terminal (Fallback)

- A link starting with `vless://` will appear in the terminal output
- Copy the entire link manually

> 🔑 **Security Tip:** Change the default admin password immediately (see Advanced Configuration).

### 5. Connect to the Internet

Paste the copied VLESS link into one of the following clients:

| Client | Platform |
|:---|:---|
| **V2rayNG** | Android |
| **Hiddify** | Android, Windows, macOS, Linux |
| **Streisand** | Windows, macOS, Linux |
| **Nekobox** | Windows, Linux, macOS |

---

## ⏰ Quota Management: Stop vs Delete

| Action | Effect on Compute Hours | Effect on Storage | Best Practice |
|:---|:---:|:---:|:---|
| **Stop** | ✅ Stops | ❌ Continues | Short breaks (≤ 1 hour) |
| **Delete** | ✅ Stops | ✅ Stops | After each session or long breaks |

- **Stop:** Halts the virtual machine. Your files remain on GitHub's disk, consuming your 15 GB storage quota. Use this if you plan to resume work within a few hours.
- **Delete:** Completely removes the Codespace environment. Frees both compute hours and storage space. Use this as your default action for maximum efficiency.

> ✅ **Recommended Workflow:** **Delete** your Codespace after every use, then recreate it next time. This ensures zero storage waste and predictable quota usage.

---

## 🛠️ Advanced Configuration (Pro Section)

### Changing Machine Type (CPU/RAM)

To increase resources, edit `.devcontainer/devcontainer.json`:

```json
"hostRequirements": {
   "cpus": 4,
   "memory": "8gb",
   "storage": "64gb"
}

Machine Type	Free Monthly Hours
2-core (default)	60 hours
4-core	30 hours
8-core	15 hours
16-core	7.5 hours
Securing the Admin Panel (Change Password)
Set environment variables in your Codespace terminal:

export MRH_ADMIN_USERNAME="your-username"
export MRH_ADMIN_PASSWORD="your-strong-password"

Or hardcode them in .devcontainer/devcontainer.json:

"containerEnv": {
   "MRH_ADMIN_USERNAME": "your-username",
   "MRH_ADMIN_PASSWORD": "your-strong-password"
}

Syncing with Upstream
To receive updates from the main repository:

Go to your forked repository on GitHub

Click Sync fork

Click Update branch

Manual Setup (For Developers)

# Clone the repository
git clone https://github.com/mrh000mrh/MRH-G2Ray-2.git
cd MRH-G2Ray-2

# Build the Docker image
docker build -t mrh-g2ray .devcontainer/

# Run the container
docker run -p 443:443 -p 8080:8080 mrh-g2ray




❓ Troubleshooting & FAQ
Issue	Solution
Codespace won't start	Check your free quota (Settings → Billing). If exceeded, wait until next month or use another account.
Admin Panel not opening	Ensure port 8080 is listed in the "Ports" tab. If not, restart the Codespace.
Default password not working	Use admin / Sample@Sample. Change immediately after first login.
VLESS link doesn't connect	Verify the link starts with vless://. Try a different client (e.g., Hiddify instead of V2rayNG).
GitHub Actions error	This is normal on first run. Wait 2 minutes and refresh. If persists, fork again.
💝 Credits & Support
Maintainer: @mrh000mrh
Major Contributor (v2.0): @mahdiit

Donation Address:
0x3A90B058E51deeA95dd8912b4bA71c4b159Ec582
(BNB, Ethereum, Arbitrum, Base, USDT, USDC, DAI)

<p align="center"> <b>© 2026 MRH-G2Ray | Licensed under MIT</b><br> <sub>Empowering free internet access worldwide</sub> </p> ```
