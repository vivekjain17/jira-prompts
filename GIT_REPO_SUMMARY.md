# Jira Prompt - Git Repository Summary

## 📍 Repository Location
```
/Users/vivekjain/.cursor/Jira Prompt/
```

## 📁 Repository Structure

```
Jira Prompt/
├── .git/                           # Git repository
├── .gitignore                      # Git ignore rules
├── README.md                       # Main documentation
├── EPIC_Description_Generation_Prompt.md  # Core prompt (v2.0)
├── USAGE_EXAMPLES.md              # Usage examples
├── CHANGELOG.md                    # Complete version history
├── GIT_REPO_SUMMARY.md            # This file
└── examples/                       # Example HTML outputs
    ├── STK-119963_EPIC_Description_Review.html (Detailed)
    ├── STK-124663_EPIC_Description_Review.html (Detailed)
    ├── STK-124663_Short_Description_Review.html (Short)
    ├── STK-122640_Short_Description_Review.html (Short)
    ├── STK-125561_Short_Description_Review.html (Short)
    └── STK-123409_Short_Description_Review.html (Short)
```

## 🏷️ Version Tags

### v1.0 (Initial Release)
**Tag:** `v1.0`  
**Commit:** `3c7ac07`

**Features:**
- Initial release with detailed and short description modes
- Information gathering workflow from 6+ sources
- HTML review file generation with Adobe branding
- Copy-to-clipboard functionality
- Template adherence (STK-68219 structure)
- GitHub PR discovery from Story/Bug/Task comments

### v2.0 (Current - Production Ready)
**Tag:** `v2.0`  
**Commit:** `f64b966`

**New Features:**
- ✅ Fixed: Story points field corrected to `cf[10003]` (critical bug fix)
- ✅ Added: Jira Custom Fields Reference section
- ✅ Added: "Ensuring Consistency Across Runs" section
- ✅ Added: 8-point troubleshooting guide
- ✅ Added: Quality assurance checklist
- ✅ Added: Edge case handling guidelines

## 📊 Git History

```bash
f64b966 (HEAD -> master, tag: v2.0) v2.0: Critical fixes and consistency improvements
3c7ac07 (tag: v1.0) v1.0: Initial release of EPIC Description Generation Prompt
```

## 🔄 Version Access

### To view v1.0:
```bash
cd "/Users/vivekjain/.cursor/Jira Prompt"
git checkout v1.0
```

### To return to v2.0 (current):
```bash
cd "/Users/vivekjain/.cursor/Jira Prompt"
git checkout master
# or
git checkout v2.0
```

### To see differences between versions:
```bash
git diff v1.0 v2.0
```

### To view version history:
```bash
git log --oneline --decorate --all
```

### To list all tags:
```bash
git tag -l
```

## 📝 Key Improvements in v2.0

### 1. Critical Bug Fix
**Problem:** Story points were being read from wrong custom field (`customfield_10016`)  
**Solution:** Corrected to `cf[10003]` in JQL and `customfield_10003` in fields array

### 2. Jira Custom Fields Reference
Complete reference table for all STK project custom fields:
- Story Points: `cf[10003]`
- Team: `cf[12900]`
- Parent Link: `cf[21401]`
- Epic Link: `cf[11800]`
- Target End: `cf[25801]`
- Beta Date: `cf[20000]`
- Flagged: `cf[10001]`

### 3. Consistency Mechanisms
- Exact sequence for source checking
- Standardized Jira queries
- Consistent Confluence searches
- Template adherence rules
- Information quality indicators
- Edge case handling
- QA checklist
- Troubleshooting guide

## 🚀 Usage

### Using the Current Version (v2.0)
The repository is currently on v2.0 (master branch). Simply refer to:
```
EPIC_Description_Generation_Prompt.md
```

### Switching Between Versions
Use git tags to switch between versions:
- `git checkout v1.0` - Original release
- `git checkout v2.0` - Current production version

## 📚 Documentation Files

| File | Purpose |
|------|---------|
| `README.md` | Main documentation and overview |
| `EPIC_Description_Generation_Prompt.md` | Core prompt with complete instructions |
| `USAGE_EXAMPLES.md` | Practical usage examples |
| `CHANGELOG.md` | Complete version history and changes |
| `GIT_REPO_SUMMARY.md` | This file - repository summary |

## 🔍 Quality Assurance

### Consistency Features (v2.0)
- ✅ Standardized information gathering sequence
- ✅ Consistent Jira query patterns
- ✅ Template adherence enforcement
- ✅ Quality indicators (High/Medium/Low confidence)
- ✅ Edge case handling
- ✅ Pre-generation checklist
- ✅ Troubleshooting guide

### Testing
All examples in `examples/` folder demonstrate:
- Detailed descriptions (STK-119963, STK-124663)
- Short descriptions (STK-124663, STK-122640, STK-125561, STK-123409)
- HTML review output format
- Copy-to-clipboard functionality

## 🎯 Next Steps

1. **Use v2.0 for production** - It includes critical bug fixes
2. **Review CHANGELOG.md** - Complete version history
3. **Check examples/** - HTML output samples
4. **Use git tags** - Easy version switching

## 📞 Support

For questions or issues:
1. Check `CHANGELOG.md` for version-specific changes
2. Review `USAGE_EXAMPLES.md` for practical examples
3. Consult troubleshooting section in main prompt (v2.0)

---

**Repository Initialized:** October 28, 2025  
**Current Version:** v2.0  
**Status:** Production Ready ✅

© 2025 Adobe. All rights reserved.

