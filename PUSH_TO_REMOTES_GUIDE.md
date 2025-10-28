# 🚀 Push to Remote Repositories Guide

## ✅ What's Already Done

1. ✅ Enhanced `.gitignore` with comprehensive security rules
2. ✅ Created Corporate GitHub repository
3. ✅ Added both remote URLs (corp and personal)
4. ✅ Local git repository is ready with v1.0 and v2.0 tags

---

## 📍 Repository URLs

### Corporate GitHub (Already Created)
- **URL:** https://git.corp.adobe.com/vivekj/jira-epic-description-prompts
- **SSH:** git@git.corp.adobe.com:vivekj/jira-epic-description-prompts.git
- **Remote name:** `corp`
- **Status:** ✅ Repository created and ready

### Personal GitHub (Needs to be Created)
- **URL:** https://github.com/vivekjain/jira-epic-description-prompts
- **SSH:** git@github.com:vivekjain/jira-epic-description-prompts.git
- **Remote name:** `personal`
- **Status:** ⚠️ Needs to be created manually

---

## 🔑 Step 1: Set Up SSH Keys (If Not Already Done)

### Check if SSH keys exist:
```bash
ls -la ~/.ssh/
```

Look for files like `id_rsa` or `id_ed25519` (private key) and `id_rsa.pub` or `id_ed25519.pub` (public key).

### If SSH keys don't exist, create them:

#### For Corporate GitHub:
```bash
ssh-keygen -t ed25519 -C "vivekjain@adobe.com" -f ~/.ssh/id_ed25519_corp
```

#### For Personal GitHub:
```bash
ssh-keygen -t ed25519 -C "your-personal-email@example.com" -f ~/.ssh/id_ed25519_personal
```

### Add SSH keys to ssh-agent:
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519_corp
ssh-add ~/.ssh/id_ed25519_personal
```

### Configure SSH config file:
```bash
cat >> ~/.ssh/config << 'EOF'

# Corporate GitHub
Host git.corp.adobe.com
  HostName git.corp.adobe.com
  User git
  IdentityFile ~/.ssh/id_ed25519_corp
  IdentitiesOnly yes

# Personal GitHub
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_personal
  IdentitiesOnly yes
EOF
```

### Add public key to Corporate GitHub:
```bash
# Copy the public key
cat ~/.ssh/id_ed25519_corp.pub | pbcopy

# Then go to: https://git.corp.adobe.com/settings/keys
# Click "New SSH Key" and paste
```

### Add public key to Personal GitHub:
```bash
# Copy the public key
cat ~/.ssh/id_ed25519_personal.pub | pbcopy

# Then go to: https://github.com/settings/keys
# Click "New SSH Key" and paste
```

### Test SSH connections:
```bash
ssh -T git@git.corp.adobe.com
ssh -T git@github.com
```

---

## 🏗️ Step 2: Create Personal GitHub Repository

1. Go to: https://github.com/new
2. **Repository name:** `jira-epic-description-prompts`
3. **Description:** AI prompts for automated EPIC description generation in Jira
4. **Visibility:** Choose Public or Private
5. **DO NOT initialize with README** (we already have content)
6. Click **Create repository**

---

## 📤 Step 3: Push to Both Remotes

### Push to Corporate GitHub:
```bash
cd "/Users/vivekjain/.cursor/Jira Prompt"
git push corp master:main --tags
```

### Push to Personal GitHub:
```bash
cd "/Users/vivekjain/.cursor/Jira Prompt"
git push personal master --tags
```

### Set up tracking branches (optional):
```bash
# For corp
git branch --set-upstream-to=corp/main master

# For personal
git push personal master:main --tags
git branch --set-upstream-to=personal/main master
```

---

## 🔄 Step 4: Future Updates (Push to Both)

### Create a convenient alias:
```bash
# Add to ~/.zshrc or ~/.bashrc
alias gitpushboth='git push corp master:main && git push personal master:main'
```

### Or create a script:
```bash
cat > "/Users/vivekjain/.cursor/Jira Prompt/push_both.sh" << 'EOF'
#!/bin/bash
echo "🚀 Pushing to Corporate GitHub..."
git push corp master:main --tags
if [ $? -eq 0 ]; then
    echo "✅ Corporate GitHub push successful"
else
    echo "❌ Corporate GitHub push failed"
    exit 1
fi

