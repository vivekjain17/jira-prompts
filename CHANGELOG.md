# EPIC Description Generation Prompt - Changelog

All notable changes to the EPIC Description Generation Prompt are documented in this file.

---

## [v2.0] - October 17, 2025

### 🐛 Critical Bug Fixes

#### Story Points Field Correction (CRITICAL)
**Issue:** Using wrong custom field for story points caused incorrect data.

**Before (Wrong):**
```python
❌ field: "customfield_10016"  # Wrong field!
❌ Trying to sum story points from child tickets
```

**After (Correct):**
```python
✅ JQL: cf[10003]              # Use in JQL queries
✅ Fields: customfield_10003   # Use in fields array
✅ Read directly from EPIC level, never sum from children
```

**Impact:** Story point calculations were completely wrong. Now fixed with correct field ID.

### ✨ New Features

#### 1. Jira Custom Fields Reference Section
Added comprehensive reference table for all STK project custom fields:

| Field Name | Custom Field ID | Usage |
|------------|----------------|-------|
| **Story Points** | `cf[10003]` | Story points on EPICs and tickets |
| Team | `cf[12900]` | Team assignment |
| Parent Link | `cf[21401]` | Links Initiative to EPIC |
| Epic Link | `cf[11800]` | Links Story/Bug/Task to EPIC |
| Target End | `cf[25801]` | Expected completion date |
| Beta Date | `cf[20000]` | AB test start date |
| Flagged | `cf[10001]` | "Yes" = crucial business value |

#### 2. Ensuring Consistency Across Runs
Comprehensive guide covering 8 key areas:

- **Follow the Exact Sequence**: Standardized 6-step source checking
- **Use Consistent Jira Queries**: Standardized JQL with correct fields
- **Use Consistent Confluence Searches**: Two-query approach
- **Template Adherence**: Mandatory sections for both modes
- **Information Quality Indicators**: High/Medium/Low confidence scoring
- **Handling Edge Cases**: Parent/child EPICs, programs, multi-phase
- **Quality Assurance Checklist**: 8-point pre-generation checklist
- **Troubleshooting Guide**: Common issues and solutions

### 📝 Documentation Updates

- Added "Common Mistakes to Avoid" section
- Added troubleshooting guide for API issues, missing data, formatting
- Added consistency validation examples
- Updated all JQL examples to use correct custom fields

### 🔧 Technical Improvements

- Standardized Jira query patterns
- Consistent field arrays across all queries
- Explicit instructions to avoid wrong custom field IDs
- Better error handling guidance

---

## [v1.1] - October 17, 2025

### ✨ Major Features

#### 1. Two Description Modes

**Mode 1: Detailed Description (Default)**
- Purpose: Comprehensive documentation for all stakeholders
- Template: Full STK-68219 template structure
- Length: 1000-3000 words typical
- Sections: Business Value, Success Metrics, Context, Implementation Scope, Technical Requirements, Timeline, References
- Use Cases: Complete documentation, stakeholder alignment, historical reference

**Mode 2: Short Description**
- Purpose: Executive summary and quick reference
- Template: Condensed format focusing on essentials
- Length: **Under 300 words** (max 500 words when needed)
- Sections: Business Value, Success Metrics, Scope, Context, References
- Use Cases: Quick updates, executive reviews, sprint planning

**How to Use:**
- `"Generate a description for STK-XXXXX"` → Detailed mode (default)
- `"Generate a SHORT description for STK-XXXXX"` → Short mode

#### 2. GitHub PR Link Discovery Enhancement

**Previous Behavior:**
- Only checked Story/Bug/Task descriptions for GitHub links
- Often missed PR links added via automation

**New Behavior:**
- **Checks Story/Bug/Task COMMENTS** for GitHub PR links
- Looks for Adobe Stock Jira bot that adds PR links
- Parses comment tables with format: `Author | Pull Request | PR Status`

**Pattern Recognition:**
- URL pattern: `https://git.corp.adobe.com/AdobeStock/*/pull/*`
- Table format detection
- Merged PR status tracking

**Process:**
1. Retrieve all Stories linked to EPIC
2. Call `mcp_Corp_Jira_get_jira_comments` for each Story/Bug/Task
3. Parse comments to extract GitHub PR links
4. Use `mcp_Corp_GitHub_get_pull_request` to get PR details
5. Use `mcp_Corp_GitHub_get_pull_request_files` to see implementation
6. Extract technical context and architectural decisions

**Benefits:**
- More complete technical context
- Better understanding of implementation approach
- Architectural decisions documented in PRs
- Code changes indicating feature scope

#### 3. One-Click Copy Button in HTML Output

**New HTML Features:**
- Prominent "📋 Copy Description" button above proposed description
- One-click copying to clipboard
- Visual feedback when copied (green checkmark, success notification)
- Automatically resets after 3 seconds

