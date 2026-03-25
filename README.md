# FlowBoard

**Free, open-source project management that lives in your Google Drive.**

No servers. No monthly fees. No data stored by us. Your projects live in your own Google Drive account — forever.

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/YOUR_USERNAME/flowboard)

> ⚠️ After deploying, you still need to complete the **Google OAuth setup** (Step 3 in the guide below). The app won't work until you do — it takes about 10 minutes.

---

## Features

- **Personal workspace** — private projects only you can see, stored in your Drive
- **Organization workspace** — shared projects with role-based permissions
- **Admin / Member roles** — invite people, promote/demote, remove at any time
- **Hidden projects** — only visible to assigned collaborators
- **Tasks** with To Do / In Progress / Complete status
- **Progress tracking**, filters, and statistics
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

Each user's data lives in **their own Google Drive**. You as the app owner never see, access, or store anyone's data. There is no central database.

---

## Deploy Your Own Copy

Follow these steps to get your own FlowBoard instance running. Total time: ~20-30 minutes.

---

### Step 1 — Fork & Deploy to Netlify

1. Click the **Deploy to Netlify** button above
2. Connect your GitHub account when prompted
3. Netlify will fork this repo into your GitHub and deploy it automatically
4. Wait ~30 seconds — you'll get a URL like `https://random-name-123.netlify.app`
5. Optional: go to **Site settings → Domain management** to customize your URL

---

### Step 2 — Set Up Google OAuth (Required)

This is what allows users to sign in with Google. You do this once.

#### 2a. Create a Google Cloud Project
1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Click **Select a project** at the top → **New Project**
3. Name it `FlowBoard` → click **Create**
4. Make sure your new project is selected in the top dropdown

#### 2b. Enable Google Drive API
1. Go to **APIs & Services → Library**
2. Search for **Google Drive API** → click it → click **Enable**

#### 2c. Configure OAuth Consent Screen
1. Go to **APIs & Services → OAuth consent screen**
2. Choose **External** → click **Create**
3. Fill in:
   - **App name:** FlowBoard
   - **User support email:** your email
   - **Developer contact email:** your email
4. Click **Save and Continue** through all remaining screens (defaults are fine)

#### 2d. Create OAuth Credentials
1. Go to **APIs & Services → Credentials**
2. Click **Create Credentials → OAuth 2.0 Client ID**
3. Choose **Web application**
4. Under **Authorized JavaScript origins**, click **Add URI** and enter:
   ```
   https://your-site-name.netlify.app
   ```
   *(use your actual Netlify URL)*
5. Also add `http://localhost` for local testing
6. Click **Create**
7. **Copy your Client ID** — it looks like: `123456789-abc.apps.googleusercontent.com`

---

### Step 3 — Add Your Client ID to the App

1. Go to your forked GitHub repository
2. Click on `index.html`
3. Click the **pencil icon** (Edit file)
4. Find this line (near the top of the `<script>` section):
   ```javascript
   const HARDCODED_CLIENT_ID = '';
   ```
5. Replace it with your Client ID:
   ```javascript
   const HARDCODED_CLIENT_ID = '123456789-abc.apps.googleusercontent.com';
   ```
6. Scroll down → click **Commit changes**
7. Netlify will automatically redeploy within ~30 seconds

---

### Step 4 — Test It

1. Visit your Netlify URL
2. Click **Continue with Google**
3. Sign in — you should land on your personal workspace
4. Done! 🎉

---

### Step 5 — Set Up Your Organization (Optional)

See the full [Organization Setup Guide](SETUP.md) for:
- Creating an org with a dedicated Google account
- Inviting members
- Managing roles and permissions
- Hidden projects and collaborators

---

## Installing as an App (PWA)

FlowBoard can be installed on any device like a native app.

| Platform | How to install |
|---|---|
| **Chrome / Edge (Desktop)** | Click the install icon in the address bar |
| **iPhone / iPad** | Safari → Share → Add to Home Screen |
| **Android** | Chrome → three-dot menu → Install app |

---

## Roles & Permissions

| Role | Can do |
|---|---|
| **Owner** | Everything. Created the org. |
| **Admin** | Invite/remove members, manage all projects, mark projects hidden |
| **Member** | Create projects, manage their own project's collaborators |
| **Collaborator** | View and work on specific hidden projects they've been added to |

---

## Troubleshooting

| Problem | Fix |
|---|---|
| Sign in shows error | Make sure your Netlify URL is added as an Authorized JavaScript Origin in Google Cloud |
| Projects not loading | Sign out and back in — your session may have expired |
| Can't see org after being invited | Sign out and back in |
| Changes not saving | Check your internet connection — saves go directly to Google Drive |
| PWA install option not showing | Must be on HTTPS — Netlify provides this by default |

---

## Technology

| | |
|---|---|
| **Frontend** | Vanilla HTML/CSS/JavaScript — no build tools, no dependencies |
| **Auth** | Google OAuth 2.0 via `apis.google.com/js/api.js` |
| **Storage** | Google Drive API v3 |
| **Hosting** | Netlify (free tier) |
| **Cost** | $0 |

---

## License

MIT License — free to use, modify, and distribute.

---

*Built with Google Drive API · Hosted on Netlify · No tracking · No ads · No data collection*
