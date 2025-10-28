# 🔄 Repository Rename - Final Steps

## ✅ What's Already Done

1. ✅ Files reorganized into `docs/` folder
2. ✅ README updated with new structure
3. ✅ New Corp GitHub repo created: `jira-prompts`
4. ✅ Git remotes updated to new URLs
5. ✅ All changes committed locally

---

## 🚀 Steps to Complete (3-5 minutes)

### Step 1: Add SSH Key to Agent & Push to Corp
```bash
# Add your SSH key (you'll need to enter passphrase)
ssh-add ~/.ssh/id_ed25519_adobe

# Verify it's added
ssh -T git@git.corp.adobe.com

# Push to new corp repo
cd "/Users/vivekjain/.cursor/Jira Prompt"
git push corp master:main --tags
```

**Expected result:** All commits and tags pushed to new `jira-prompts` repo

---

### Step 2: Create New Personal GitHub Repository

1. Go to: https://github.com/new
2. **Repository name:** `jira-prompts` (changed from jira-epic-description-prompts)
3. **Description:** Collection of AI prompts for Jira automation tasks
4. **Visibility:** Public or Private (your choice)
5. **Important:** DO NOT initialize with README
6. Click **"Create repository"**

---

### Step 3: Push to Personal GitHub
```bash
cd "/Users/vivekjain/.cursor/Jira Prompt"
git push personal master:main --tags
```

---

### Step 4: Rename Local Folder (Optional but Recommended)
```bash
cd /Users/vivekjain/.cursor/
mv "Jira Prompt" "jira-prompts"
cd jira-prompts
```

---

### Step 5: Delete Old Repositories (After Verifying New Ones Work)

#### Delete old Corp GitHub repo:
```bash
# Go to: https://git.corp.adobe.com/vivekj/jira-epic-description-prompts/settings
# Scroll to "Danger Zone"
# Click "Delete this repository"
```

#### Delete old Personal GitHub repo:
```bash
# Go to: https://github.com/vivekjain17/jira-epic-description-prompts/settings
# Scroll to "Danger Zone"  
# Click "Delete this repository"
```

---

## 📍 New Repository URLs

### Corporate GitHub
```
https://git.corp.adobe.com/vivekj/jira-prompts
```

### Personal GitHub
```
https://github.com/vivekjain17/jira-prompts
```

---

## 📊 What Changed

### Repository Name:
- **Old:** `jira-epic-description-prompts`
- **New:** `jira-prompts`
- **Why:** More generic name for adding future Jira prompts

### File Structure:
```
jira-prompts/                          (new name)
├── README.md                          (root)
├── CHANGELOG.md                       (root)
├── docs/                              ← NEW FOLDER
│   ├── EPIC_Description_Generation_Prompt.md
│   ├── USAGE_EXAMPLES.md
│   ├── GIT_REPO_SUMMARY.md
│   ├── SETUP_COMPLETE.md
│   ├── PUSH_TO_REMOTES_GUIDE.md
│   └── REPOSITORY_STATUS.md
└── examples/
    └── *.html (6 files)
```

**Benefits:**
- ✅ Cleaner root directory
- ✅ Easy to add new prompt types (e.g., `docs/Bug_Triage_Prompt.md`)
- ✅ Scalable for future growth
- ✅ Better organization

---

## 🎯 Quick Commands Summary

```bash
# 1. Add SSH key
ssh-add ~/.ssh/id_ed25519_adobe

# 2. Push to corp
cd "/Users/vivekjain/.cursor/Jira Prompt"
git push corp master:main --tags

# 3. Create personal repo at github.com/new

# 4. Push to personal
git push personal master:main --tags

# 5. Rename local folder (optional)
cd /Users/vivekjain/.cursor/
mv "Jira Prompt" "jira-prompts"

# 6. Verify both repos
open https://git.corp.adobe.com/vivekj/jira-prompts
open https://github.com/vivekjain17/jira-prompts

# 7. Delete old repos (after verification)
# Use web interface danger zone
```

---

## ✅ Verification Checklist

After pushing to both remotes, verify:

- [ ] Corp GitHub shows new structure with `docs/` folder
- [ ] Personal GitHub shows new structure with `docs/` folder
- [ ] Both repos have v1.0 and v2.0 tags
- [ ] Both repos have all 8 commits (including the refactor commit)
- [ ] README displays correctly on both repos
- [ ] Examples folder is visible on both repos
- [ ] Local folder renamed to `jira-prompts` (optional)
- [ ] Old repositories deleted (after confirmation)

---

## 🔮 Future: Adding More Prompts

With the new structure, adding new Jira prompts is easy:

```bash
cd "/Users/vivekjain/.cursor/jira-prompts"

# Create new prompt file
cat > docs/Bug_Triage_Prompt.md << 'EOF'
# Bug Triage Automation Prompt
...
EOF

# Commit and push
git add docs/Bug_Triage_Prompt.md
git commit -m "feat: Add bug triage automation prompt"
git push corp master:main
git push personal master:main
```

---

## 🎊 When Complete

You'll have:
- ✅ Clean, organized repository structure
- ✅ Generic name for future expansion  
- ✅ Better documentation organization
- ✅ Same content, better structure
- ✅ Ready to add more Jira prompts

---

**Status:** Ready to push with new structure  
**Commits:** 8 total (including refactor)  
**New Repos:** Created and configured  
**Old Repos:** Safe to delete after verification

© 2025 Adobe. All rights reserved.