echo ""
echo "🚀 Pushing to Personal GitHub..."
git push personal master:main --tags
if [ $? -eq 0 ]; then
    echo "✅ Personal GitHub push successful"
else
    echo "❌ Personal GitHub push failed"
    exit 1
fi

echo ""
echo "🎉 Successfully pushed to both remotes!"
EOF

chmod +x "/Users/vivekjain/.cursor/Jira Prompt/push_both.sh"
```

Then use it:
```bash
cd "/Users/vivekjain/.cursor/Jira Prompt"
./push_both.sh
```

---

## 📊 Verify Push Success

### Check Corporate GitHub:
```bash
open https://git.corp.adobe.com/vivekj/jira-epic-description-prompts
```

### Check Personal GitHub:
```bash
open https://github.com/vivekjain/jira-epic-description-prompts
```

### Verify tags were pushed:
Both repositories should show:
- ✅ v1.0 tag
- ✅ v2.0 tag
- ✅ All 5 commits
- ✅ All documentation files
- ✅ Examples folder with 6 HTML files

---

## 🔍 Current Remote Configuration

```bash
cd "/Users/vivekjain/.cursor/Jira Prompt"
git remote -v
```

**Expected output:**
```
corp      git@git.corp.adobe.com:vivekj/jira-epic-description-prompts.git (fetch)
corp      git@git.corp.adobe.com:vivekj/jira-epic-description-prompts.git (push)
personal  git@github.com:vivekjain/jira-epic-description-prompts.git (fetch)
personal  git@github.com:vivekjain/jira-epic-description-prompts.git (push)
```

---

## 🛡️ Security Check Before Pushing

Run this to ensure no sensitive data will be pushed:
```bash
cd "/Users/vivekjain/.cursor/Jira Prompt"

# Check what will be pushed
git ls-files

# Ensure .gitignore is working
git status --ignored

# Check for any token files
find . -type f -name "*token*" -o -name "*TOKEN*" -o -name "*.env"
```

**The .gitignore is configured to block:**
- ✅ Tokens and credentials
- ✅ Environment files (.env)
- ✅ SSH keys (.key, .pem, .pfx)
- ✅ Config with sensitive data
- ✅ Personal notes

---

## 🎯 Quick Command Summary

```bash
# 1. Test SSH (if not already done)
ssh -T git@git.corp.adobe.com
ssh -T git@github.com

# 2. Push to Corp GitHub
cd "/Users/vivekjain/.cursor/Jira Prompt"
git push corp master:main --tags

# 3. Create personal repo on github.com
# (Manual step via web interface)

# 4. Push to Personal GitHub
git push personal master:main --tags

# 5. Verify
open https://git.corp.adobe.com/vivekj/jira-epic-description-prompts
open https://github.com/vivekjain/jira-epic-description-prompts
```

---

## ⚠️ Troubleshooting

### "Permission denied (publickey)"
- SSH keys not set up or not added to GitHub
- Follow Step 1 above to set up SSH keys

### "Repository not found" (for personal)
- Personal GitHub repo not created yet
- Follow Step 2 to create it

### "Updates were rejected"
- Remote has changes not in local
- Run: `git pull corp main --rebase` or `git pull personal main --rebase`

### Want to use HTTPS instead of SSH?
```bash
# For corp (requires git credentials)
git remote set-url corp https://git.corp.adobe.com/vivekj/jira-epic-description-prompts.git

# For personal (requires personal access token)
git remote set-url personal https://github.com/vivekjain/jira-epic-description-prompts.git
```

---

## 📍 Final Repository Locations

Once pushed, your code will be available at:

### 🏢 Corporate (Internal)
```
https://git.corp.adobe.com/vivekj/jira-epic-description-prompts
```

### 🌐 Personal (Public/Private - your choice)
```
https://github.com/vivekjain/jira-epic-description-prompts
```

### 💻 Local
```
/Users/vivekjain/.cursor/Jira Prompt/
```

---

## 🎉 When Complete

Both remotes will have:
- ✅ v1.0 and v2.0 tags
- ✅ Complete version history
- ✅ All documentation
- ✅ Example HTML files
- ✅ Enhanced .gitignore for security
- ✅ 5 commits with meaningful messages

---

**Need Help?** Check:
- Corporate GitHub Docs: https://git.corp.adobe.com/help
- Personal GitHub Docs: https://docs.github.com

© 2025 Adobe. All rights reserved.