**User Experience:**
1. Open HTML review file in browser
2. Review the formatted description
3. Click "📋 Copy Description" button
4. Description copied to clipboard (ready for Jira)
5. Visual confirmation: "✓ Description copied to clipboard!"
6. Paste directly into Jira description field

**Technical Implementation:**
```javascript
function copyToClipboard() {
    const descElement = document.getElementById('descriptionContent');
    const text = descElement.innerText;
    
    // Create temporary textarea for clipboard access
    const textarea = document.createElement('textarea');
    textarea.value = text;
    textarea.style.position = 'fixed';
    textarea.style.opacity = '0';
    document.body.appendChild(textarea);
    textarea.select();
    
    document.execCommand('copy');
    
    // Show success notification and update button
    // Auto-reset after 3 seconds
    
    document.body.removeChild(textarea);
}
```

**Styling:**
- Adobe Red (#EB1000) primary button
- Success green (#0AA35B) when copied
- Smooth transitions and animations
- Mobile-responsive design

### 📝 Updated Process Flow

```
1. Receive EPIC ID(s) and mode (detailed or short)
   ↓
2. Retrieve EPIC from Jira
   ↓
3. Check current description (empty/template/real data?)
   ↓
4. Search sources in order (1-6):
   - Wiki pages (mentioned in)
   - Figma files (attachments)
   - Stories (descriptions)
   - GitHub PRs (in Story COMMENTS) ← NEW!
   - Confluence (search)
   - Other sources
   ↓
5. Aggregate all findings
   ↓
6. Generate description (detailed or short mode)
   ↓
7. Create HTML review file with copy button ← NEW!
   ↓
8. Present to user for review
   ↓
9. If approved → Update Jira
```

### ⚠️ Updated Critical Reminders

- NEVER assume or fabricate data
- ALWAYS check current description before overwriting
- ALWAYS output HTML for review before updating
- ALWAYS get permission before updating Jira
- ALWAYS follow the appropriate template (detailed vs short)
- ALWAYS maintain consistency across multiple EPICs
- **ALWAYS check Story/Bug/Task COMMENTS for GitHub PR links** ← NEW!
- **ALWAYS include copy button in HTML output** ← NEW!

---

## [v1.0] - Initial Release

### Core Features

#### Information Gathering Process (6-Step Sequential Order)

1. **Wiki Pages**: Check "mentioned in" section for linked pages
2. **Figma Files**: Review attached Figma files for design context
3. **Stories**: Check descriptions of Stories within EPIC
4. **GitHub Files**: Check for GitHub links in Story/Bug/Task tickets
5. **Confluence**: Search based on EPIC title/summary and Jira ID
6. **Other Sources**: Images, documents, attachments

#### Template Structure

Based on STK-68219 template:
- Business Value
- Success Metrics
- Context
- Implementation Scope
- Technical Requirements
- Timeline
- Dependencies
- References

#### Description Management Rules

- **Append** to existing non-empty descriptions
- **Override** empty template descriptions
- **Add template** if description is empty and no details found
- **Never delete** existing meaningful content
- **Maintain consistency** for bulk operations

#### Output Format

- HTML review file required before any Jira update
- Must seek permission before updating tickets
- Professional formatting with all sections
- Source documentation included

#### Quality Standards

- **No assumptions**: If info not found, state EPIC ID and insufficient information
- **Template adherence**: Follow STK-68219 structure
- **Professional tone**: Well-formatted business documentation
- **Complete attribution**: Document all sources used

#### Reference Examples

- **STK-68219**: Template structure to follow
- **STK-129540**: Example of good description content (cannot be copied verbatim)

---

## Benefits Summary

### For Users
✅ **Flexibility**: Choose detail level based on need  
✅ **Efficiency**: Short descriptions save time for simple updates  
✅ **Completeness**: GitHub PRs provide better technical context  
✅ **Convenience**: One-click copy eliminates formatting errors  
✅ **Consistency**: Same results every run with standardized process

### For Quality
✅ **Better Information**: GitHub PRs reveal implementation details  
✅ **Consistency**: Template ensures uniform structure  
✅ **Accuracy**: No manual copy-paste errors, correct custom fields  
✅ **Traceability**: All sources documented  
✅ **Reliability**: Correct story points and custom field usage

### For Process
✅ **Faster Reviews**: Short mode for quick approvals  
✅ **Detailed Archive**: Detailed mode for documentation  
✅ **Bulk Operations**: Consistent across multiple EPICs  
✅ **Easy Updates**: Copy button streamlines Jira updates  
✅ **Predictable**: Same inputs = same outputs

---

© 2025 Adobe. All rights reserved.

