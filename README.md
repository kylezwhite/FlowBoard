# Taskie

**Free, open-source project management powered by your Google Drive.**

No servers. No monthly fees. No data stored by us. Your projects live in your own Google Drive — forever.

[![Deploy to GitHub Pages](https://img.shields.io/badge/Deploy%20to-GitHub%20Pages-blue?style=for-the-badge&logo=github)](https://github.com/kylezwhite/Taskie/fork)

---

## Features

- **Personal workspace** — private projects stored in your Drive, invisible to everyone else
- **Organization workspace** — shared projects with role-based permissions
- **Admin / Member roles** — invite people, promote/demote, remove at any time
- **Hidden projects** — only visible to assigned collaborators
- **Tasks** — To Do / In Progress / Complete, with sorting and filtering
- **Task detail panels** — timestamped notes log, due dates with time, calendar sync
- **Assign tasks** — to org members, saved contacts, or placeholder names (no account needed)
- **Assigned to Me** — all tasks assigned to you across every project and org, in one view
- **Google Calendar sync** — dedicated Taskie calendars per workspace, never pollutes your primary calendar
- **Share personal projects** — via email invite link
- **Transfer projects to an org** — move personal work into your organization
- **Transfer org ownership** — full 3-step Drive ownership transfer flow
- **4 themes** — Dark, Light, Slate, Retro 70s
- **Global alert defaults** — configure reminder timing once, applies everywhere
- **People list** — manage your assignment autocomplete in Settings
- **Live sync** — polls for changes every 5 seconds when viewing org projects
- **Installable PWA** — works on desktop and mobile like a native app
- **100% free** — Google Drive storage + Google OAuth, both free

---

## How Data Is Stored

```
Your Google Drive
└── Taskie/
    ├── My Projects/
    │   ├── project_abc.json
    │   └── ...
    └── Organizations/
        └── org_xyz/
            ├── taskie_org_xyz.json
            └── projects/
                ├── project_1.json
                └── ...
```

All data lives in **your own Google Drive**. You as the app owner never see or have access to anyone's data. There is no central database or server.

---

## Deploy Your Own Copy

**Total time: ~20 minutes.** Hosted free on GitHub Pages — no bandwidth limits, no suspensions.

---

### Step 1 — Fork & Enable GitHub Pages

1. Click **Fork** at the top right of this repository
2. Go to your fork → **Settings** → **Pages** (left sidebar)
3. Under **Source**, select **Deploy from a branch**
4. Branch: **main**, Folder: **/ (root)** → click **Save**
5. Wait ~60 seconds — your URL appears: `https://YOUR_USERNAME.github.io/Taskie`

---

### Step 2 — Create a Google Cloud Project

1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Click **Select a project** → **New Project**
3. Name it `Taskie` → click **Create**
4. Make sure your new project is selected in the top dropdown

---

### Step 3 — Enable Required APIs

Both APIs are required. Missing either one will cause sign-in or calendar features to fail.

1. Go to **APIs & Services → Library**
2. Search **Google Drive API** → click it → click **Enable**
3. Go back to Library, search **Google Calendar API** → click it → click **Enable**

---

### Step 4 — Configure Google Auth Platform

1. In the left sidebar, click **Google Auth Platform**
   - If you see "Google Auth Platform not configured", click **Get started**
2. Complete the setup across 4 screens:
   - **App Information:** App name = `Taskie`, User support email = your email → **Next**
   - **Audience:** select **External** → **Next**
   - **Contact Information:** your email → **Next**
   - **Finish:** check the agreement → **Continue**

---

### Step 5 — Create an OAuth Client ID

1. In the left sidebar, click **Clients**
2. Click **Create Client**
3. Application type: **Web application**
4. Under **Authorized JavaScript origins**, click **Add URI** and enter:
   ```
   https://YOUR_USERNAME.github.io
   ```
   ⚠️ This must be your GitHub username domain only — **no trailing slash, no /Taskie path**
5. Click **Create**
6. A dialog shows your credentials — **copy the Client ID**
   - It looks like: `123456789-abc.apps.googleusercontent.com`

---

### Step 6 — Bake Your Client ID Into the App

1. In your GitHub repo, click `index.html`
2. Click the **pencil icon** (Edit this file)
3. Press **Ctrl+F** and search for `HARDCODED_CLIENT_ID`
4. Find this line:
   ```javascript
   const HARDCODED_CLIENT_ID = '';
   ```
5. Replace with your Client ID:
   ```javascript
   const HARDCODED_CLIENT_ID = '123456789-abc.apps.googleusercontent.com';
   ```
6. Click **Commit changes** → GitHub Pages rebuilds in ~60 seconds

---

### Step 7 — Publish the App

By default Google puts new apps in "Testing" mode — only explicitly added test users can sign in.

**To open to everyone:**
1. Go to **Google Auth Platform → Audience**
2. Click **Publish App**
3. Confirm

**To stay in testing (just for yourself or a small team):**
1. Go to **Google Auth Platform → Audience → Test users**
2. Click **Add users** and add each Google email that should have access

---

### Step 8 — First Sign In

1. Go to `https://YOUR_USERNAME.github.io/Taskie`
2. Click **Continue with Google**
3. Google will show a consent screen listing the permissions Taskie requests:
   - **Google Drive** — to store your project data
   - **Google Calendar** — to create dedicated Taskie calendars
   - **Profile & Email** — to identify you
4. Click **Allow**
5. You're in. Taskie creates its folder structure in your Drive automatically.

---

## Google OAuth Permissions Explained

Taskie requests these scopes:

| Scope | Why |
|---|---|
| `drive.file` | Read/write only files Taskie itself creates — never your whole Drive |
| `calendar` | Create and manage dedicated Taskie calendars |
| `userinfo.email` | Know who you are |
| `userinfo.profile` | Show your name and photo |

---

## Google Calendar Integration

Taskie never adds events to your primary Google Calendar. Instead it creates dedicated calendars automatically on first sync:

- **Taskie - My Projects** — for personal workspace tasks
- **Taskie - [Org Name]** — one per organization you belong to

These appear in Google Calendar's sidebar and can be shown/hidden independently.

**If calendars aren't appearing:** Go to Taskie Settings → click **↺ Reset Calendar Cache**, then try syncing a task again. This clears any stale calendar IDs and forces fresh creation.

**If you get a permission error on sync:** Sign out of Taskie and back in. Google needs to re-issue your token with Calendar permissions if they weren't granted on your first sign in.

---

## Installing as a PWA

| Platform | How |
|---|---|
| **Chrome / Edge (Desktop)** | Click the install icon in the address bar |
| **iPhone / iPad** | Safari → Share button → Add to Home Screen |
| **Android** | Chrome → three-dot menu → Install app |

---

## Themes

Switch themes in Settings → Theme:

| Theme | Look |
|---|---|
| **Dark** | Deep navy, sky blue accents (default) |
| **Light** | Clean white, blue accents |
| **Slate** | Dark slate, purple accents |
| **Retro 70s** | Deep navy with teal, pink, orange, amber gradient |

---

## Organization Setup

See **ORG_SETUP.md** for the full guide. Short version:

**Use a dedicated Google account** (e.g. `yourcompany.taskie@gmail.com`) so the org isn't tied to one person. Store credentials in a shared password manager. Sign into Taskie with that account to create the org, then invite your personal account as Admin.

---

## Roles & Permissions

| Role | Can do |
|---|---|
| **Owner** | Everything — created the org |
| **Admin** | Invite/remove members, manage all projects, org settings, transfer ownership |
| **Member** | Create and manage their own projects |

**Task assignment:** Owners, Admins, and project creators can assign anyone. Members can only self-assign.

---

## Troubleshooting

| Problem | Fix |
|---|---|
| **Sign in error / "origin not allowed"** | Add `https://YOUR_USERNAME.github.io` as Authorized JavaScript Origin in Google Cloud → Clients. No trailing slash. No `/Taskie` path. |
| **"Access blocked: app not verified"** | Go to Google Auth Platform → Audience → Publish App (or add your email as a Test User) |
| **Setup screen appears on new device** | The Client ID must be hardcoded in `index.html` — not just saved in browser localStorage |
| **Calendar events not appearing** | 1) Make sure Google Calendar API is enabled in Google Cloud. 2) Sign out and back in to re-grant calendar permissions. 3) Settings → Reset Calendar Cache |
| **"Permission denied" on calendar sync** | Sign out and back in — your session was granted before calendar permissions were added |
| **Projects not loading** | Sign out and back in — your session token may have expired |
| **Org not appearing after being invited** | Sign out and back in |
| **Changes not saving** | Check internet connection — saves go directly to Google Drive |
| **404 on GitHub Pages** | Wait a few minutes after enabling Pages. Check Settings → Pages to confirm it's active and pointing to main branch |
| **PWA install option missing** | Must be on HTTPS — GitHub Pages provides this automatically |

---

## Tech Stack

| | |
|---|---|
| **Frontend** | Vanilla HTML/CSS/JS — single file, no build tools, no dependencies |
| **Auth** | Google Identity Services (OAuth 2.0) |
| **Storage** | Google Drive API v3 (`drive.file` scope) |
| **Calendar** | Google Calendar API v3 |
| **Fonts** | Outfit, JetBrains Mono, Courier Prime (Google Fonts) |
| **Hosting** | GitHub Pages (free, unlimited bandwidth) |
| **Cost** | $0 |

---

## Drive Folder Structure

When you first sign in, Taskie creates this structure in your Google Drive automatically:

```
Taskie/                         ← root folder
├── My Projects/                ← personal project files
│   ├── project_[id].json
│   └── ...
└── Organizations/              ← org data (if you create or join orgs)
    └── org_[id]/
        ├── taskie_org_[id].json
        └── projects/
            ├── project_[id].json
            └── ...
```

You can move or rename other things in your Drive freely — Taskie only touches files inside its own `Taskie/` folder.

---

*MIT License · No tracking · No ads · No data collection · Your data stays in your Drive*
