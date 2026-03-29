# Taskie

**Free, open-source project management that lives in your Google Drive.**

No servers. No monthly fees. No data stored by us. Your projects live in your own Google Drive — forever.

[![Deploy to GitHub Pages](https://img.shields.io/badge/Deploy%20to-GitHub%20Pages-blue?style=for-the-badge&logo=github)](https://github.com/kylezwhite/Taskie/fork)

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
- **Google Calendar sync** — dedicated Taskie calendars per workspace, with alerts
- **Share personal projects** — via email invite link
- **Transfer projects to an org** — move personal work into your organization
- **Transfer org ownership** — hand off an org to another user with Drive access instructions
- **Settings** — Dark, Light, Slate, and Retro 70s themes; global alert defaults; people list
- **Installable PWA** — works on desktop and mobile like a native app
- **100% free** — runs on Google Drive storage and Google OAuth, both free

---

## How It Works

```
Your Google Drive
└── Taskie_Data/
    ├── project_abc.json    ← your personal projects
    └── ...

Taskie_Orgs/
└── org_xyz/
    ├── taskie_org_xyz.json     ← org members & settings
    └── projects/
        ├── project_1.json      ← org projects
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
5. Wait ~60 seconds — your URL will appear: `https://YOUR_USERNAME.github.io/Taskie`

---

### Step 2 — Set Up Google OAuth (Required)

#### 2a. Create a Google Cloud Project
1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Click **Select a project** → **New Project** → name it `Taskie` → **Create**

#### 2b. Enable Required APIs
1. Go to **APIs & Services → Library**
2. Search **Google Drive API** → **Enable**
3. Search **Google Calendar API** → **Enable**

#### 2c. Configure Google Auth Platform
1. Click **Google Auth Platform** in the sidebar (or APIs & Services → OAuth consent screen)
2. If unconfigured, click **Get started** and complete the 4-screen setup:
   - App name: `Taskie`, support email: yours
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
   *(your GitHub username — no trailing slash, no /Taskie path)*
4. Click **Create** → **copy your Client ID**

#### 2e. Publish the App
1. Click **Audience** in the sidebar
2. Click **Publish App** so any Google account can sign in
3. If you want to test first, add your email under **Test users** → **Add users** before publishing

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

Visit `https://YOUR_USERNAME.github.io/Taskie` → **Continue with Google** → done!

---

## Installing as a PWA

| Platform | How to install |
|---|---|
| **Chrome / Edge (Desktop)** | Install icon in the address bar |
| **iPhone / iPad** | Safari → Share → Add to Home Screen |
| **Android** | Chrome → menu → Install app |

---

## Themes

Taskie ships with four built-in themes, switchable in Settings:

| Theme | Description |
|---|---|
| **Dark** | Deep navy with sky blue accents (default) |
| **Light** | Clean white with blue accents |
| **Slate** | Dark slate with purple accents |
| **Retro 70s** | Deep navy with teal, red-orange, and amber — inspired by classic 70s poster art |

---

## Google Calendar Integration

When you sync a task to Google Calendar, Taskie creates a **dedicated calendar** — it won't pollute your primary calendar:

- Personal tasks → **Taskie - My Projects** calendar
- Org tasks → **Taskie - [Org Name]** calendar (one per org)

Calendars are created automatically on first sync and reused after that.

---

## Organization Setup

**Recommended: use a dedicated Google account** (e.g. `yourcompany.taskie@gmail.com`) so the org isn't tied to one person. Store credentials in a shared password manager.

1. Sign into Taskie with the dedicated account → create the org
2. Sign back out, sign in with your personal account
3. Get invited as admin by the dedicated account

See **ORG_SETUP.md** for the full organization setup guide.

---

## Roles & Permissions

| Role | Permissions |
|---|---|
| **Owner** | Full control — created the org |
| **Admin** | Invite/remove members, manage all projects, org settings, transfer ownership |
| **Member** | Create projects, manage their own |

**Task assignment:** Owners, Admins, and project creators can assign anyone. Members can only self-assign.

---

## Troubleshooting

| Problem | Fix |
|---|---|
| Sign in error | Add `https://YOUR_USERNAME.github.io` as Authorized JavaScript Origin (no path, no trailing slash) |
| "Access blocked" | Publish the app under Audience in Google Auth Platform, or add your email as a Test User |
| 404 on GitHub Pages | Wait a few minutes after enabling, or check Settings → Pages |
| Projects not loading | Sign out and back in |
| Changes not saving | Check internet connection — saves go direct to Google Drive |
| Setup screen on new device | Make sure `HARDCODED_CLIENT_ID` is set in `index.html` — not just stored in browser localStorage |
| Calendar sync fails | Make sure Google Calendar API is enabled in your Google Cloud project |

---

## Tech Stack

- **Frontend:** Vanilla HTML/CSS/JS — no build tools, no dependencies
- **Auth:** Google Identity Services (OAuth 2.0)
- **Storage:** Google Drive API v3
- **Calendar:** Google Calendar API v3
- **Hosting:** GitHub Pages (free, unlimited bandwidth)
- **Cost:** $0

---

*MIT License · No tracking · No ads · No data collection*
