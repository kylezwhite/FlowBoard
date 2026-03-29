# Taskie — Organization Setup Guide

This guide covers everything an organization needs to do after Taskie is deployed.

---

## The Dedicated Account Model

Before creating your organization, understand the recommended setup:

**❌ Don't do this:** Create the org while signed in as `mark@gmail.com`. If Mark ever leaves, the org is still tied to his personal Google account.

**✅ Do this instead:** Create a dedicated Google account like `acmecorp.taskie@gmail.com`. The company shares access to this account. Nobody "owns" the org personally — the company does.

This is how real companies handle this. It takes 2 extra minutes and prevents problems forever.

**However:** If you trust Mark, you can transfer ownership of organizations to different users.
---

## Step 1 — Create a Dedicated Google Account

1. Go to [accounts.google.com](https://accounts.google.com) and create a new Google account
2. Use an email like `yourcompany.taskie@gmail.com`
3. Store the credentials somewhere the whole admin team can access (e.g. a shared password manager like 1Password or Bitwarden)

---

## Step 2 — Create the Organization

1. Open Taskie and sign in with the **dedicated account** (not your personal account)
2. Click the **Org** tab in the left sidebar
3. Click **Create Org**
4. Fill in your organization name and description
5. Click **Create Organization**
6. Sign out of Taskie

> The org data is now stored in the dedicated account's Google Drive. Nobody's personal account owns it.

---

## Step 3 — Add Yourself as an Admin

1. Sign back into Taskie with your **personal work account**
2. You won't see the org yet — that's expected
3. Sign back in with the **dedicated account**
4. Go to your org → **Members** → **Invite Member**
5. Enter your personal work email
6. Set role to **Admin**
7. Click **Send Invite**
8. Sign out
9. Sign back in with your personal account — you'll now see the org

---

## Step 4 — Invite Your Team

Once you're an admin using your personal account:

1. Go to your org → **Members** → **Invite Member**
2. Enter each person's Google email address
3. Choose their role:
   - **Admin** — for people who manage the org (IT admins, managers, team leads)
   - **Member** — for everyone else
4. Click **Send Invite**
5. Repeat for each person

Invited users will see the organization the next time they sign into Taskie. No email is sent — they just need to know to sign in.

---

## Managing Members

### Promote a Member to Admin
1. Go to **Members** in the org sidebar
2. Find the person
3. Change their role dropdown from **Member** to **Admin**
4. Done — takes effect immediately

### Demote an Admin to Member
Same as above — change the dropdown to **Member**.

### Remove a Member
1. Go to **Members**
2. Click **Remove** next to their name
3. They will no longer see the org when they sign in

### What happens if the org owner account is lost?
If your team loses access to the dedicated account, any existing Admin can still manage the org through their personal account. The org data remains in Google Drive. Contact your admin team to regain access to the dedicated account credentials.

---

## Transferring Org Ownership

If you need to hand off the org to a different user (e.g. someone is leaving the company):

1. Go to your org → **Org Settings** → **Danger Zone**
2. Click **Transfer Ownership**
3. Select the new owner from the dropdown
4. Check **Grant new owner full write access to all org files** — this gives them Drive access to all org data
5. Follow the manual steps shown in the dialog to have the new owner copy the org folder to their Drive
6. Type **CONFIRM** and click **Transfer Ownership**

> **Important:** Do not delete the original org files from your Drive until the new owner confirms everything is working correctly in Taskie.

---

## Projects

### Creating an Org Project
1. Go to the org workspace
2. Click **New Project**
3. Fill in the name and description
4. Choose visibility:
   - **Visible to all members** — everyone in the org can see and work on it
   - **Hidden** — only admins and assigned collaborators can see it

### Hidden Projects
Use hidden projects for:
- Executive or sensitive work not relevant to the whole team
- Projects in early planning stages not ready to share
- Client work that should only be seen by the assigned team

To add collaborators to a hidden project:
1. Open the hidden project
2. Click **Collaborators** in the top right
3. Check the org members who should have access
4. Click **Save**

### Who can edit org projects?
- **Admins** can edit any project
- **Project creators** can edit their own projects
- **Members** can only edit projects they created

---

## Google Calendar Integration

When org members sync tasks to Google Calendar, Taskie automatically creates a shared calendar called **Taskie - [Org Name]**. This keeps org task deadlines separate from personal calendars and primary calendar clutter.

Each org gets its own dedicated calendar. Members see their synced tasks in that calendar alongside their personal **Taskie - My Projects** calendar.

---

## Roles Reference

| Action | Owner | Admin | Member |
|---|---|---|---|
| Create org projects | ✓ | ✓ | ✓ |
| Edit any project | ✓ | ✓ | Own only |
| Mark project hidden | ✓ | ✓ | ✗ |
| Manage collaborators | ✓ | ✓ | Own projects only |
| Invite members | ✓ | ✓ | ✗ |
| Remove members | ✓ | ✓ | ✗ |
| Promote/demote roles | ✓ | ✓ | ✗ |
| Delete any project | ✓ | ✓ | Own only |
| Transfer ownership | ✓ | ✓ | ✗ |
| Delete org | ✓ | ✓ | ✗ |

---

## Personal vs Org Workspace

Every user has two separate workspaces:

**Personal** — completely private. Nobody in your org can see your personal projects, even admins. Your personal data lives in your own Google Drive.

**Org** — shared workspace. Subject to the role permissions above.

Switch between them using the **Personal / Org** toggle at the top of the left sidebar.

---

## Checklist for New Organizations

- [ ] Created a dedicated Google account for the org (`yourcompany.taskie@gmail.com`)
- [ ] Signed into Taskie with dedicated account and created the org
- [ ] Added at least one personal account as Admin
- [ ] Added a second Admin (so there's always a backup)
- [ ] Invited all team members
- [ ] Shared dedicated account credentials with all admins securely
- [ ] Created first org project
- [ ] Shared Taskie URL with the team: `https://kylezwhite.github.io/Taskie`

---

*Questions? Open an issue on the GitHub repository.*
