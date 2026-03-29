# Taskie — Organization Setup Guide

Everything your organization needs to do after Taskie is deployed.

---

## Before You Start — The Dedicated Account Model

**❌ Don't do this:** Create the org while signed in as `mark@company.com`. If Mark leaves, the org data is tied to his personal Google account.

**✅ Do this instead:** Create a dedicated Google account like `yourcompany.taskie@gmail.com`. The company shares this account. Nobody personally owns the org — the company does.

This takes 2 extra minutes and prevents problems forever.

---

## Step 1 — Create a Dedicated Google Account

1. Go to [accounts.google.com](https://accounts.google.com) → **Create account**
2. Use something like `yourcompany.taskie@gmail.com`
3. Store the credentials in a shared password manager (1Password, Bitwarden, etc.)
4. Make sure at least 2 admins have access to these credentials

---

## Step 2 — Sign In and Create the Org

1. Open Taskie and sign in with the **dedicated account**
2. On first sign in, Google will ask you to grant permissions — click **Allow**
   - This grants Drive and Calendar access for the dedicated account
3. Click the **Org** tab in the sidebar
4. Click **Create Org**
5. Enter your org name and description
6. Click **Create Organization**

The org data is now stored in the dedicated account's Google Drive under `Taskie/Organizations/`.

7. Sign out of Taskie

---

## Step 3 — Add Your Personal Account as Admin

1. Sign back into Taskie with your **personal work account**
   - You won't see the org yet — that's expected
2. Sign back in with the **dedicated account**
3. Go to your org → **Members** → **Invite Member**
4. Enter your personal work email, role = **Admin** → **Send Invite**
5. Sign out
6. Sign back in with your **personal account**
7. The org now appears — you're an admin

---

## Step 4 — Add a Second Admin (Important)

Always have at least 2 admins. If one person loses access, the other can still manage the org.

1. As admin on your personal account, go to org → **Members** → **Invite Member**
2. Add a second trusted person as **Admin**
3. Confirm they can see and access the org

---

## Step 5 — Invite Your Team

1. Go to org → **Members** → **Invite Member**
2. Enter each person's Google email
3. Choose role:
   - **Admin** — managers, IT admins, team leads who need full control
   - **Member** — everyone else
4. Repeat for each person

Members see the org the next time they sign into Taskie. They'll be prompted to grant Drive and Calendar permissions on first sign in.

---

## Step 6 — First Sign In for Each Member

Every new user signing into Taskie for the first time will see a Google consent screen asking for:

- **Google Drive** — to store project data in their own Drive
- **Google Calendar** — to sync task due dates to dedicated Taskie calendars
- **Profile & Email** — to identify them

They must click **Allow** for Taskie to work. If they dismiss the screen, they can sign out and back in to see it again.

---

## Managing Members

### Change a Member's Role
1. Go to org → **Members**
2. Find the person → change the role dropdown
3. Takes effect immediately

### Remove a Member
1. Go to org → **Members**
2. Click **Remove** next to their name
3. They no longer see the org on next sign in

### What if the dedicated account is lost?
Any existing Admin can still manage the org from their personal account. Contact your admin team to recover access to the dedicated account credentials in your password manager.

---

## Transferring Org Ownership

Use this when you need to move the org to a new person — for example, if someone is leaving the company.

### How it works

Taskie's 3-step ownership transfer:

**Step 1 — Select & Grant (in Taskie)**
1. Go to org → **Org Settings** → **Danger Zone** → **Transfer Ownership**
2. Select the new owner from the dropdown
3. Check **Transfer ownership of all org Drive files to the new owner**
4. Type `CONFIRM` → click **Grant Access & Continue**

Taskie immediately:
- Updates the new owner's role to Owner in org metadata
- Sends Google Drive ownership transfer requests for every org file

**Step 2 — New Owner Accepts (in Google Drive)**

Google requires the recipient to explicitly accept ownership — this cannot be bypassed.

The new owner must:
1. Open [Google Drive](https://drive.google.com)
2. Look for a notification or email: "Someone wants to transfer file ownership to you"
3. Click **Accept** for each file

Once they've accepted, come back to Taskie and click **Confirm Transfer Complete**.

**Step 3 — Finalize**

Taskie shows a summary of what transferred. You remain in the org as Admin.

⚠️ **Do not delete the original files from your Drive until the new owner confirms Taskie is working correctly for them.**

### If some files fail to transfer

The transfer dialog shows a log of each file. Any that show ✗ can be manually shared:
1. Open [Google Drive](https://drive.google.com)
2. Find the `Taskie/Organizations/` folder
3. Right-click → **Share** → add the new owner with **Editor** access
4. Then right-click again → **Transfer ownership**

---

## Projects

### Creating an Org Project
1. Go to your org → **New Project**
2. Set name, description, and visibility:
   - **Visible to all members** — everyone sees it
   - **Hidden** — only admins and assigned collaborators

### Hidden Projects
Use for sensitive, early-stage, or client-specific work.

To assign collaborators to a hidden project:
1. Open the project → click **Collaborators** (top right)
2. Check members who should have access → **Save**

### Editing Projects
- **Admins** can edit any project
- **Project creators** can edit their own
- **Members** can only edit projects they created

---

## Google Calendar Integration

When org members sync tasks to Google Calendar, Taskie automatically creates a dedicated **Taskie - [Org Name]** calendar. Tasks never appear in anyone's primary calendar.

Each org has its own dedicated calendar. The personal workspace has a separate **Taskie - My Projects** calendar.

**If calendars aren't appearing:**
1. Make sure Google Calendar API is enabled in the Google Cloud project
   - Google Cloud Console → APIs & Services → Library → Google Calendar API → Enable
2. Sign out of Taskie and back in (re-grants calendar permission with the current token)
3. Settings → **↺ Reset Calendar Cache** → try syncing again

---

## Roles Reference

| Action | Owner | Admin | Member |
|---|---|---|---|
| Create projects | ✓ | ✓ | ✓ |
| Edit any project | ✓ | ✓ | Own only |
| Delete any project | ✓ | ✓ | Own only |
| Mark project hidden | ✓ | ✓ | ✗ |
| Manage collaborators | ✓ | ✓ | Own projects only |
| Invite members | ✓ | ✓ | ✗ |
| Remove members | ✓ | ✓ | ✗ |
| Promote / demote roles | ✓ | ✓ | ✗ |
| Org settings | ✓ | ✓ | ✗ |
| Transfer ownership | ✓ | ✓ | ✗ |
| Delete org | ✓ | ✓ | ✗ |

---

## Personal vs Org Workspace

**Personal** — completely private. Even org admins cannot see your personal projects. Personal data lives only in your own Drive.

**Org** — shared workspace governed by the role permissions above.

Switch between them with the **Personal / Org** toggle at the top of the sidebar.

---

## Live Updates

Taskie polls for changes every 5 seconds when you're viewing an org project. If another user modifies a task, you'll see a toast notification and the view refreshes automatically. This works for both project content and org membership changes.

---

## New Organization Checklist

- [ ] Created dedicated Google account (`yourcompany.taskie@gmail.com`)
- [ ] Stored credentials in shared password manager
- [ ] Signed into Taskie with dedicated account, granted all permissions, created org
- [ ] Added at least one personal account as Admin
- [ ] Added a second Admin as backup
- [ ] Invited all team members
- [ ] Each member has signed in and granted permissions (Drive + Calendar)
- [ ] Created first org project
- [ ] Verified Google Calendar API is enabled in Google Cloud Console
- [ ] Shared Taskie URL with the team: `https://kylezwhite.github.io/Taskie`

---

*Questions? Open an issue on the GitHub repository.*
