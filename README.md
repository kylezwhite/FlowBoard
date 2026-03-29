# FlowBoard

**Free, open-source project management that lives in your Google Drive.**

No servers. No monthly fees. No data stored by us. Your projects live in your own Google Drive — forever.

[![Deploy to GitHub Pages](https://img.shields.io/badge/Deploy%20to-GitHub%20Pages-blue?style=for-the-badge&logo=github)](https://github.com/kylezwhite/FlowBoard/fork)

> ⚠️ After deploying, you still need to complete the **Google OAuth setup** (Step 3 below). The app won't work until you do — it takes about 10 minutes.

---

## Features

- **Personal workspace** — private projects only you can see, stored in your Drive
- **Organization workspace** — shared projects with role-based permissions
- **Admin / Member roles** — invite people, promote/demote, remove at any time
- **Hidden projects** — only visible to assigned collaborators
- **Tasks** with To Do / In Progress / Complete status and sorting
- **Task detail panels** — notes with timestamps, due dates, calendar sync
- **Assign tasks** — to org members, personal contacts, or placeholder names
- **Assigned to Me** — view all tasks assigned to you across every project and org
- **Google Calendar sync** — with past-due reminders and alert customization
- **Share personal projects** — via email invite link
- **Transfer projects to an org** — move personal work into your organization
- **Settings** — light, dark, and slate themes; global alert defaults; people list management
- **Installable PWA** — works on desktop and mobile like a native app
- **100% free** — runs on Google Drive storage and Google OAuth, both free

---

## How It Works

```
Your Google Drive
└── FlowBoard_Data/
    ├── project_abc.json    ← your personal projects
    └── ...

FlowBoard_Orgs/
└── org_xyz/
    ├── fb_org_xyz.json     ← org members & settings
    └── projects/
        ├── project_1.json  ← org projects
        └── ...
```

Each user's data lives in **their own Google Drive**. You as the app owner never see, store, or have access to anyone's data. There is no central database.

---

## Deploy Your Own Copy

Total time: ~15 minutes. Hosted free on GitHub Pages — no bandwidth limits, no suspensions.

---

### Step 1 — Fork & Enable GitHub Pages

1. Click **Fork** at the top right of this repository
2. Go to your fork → **Settings** → **Pages** (left sidebar)
3. Under **Source**, select **Deploy from a branch**
4. Choose **main** branch, **/ (root)** folder → click **Save**
5. Wait ~60 seconds — your URL will appear: `https://YOUR_USERNAME.github.io/FlowBoard`

---

### Step 2 — Set Up Google OAuth (Required)

#### 2a. Create a Google Cloud Project
1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Click **Select a project** → **New Project** → name it `FlowBoard` → **Create**

#### 2b. Enable Google Drive API
1. Go to **APIs & Services → Library**
2. Search **Google Drive API** → **Enable**

#### 2c. Configure Google Auth Platform
1. Click **Google Auth Platform** in the sidebar (or APIs & Services → OAuth consent screen)
2. If unconfigured, click **Get started** and complete the 4-screen setup:
   - App name: `FlowBoard`, support email: yours
   - Audience: **External**
   - Contact email: yours
   - Agree and continue

#### 2d. Create OAuth Client ID
1. Click **Clients** in the sidebar → **Create Client**
2. Choose **Web application**
3. Under **Authorized JavaScript origins** add:
   ```
   https://YOUR_USERNAME.github.io
   ```
   *(your GitHub username, no trailing slash, no /FlowBoard)*
4. Click **Create** → **copy your Client ID**

#### 2e. Add Yourself as a Test User
1. Click **Audience** in the sidebar
2. Scroll to **Test users** → **Add users** → add your Google email → **Save**

---

### Step 3 — Add Your Client ID to the App

1. In your GitHub repo, click `index.html` → pencil icon to edit
2. Find:
   ```javascript
   const HARDCODED_CLIENT_ID = '';
   ```
3. Replace with your Client ID:
   ```javascript
   const HARDCODED_CLIENT_ID = '123456789-abc.apps.googleusercontent.com';
   ```
4. Click **Commit changes** — GitHub Pages redeploys in ~60 seconds

---

### Step 4 — Test It

Visit `https://YOUR_USERNAME.github.io/FlowBoard` → **Continue with Google** → done!

---

## Installing as a PWA

| Platform | How to install |
|---|---|
| **Chrome / Edge (Desktop)** | Install icon in the address bar |
| **iPhone / iPad** | Safari → Share → Add to Home Screen |
| **Android** | Chrome → menu → Install app |

---

## Organization Setup

**Recommended: use a dedicated Google account** (e.g. `yourcompany.flowboard@gmail.com`) so the org isn't tied to one person. Store credentials in a shared password manager.

1. Sign into FlowBoard with the dedicated account → create the org
2. Sign back out, sign in with your personal account
3. Get invited as admin by the dedicated account

---

## Roles & Permissions

| Role | Permissions |
|---|---|
| **Owner** | Full control — created the org |
| **Admin** | Invite/remove members, manage all projects, org settings |
| **Member** | Create projects, manage their own |

**Task assignment:** Owners, Admins, and project creators can assign anyone. Members can only self-assign.

---

## Troubleshooting

| Problem | Fix |
|---|---|
| Sign in error | Add `https://YOUR_USERNAME.github.io` as Authorized JavaScript Origin (no path, no trailing slash) |
| "Access blocked" | Add your email as a Test User under Audience in Google Auth Platform |
| 404 on GitHub Pages | Wait a few minutes after enabling, or check Settings → Pages |
| Projects not loading | Sign out and back in |
| Changes not saving | Check internet connection — saves go direct to Google Drive |

---

## Tech Stack

- **Frontend:** Vanilla HTML/CSS/JS — no build tools
- **Auth:** Google Identity Services (OAuth 2.0)
- **Storage:** Google Drive API v3
- **Hosting:** GitHub Pages (free, unlimited)
- **Cost:** $0

---

*MIT License · No tracking · No ads · No data collection*
