
# 🔐 GitHub SSH Setup Guide (Personal Account)

This guide helps you configure SSH on your system to securely connect to your **personal GitHub account**.

---

## 🎯 Goal

Enable secure and password-less access to GitHub using SSH on a single system.

---

## ✅ Prerequisites

- Git Bash (Windows) or Terminal (Mac/Linux)
- GitHub account (we're setting up SSH for your **personal** account)
- Internet access

---

## 🪜 Step 1: Check for Existing SSH Keys

```bash
ls ~/.ssh
```

**Why:** Ensures no existing SSH keys (like `id_ed25519`) will be overwritten.

---

## 🪜 Step 2: Generate a New SSH Key

```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

- `-t ed25519`: Modern, secure key type
- `-C`: Adds your email to help identify the key

You'll be prompted:

```
Enter file in which to save the key (/c/Users/YOURNAME/.ssh/id_ed25519):
```

👉 **Press Enter** to accept the default location.

Then:

```
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```

👉 **Press Enter twice** to skip passphrase (recommended for simplicity)

---

## 🪜 Step 3: Start the SSH Agent and Add the Key

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

**Why:** Loads your SSH key into memory so Git can use it without prompting.

---

## 🪜 Step 4: Copy Your Public Key

```bash
cat ~/.ssh/id_ed25519.pub
```

👉 Copy the full output that starts with `ssh-ed25519` and ends with your email.

---

## 🪜 Step 5: Add the SSH Key to GitHub

1. Go to [GitHub SSH Keys](https://github.com/settings/keys)
2. Click **"New SSH key"**
3. Add:
   - **Title**: e.g., `CMS-PC`
   - **Key**: Paste the key from Step 4
4. Click **"Add SSH key"**

**Why:** Tells GitHub that your computer is authorized to access your repositories.

---

## 🪜 Step 6: Test the SSH Connection

```bash
ssh -T git@github.com
```

If successful, you'll see:

```
Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.
```

If prompted:

```
Are you sure you want to continue connecting (yes/no)?
```

👉 Type `yes` and press Enter

---

## 🪜 Step 7: Use SSH to Clone or Connect Repos

### To clone a repo:
1. Go to the repo on GitHub
2. Click **"Code"** → select **SSH**
3. Run:

```bash
git clone git@github.com:your-username/your-repo.git
```

### To set SSH remote for an existing repo:

```bash
cd your-project-folder
git remote set-url origin git@github.com:your-username/your-repo.git
```

---

## ✅ You're Done!

You can now push/pull/clone repos from your **personal GitHub account** using SSH — no username/password required.

---

## 📌 Next Steps (Optional)

- Want to set up a second GitHub (e.g., work/org) account on the same system?
- Need SSH config to manage both accounts at once?

Let us know and continue with the advanced setup guide.
