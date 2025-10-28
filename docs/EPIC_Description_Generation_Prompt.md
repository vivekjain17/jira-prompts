# EPIC Description Generation Prompt

## Quick Reference

**Purpose:** Automatically generate EPIC descriptions (detailed or short) by gathering information from multiple sources (Wiki, Figma, Stories, GitHub, Confluence, etc.) and following Adobe Stock's standardized template.

**Description Modes:**
- 📖 **Detailed Description**: Comprehensive, following full STK-68219 template structure
- 📝 **Short Description**: Concise summary (under 300 words, max 500 words when needed)

**Key Principles:**
- ✅ Follow template from STK-68219 (detailed mode) or condensed format (short mode)
- ✅ Gather information from 6+ sources in sequential order
- ✅ Never assume or fabricate data
- ✅ Output HTML review file first, get permission before updating Jira
- ✅ Append to existing descriptions (don't overwrite real data)
- ✅ Maintain consistency across bulk operations

**Quick Start:**
1. Receive EPIC ID(s) and description mode from user (detailed or short)
2. Retrieve EPIC from Jira and check current description
3. Search information sources in order (Wiki → Figma → Stories → GitHub → Confluence → Other)
4. Generate description following appropriate template
5. Create HTML review file with Adobe branding and copy button
6. Get user approval before updating Jira

---

## Objective
Generate professional EPIC descriptions for Jira tickets by gathering information from multiple sources and following a standardized template. Support two modes:

### Mode 1: Detailed Description
- Comprehensive, thorough documentation following full STK-68219 template
- Includes all sections: Business Value, Success Metrics, Context, Implementation Scope, etc.
- Target audience: All stakeholders needing complete understanding
- Typical length: 1000-3000 words

### Mode 2: Short Description
- Concise, executive summary format
- Target length: **Under 300 words** (max 500 words when complexity requires)
- Focus: Business value, key deliverables, success metrics
- Target audience: Quick reference, status updates, executive reviews

## Information Gathering Process (Sequential Order)

### 1. Check Linked Wiki Pages
- **Location**: Look in the "mentioned in" section of the EPIC ticket
- **Action**: 
  - If wiki pages are found, read and extract relevant information
  - Use `mcp_Adobe_Wiki_Confluence_get_wiki_content` to retrieve content
  - Document key findings: business value, scope, context, metrics

### 2. Check Figma Files
- **Location**: Look for Figma attachments or links in the EPIC
- **Action**:
  - Use `mcp_Figma_get_figma_file` to analyze the design file
  - Extract: design intent, user flows, features being built, UI/UX goals
  - Use `mcp_Figma_get_figma_components` to understand component structure
  - Use `mcp_Figma_get_figma_styles` to understand design tokens

### 3. Check Stories within the EPIC
- **JQL Query**: `"Epic Link" = <EPIC_JIRA_ID>`
- **Action**:
  - Search all Stories, Bugs, Tasks linked to the EPIC
  - Read each Story's description field
  - Aggregate common themes, requirements, and acceptance criteria
  - Identify technical implementation details

### 4. Check GitHub Files Linked to Tickets
- **Location**: Look in **comments** of Story/Bug/Task tickets for GitHub PR links
  - GitHub links are typically found in ticket comments, not descriptions
  - Look for patterns like: `https://git.corp.adobe.com/AdobeStock/*/pull/*`
  - Check comments from the "Adobe Stock Jira account to add PR links in comments" bot
  - Example format: Table with columns "Author | Pull Request | PR Status"
- **Action**:
  - First, retrieve all comments from Stories: Use `mcp_Corp_Jira_get_jira_comments` for each Story/Bug/Task
  - Parse comments to extract GitHub PR links
  - Use `mcp_Corp_GitHub_get_pull_request` to get PR details (title, description, files changed)
  - Use `mcp_Corp_GitHub_get_pull_request_files` to see what was implemented
  - Use `mcp_Corp_GitHub_get_file_contents` to read specific files if needed for context
  - Extract technical context, implementation approach, architectural decisions
  - Document code changes that indicate feature scope

### 5. Search Confluence
- **Search Strategy**:
  - Use EPIC title/summary as search query
  - Use EPIC Jira ID as search query
  - Use `mcp_Adobe_Wiki_Confluence_search_wiki_content` with both queries
- **Action**:
  - Review all matching pages
  - Extract business requirements, project context, stakeholder information
  - Look for PRDs, technical specs, design docs

### 6. Check Other Sources
- **Images**: Look for attached images (screenshots, diagrams, mockups)
- **Documents**: Look for PDFs, Word docs, or other attachments
- **Comments**: Review EPIC comments for context and decisions
- **Links**: Check custom fields for external documentation links

## Template to Follow

**Reference EPIC**: STK-68219 (This is the template structure)

### Template Structure from STK-68219:

```
*EPIC INFORMATION*
||What||Link/Description||
|*SWAG Breakdown*| |
|*Summary of Work*| |
|*Requirements*| |
|*Definition of Done/Outcome of deliverable*| |
|*Acceptance criteria*| |
|*Metrics*| |
|*Designs*| |

Is PAR required? [https://wiki.corp.adobe.com/display/adobestock/Pricing+Action+Request+Process]

*Sign Offs:*
||Step||Owner||Status||Link||
|Product/Business Requirement Wiki| |  | |
|Design Document (Figma)| | | |
|Architecture Wiki| | | |
|Solution Design Wiki| | | |
|Analytics Requirements| | | |
|Test Plan Wiki| | | |

*Team*
{panel}
EM : []  | Epic Lead (EL) :[ ]
PgM : []  | PM : [ ]  | QE : [ ]
{panel}
```

### Mode Selection: Detailed vs Short

**User will specify which mode to use:**
- "Generate a description for STK-XXXXX" → Use **Detailed** mode (default)
- "Generate a short description for STK-XXXXX" → Use **Short** mode
- "Generate descriptions for [list]" → Use **Detailed** mode (default)
- "Generate short descriptions for [list]" → Use **Short** mode

## Short Description Template (Mode 2)

For short descriptions (under 300 words, max 500 words), use this condensed format:

```
h3. Business Value
[1-2 sentences: What problem does this solve? Why does it matter?]
• [Key business driver 1]
• [Key business driver 2]
• [Revenue/strategic impact if quantifiable]

h3. Success Metrics
• Primary: [Main KPI]
• Secondary: [Supporting metrics]

h3. Scope
[2-3 sentences summarizing what will be delivered]

Key deliverables:
• [Deliverable 1]
• [Deliverable 2]
• [Deliverable 3]

h3. Context
[1-2 sentences: Why now? Related initiatives?]
• Parent: [Parent EPIC if applicable]
• Related: [Related EPICs/dependencies]

h3. References
• [Link to requirements/design]
• [Link to wiki/confluence]
```

**Short Description Guidelines:**
- Focus on essentials: business value, deliverables, metrics
- Use bullet points for scanability
- Keep sentences concise and direct
- Prioritize quantifiable information
- Skip deep technical details unless critical
- Aim for <300 words, allow up to 500 words if complexity requires
- Still maintain professional tone and clarity

## Detailed Description Template (Mode 1)

### Recommended Sections for Content:

When populating the detailed template, organize gathered information into these logical sections:

```
## Business Value
[Clear statement of why this EPIC matters to the business, customers, or internal stakeholders]
- Revenue impact, strategic alignment, customer pain points addressed

## Success Metrics
[Quantifiable metrics that define success - KPIs, user adoption, performance improvements, etc.]
- Primary metrics (CVR, revenue, retention)
- Secondary metrics (usage, engagement)

## Context
[Background information, why now, related initiatives, dependencies]
- Strategic context, market drivers, related initiatives

## Implementation Scope
[What will be delivered, what's in scope, what's out of scope]
- Core deliverables, features, exclusions

## Technical Requirements
[If applicable: key technical constraints, architecture decisions, integrations]
- Architecture, integrations, technical constraints

## User Stories / Use Cases
[If applicable: who will use this, how will they use it, what problems does it solve]
- Target personas, user flows, problem/solution fit

## Timeline & Dependencies
[If applicable: key milestones, dependent EPICs/initiatives]
- Key dates, dependent work, blocking issues

## Success Criteria
[How we'll know this is done and successful]
- Acceptance criteria, done definition

## References
[Links to related documentation, EPICs, wiki pages]
- Parent EPICs, related work, documentation links
```

## Reference Example

**Good Description Example**: STK-129540
- This EPIC has a well-written description with good detail
- It demonstrates the level of information and professionalism required
- However, it doesn't strictly follow the template structure above
- Use it to understand what "vital information" looks like
- Do NOT copy text from this EPIC to other EPICs

### Actual Content from STK-129540:

```
*BUSINESS VALUE:*

*Revenue Growth & Monetization:*
 * Introduces new mid-tier pricing option ($79.99 ABM / $99.99 M2M) filling gap between 10-credit ($29.99) and Unlimited ($134.99) plans
 * Targets customers needing more than 10 credits but not ready for unlimited pricing
 * Creates granular pricing ladder to capture different customer segments and willingness to pay

*Video Asset Strategy & Premium Content Monetization:*
 * Strategically limits video entitlement to 3 videos per month (vs. 6 in previous 40-credit plans) to optimize video asset economics
 * Supports broader video content monetization strategy through scarcity and premium positioning
 * Enables dedicated video funnel buy-choice experiences to drive higher-value conversions

*Market Expansion & Testing:*
 * International rollout across US, France, Canada, and UK markets
 * A/B testing framework to optimize conversion rates and customer acquisition costs
 * Supports SEM campaigns in Canada and UK with dedicated landing page experiences

*Customer Experience & Conversion Optimization:*
 * Provides better buy-choice options for customers in video-heavy workflows
 * Reduces friction for mid-market customers (eliminates $29.99 to $134.99 jump)
 * Enables targeted merchandising and personalized offer presentation

h2. Success Metrics
 * *Primary:* CVR (Conversion Rate) and GNARR (Gross Net Annual Recurring Revenue) improvements in video funnel
 * *Secondary:* 14-day and 3-month retention rates, video downloads/downloaders, Fast-Follow credit usage

h2. Strategic Context

This feature represents a critical fast-follow to the August 2025 Unlimited plan launch, addressing specific market gaps while supporting Adobe Stock's transition toward premium video content offerings. Part of broader pricing architecture optimization strategy.

h2. Implementation Scope

Merchandise new 40-credit plan (3 videos/month) on Stock site across multiple international markets with A/B testing framework and dedicated video funnel experiences.

References:
 * Parent Epic: STK-129909 (EC: 40 Plan & Unlimited Fast Follows)
 * Related: STK-129539 (New buy-choice design for Unlimited offer)
 * Wiki: [https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3563409065]
```

**Key Observations from STK-129540:**
- Uses bullet points and sub-sections for clarity
- Quantifies business value with specific pricing and metrics
- Clearly articulates strategic rationale ("why now")
- Includes specific success metrics (CVR, GNARR, retention)
- References related work and documentation
- Professional, concise, business-focused language
- Provides sufficient detail for stakeholders to understand scope and value

## Rules for Description Creation

### 1. Never Assume Data
- ✅ If you cannot find information, explicitly state: "Information not found"
- ✅ Leave template sections blank if no data is available
- ❌ Do NOT fabricate or assume business value, metrics, or context
- ❌ Do NOT use generic placeholder text

### 2. Handling Existing Descriptions

**If EPIC has NO description:**
- Add the full template with gathered information

**If EPIC has EMPTY template only:**
- You may override it with populated template

**If EPIC has REAL DATA in description:**
- ✅ APPEND new information (don't delete existing)
- ✅ Add a separator like `\n---\n## Updated Information\n`
- ❌ Do NOT overwrite or delete existing content

**How to identify empty template vs real data:**
- Empty template = only section headers with no content
- Real data = actual sentences, bullet points, specific information

### 3. Output Format

**Always output to HTML file first:**
```
Filename: EPIC_Description_Review_<EPIC_ID>.html
```

**HTML Structure:**
- Use Adobe Brand Guidelines for styling
- Include EPIC ID, Title, Current Status in header
- Show CURRENT description (if any) in one section
- Show PROPOSED description in another section with:
  - **Formatted display** (human-readable with proper formatting)
  - **Copy button** (one-click copy to clipboard for Jira)
- Use clear visual separation
- Make it easy to review changes

**HTML Template Example:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EPIC Description Review - [EPIC_ID]</title>
    <style>
        body {
            font-family: "Adobe Clean", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            line-height: 1.6;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            background: #FAFAFA;
            color: #2C2C2C;
        }
        header {
            background: #EB1000;
            color: white;
            padding: 30px;
            border-radius: 8px;
            margin-bottom: 30px;
        }
        h1 { margin: 0 0 10px 0; font-weight: 900; }
        .metadata {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 10px;
            margin-top: 15px;
            font-size: 14px;
        }
        .metadata-item { opacity: 0.95; }
        .section {
            background: white;
            padding: 30px;
            margin-bottom: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }
        .section h2 {
            color: #EB1000;
            border-bottom: 2px solid #EB1000;
            padding-bottom: 10px;
            margin-top: 0;
        }
        .info-table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }
        .info-table th, .info-table td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #E1E1E1;
        }
        .info-table th {
            background: #F5F5F5;
            font-weight: bold;
            width: 40%;
        }
        .status-badge {
            display: inline-block;
            padding: 4px 12px;
            border-radius: 12px;
            font-size: 12px;
            font-weight: bold;
        }
        .status-found { background: #D4EDDA; color: #155724; }
        .status-not-found { background: #F8D7DA; color: #721C24; }
        .status-partial { background: #FFF3CD; color: #856404; }
        .sources-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }
        .source-card {
            padding: 15px;
            border-radius: 6px;
            border-left: 4px solid #E1E1E1;
        }
        .source-found { border-left-color: #0AA35B; background: #F0FFF4; }
        .source-missing { border-left-color: #BDBDBD; background: #F5F5F5; }
        .description-box {
            background: #F9F9F9;
            border-left: 4px solid #0AA35B;
            padding: 20px;
            margin: 20px 0;
            border-radius: 4px;
            font-family: monospace;
            white-space: pre-wrap;
        }
        .empty-state {
            background: #FFF3CD;
            border-left: 4px solid #FFA31A;
            padding: 20px;
            margin: 20px 0;
            border-radius: 4px;
            color: #856404;
        }
        .confidence-indicator {
            display: flex;
            align-items: center;
            gap: 10px;
            margin: 15px 0;
        }
        .confidence-bar {
            flex: 1;
            height: 8px;
            background: #E1E1E1;
            border-radius: 4px;
            overflow: hidden;
        }
        .confidence-fill {
            height: 100%;
            border-radius: 4px;
        }
        .confidence-high { background: #0AA35B; }
        .confidence-medium { background: #FFA31A; }
        .confidence-low { background: #EB1000; }
        footer {
            text-align: center;
            margin-top: 50px;
            padding: 20px;
            color: #6E6E6E;
            font-size: 14px;
        }
        .action-buttons {
            margin-top: 30px;
            padding: 20px;
            background: #F0F0F0;
            border-radius: 8px;
            text-align: center;
        }
        .btn {
            display: inline-block;
            padding: 12px 24px;
            margin: 0 10px;
            border-radius: 4px;
            text-decoration: none;
            font-weight: bold;
            transition: all 0.3s;
        }
        .btn-primary {
            background: #EB1000;
            color: white;
        }
        .btn-primary:hover {
            background: #CC0E00;
        }
    </style>
</head>
<body>
    <header>
        <h1>[EPIC_ID]: [EPIC_TITLE]</h1>
        <div class="metadata">
            <div class="metadata-item"><strong>Status:</strong> [STATUS]</div>
            <div class="metadata-item"><strong>Priority:</strong> [PRIORITY]</div>
            <div class="metadata-item"><strong>Team:</strong> [TEAM]</div>
            <div class="metadata-item"><strong>Generated:</strong> [DATE]</div>
        </div>
    </header>

    <div class="section">
        <h2>📊 Information Sources</h2>
        <div class="sources-grid">
            <div class="source-card [source-found/source-missing]">
                <strong>✓/✗ Wiki Pages</strong><br>
                <small>[Details or "Not found"]</small>
            </div>
            <div class="source-card [source-found/source-missing]">
                <strong>✓/✗ Figma Files</strong><br>
                <small>[Details or "Not found"]</small>
            </div>
            <div class="source-card [source-found/source-missing]">
                <strong>✓/✗ Stories</strong><br>
                <small>[X stories found or "None"]</small>
            </div>
            <div class="source-card [source-found/source-missing]">
                <strong>✓/✗ GitHub Links</strong><br>
                <small>[Details or "Not found"]</small>
            </div>
            <div class="source-card [source-found/source-missing]">
                <strong>✓/✗ Confluence</strong><br>
                <small>[X pages found or "None"]</small>
            </div>
            <div class="source-card [source-found/source-missing]">
                <strong>✓/✗ Other Sources</strong><br>
                <small>[Details or "None"]</small>
            </div>
        </div>

        <div class="confidence-indicator">
            <strong>Information Confidence:</strong>
            <div class="confidence-bar">
                <div class="confidence-fill [confidence-high/medium/low]" style="width: [X%]"></div>
            </div>
            <span>[High/Medium/Low]</span>
        </div>
    </div>

    <div class="section">
        <h2>📄 Current Description</h2>
        <div class="description-box">
[CURRENT_DESCRIPTION or show empty-state]
        </div>
    </div>

    <div class="section">
        <h2>✨ Proposed Description</h2>
        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px;">
            <p style="margin: 0; color: #6E6E6E; font-size: 14px;">Ready to copy to Jira</p>
            <button id="copyBtn" class="btn btn-primary" onclick="copyToClipboard()">
                📋 Copy Description
            </button>
        </div>
        <div class="description-box" id="descriptionContent">
[PROPOSED_DESCRIPTION]
        </div>
        <div id="copyNotification" style="display: none; margin-top: 15px; padding: 12px; background: #0AA35B; color: white; border-radius: 4px; text-align: center; font-weight: bold;">
            ✓ Description copied to clipboard!
        </div>
    </div>

    <div class="section">
        <h2>📝 Summary of Changes</h2>
        <table class="info-table">
            <tr>
                <th>Action</th>
                <td>[New description / Appending to existing / Replacing empty template]</td>
            </tr>
            <tr>
                <th>Sections Populated</th>
                <td>[List of sections with data]</td>
            </tr>
            <tr>
                <th>Missing Information</th>
                <td>[List of sections left blank and why]</td>
            </tr>
            <tr>
                <th>Sources Used</th>
                <td>[List of information sources that contributed]</td>
            </tr>
        </table>
    </div>

    <div class="action-buttons">
        <p><strong>Ready to update Jira?</strong></p>
        <p style="color: #6E6E6E; font-size: 14px;">Review the proposed description above and confirm if you'd like to proceed with updating the EPIC.</p>
    </div>

    <footer>
        <p>© 2025 Adobe. All rights reserved.</p>
        <p>Generated by EPIC Description Automation Tool</p>
    </footer>

    <script>
        function copyToClipboard() {
            const descElement = document.getElementById('descriptionContent');
            const text = descElement.innerText;
            
            // Create a temporary textarea to copy the text
            const textarea = document.createElement('textarea');
            textarea.value = text;
            textarea.style.position = 'fixed';
            textarea.style.opacity = '0';
            document.body.appendChild(textarea);
            textarea.select();
            
            try {
                document.execCommand('copy');
                
                // Show notification
                const notification = document.getElementById('copyNotification');
                notification.style.display = 'block';
                
                // Change button text temporarily
                const btn = document.getElementById('copyBtn');
                const originalText = btn.innerHTML;
                btn.innerHTML = '✓ Copied!';
                btn.style.background = '#0AA35B';
                
                // Reset after 3 seconds
                setTimeout(() => {
                    notification.style.display = 'none';
                    btn.innerHTML = originalText;
                    btn.style.background = '#EB1000';
                }, 3000);
                
            } catch (err) {
                console.error('Failed to copy:', err);
                alert('Failed to copy to clipboard. Please copy manually.');
            }
            
            document.body.removeChild(textarea);
        }
    </script>
</body>
</html>
```

### 4. Permission Before Updating

- ✅ Always ask for explicit permission before updating Jira
- ✅ Show the HTML review file first
- ❌ Do NOT auto-update without confirmation
- **Exception**: You don't need permission to search/read data (unless stuck in a loop)

### 5. Bulk Processing

When processing multiple EPICs:
- ✅ Follow the SAME process for each EPIC
- ✅ Maintain consistency in template structure
- ✅ Generate individual HTML files for each EPIC
- ✅ Provide a summary report of all EPICs processed
- ❌ Do NOT cut corners or skip steps for speed

### 6. Error Handling

**If authentication fails:**
- Stop immediately and report the issue
- Ask user to fix authentication before proceeding

**If no information found:**
- Report: "EPIC <EPIC_ID>: Could not find enough information to generate description"
- Still add the empty template to the EPIC (with blank sections)
- List which sources were checked

**If sources are inaccessible:**
- Ask user for more details or alternative access methods
- Document which sources couldn't be accessed

## Jira Custom Fields Reference

**⚠️ CRITICAL: Use these EXACT custom field IDs for STK project:**

| Field Name | Custom Field ID | Usage |
|------------|----------------|-------|
| **Story Points** | `cf[10003]` | Story points on EPICs and tickets |
| Team | `cf[12900]` | Team assignment (e.g., "Ecomm Demand") |
| Parent Link | `cf[21401]` | Links Initiative to EPIC, Theme to Initiative |
| Epic Link | `cf[11800]` | Links Story/Bug/Task to EPIC |
| Target End | `cf[25801]` | Expected completion date |
| Beta Date | `cf[20000]` | AB test start date |
| Flagged | `cf[10001]` | "Yes" = crucial business value |

**Common Mistakes to Avoid:**
- ❌ `customfield_10016` - This is NOT story points (wrong field!)
- ❌ Summing story points from child tickets - Read from EPIC directly
- ✅ `cf[10003]` - This is the CORRECT story points field

### Getting Story Points for EPICs:
```jql
project = STK AND issuetype = Epic AND cf[10003] IS NOT EMPTY
fields: ["key", "summary", "customfield_10003", "priority", "status"]
```

**Note:** Always use `customfield_10003` in the fields array, but `cf[10003]` in JQL queries.

## Query Examples

### Check for Stories in EPIC:
```jql
"Epic Link" = STK-XXXXX
```

### Search Confluence:
```
Query 1: "<EPIC Title>"
Query 2: "STK-XXXXX"
```

### Get EPIC Details:
```jql
key = "STK-XXXXX"
```

## Output Structure

### For Single EPIC:
1. **HTML Review File**: `EPIC_Description_Review_STK-XXXXX.html`
2. **Contains**:
   - EPIC metadata (ID, Title, Status, Priority)
   - Sources checked (with checkmarks for found/not found)
   - Current description (if exists)
   - Proposed description
   - Information sources used
   - Confidence level (High/Medium/Low based on information quality)

### For Bulk EPICs:
1. **Individual HTML files** for each EPIC
2. **Summary Report**: `EPIC_Description_Bulk_Summary.html`
   - List of all EPICs processed
   - Status for each (Success/Partial/No Info Found)
   - Quick stats: how many sources found per EPIC

## Quality Standards

### Professional Description Checklist:
- [ ] Uses clear, concise business language
- [ ] Avoids jargon unless necessary (and defined)
- [ ] Quantifies benefits where possible
- [ ] Includes specific success metrics
- [ ] Provides sufficient context for stakeholders
- [ ] Defines scope boundaries clearly
- [ ] Follows Adobe Brand Guidelines voice (conversational, clear, encouraging)

### Information Completeness:
- [ ] Business value articulated
- [ ] Success metrics defined
- [ ] Context provided
- [ ] Implementation scope outlined
- [ ] All available sources checked
- [ ] No assumptions made

## Process Flow

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
   - GitHub PRs (in Story comments) ← Check comments!
   - Confluence (search)
   - Other sources (attachments, images, docs)
   ↓
5. Aggregate all findings
   ↓
6. Generate description following appropriate template:
   - Detailed mode: Full STK-68219 template
   - Short mode: Condensed format (<300 words)
   ↓
7. Create HTML review file with copy button
   ↓
8. Present to user for review
   ↓
9. If approved → Update Jira
   If not approved → Revise based on feedback
```

## Example Usage

### Example 1: Detailed Description (Default)

**User Request**: "Generate description for STK-129540"

**Your Response**:
1. "I'll analyze STK-129540 and gather information from all available sources..."
2. Search wiki pages, Figma, Stories (including comments for GitHub PRs), Confluence, attachments
3. Generate comprehensive description following STK-68219 template
4. Create HTML review file with copy button
5. "I've created a comprehensive description. Please review: EPIC_Description_Review_STK-129540.html"
6. Wait for approval
7. If approved: "Updating Jira ticket STK-129540..."

### Example 2: Short Description

**User Request**: "Generate a short description for STK-129540"

**Your Response**:
1. "I'll analyze STK-129540 and create a concise description (under 300 words)..."
2. Search same sources but prioritize business value, metrics, and key deliverables
3. Generate short description focusing on essentials
4. Create HTML review file with copy button
5. "I've created a short description (XXX words). Please review: EPIC_Description_Review_STK-129540.html"
6. Wait for approval
7. If approved: "Updating Jira ticket STK-129540..."

### Example 3: Bulk Processing with Mode

**User Request**: "Generate short descriptions for STK-129540, STK-129541, STK-129542"

**Your Response**:
1. Process each EPIC with short description mode
2. Create individual HTML files for each
3. Create summary report showing all three EPICs
4. Present for batch approval

## Critical Reminders

⚠️ **NEVER assume or fabricate data**
⚠️ **ALWAYS check current description before overwriting**
⚠️ **ALWAYS output HTML for review before updating**
⚠️ **ALWAYS get permission before updating Jira**
⚠️ **ALWAYS follow the appropriate template** (STK-68219 for detailed, condensed for short)
⚠️ **ALWAYS maintain consistency across multiple EPICs**
⚠️ **ALWAYS check Story/Bug/Task COMMENTS for GitHub PR links** (not just descriptions)
⚠️ **ALWAYS include copy button in HTML output** for easy Jira pasting
⚠️ **ALWAYS use cf[10003] for story points** (NOT customfield_10016)

---

## Ensuring Consistency Across Runs

### 1. Follow the Exact Sequence
Always search sources in this order:
1. Wiki pages (mentioned in EPIC)
2. Figma files (attachments)
3. Stories (descriptions + comments for GitHub PRs)
4. GitHub PRs (from Story comments)
5. Confluence (search by title + EPIC ID)
6. Other sources (attachments, images)

**Why:** Ensures the same sources are checked every time, in the same priority order.

### 2. Use Consistent Jira Queries

**For EPIC Details:**
```python
jql = f"key = {EPIC_ID}"
fields = ["summary", "description", "status", "priority", "assignee", 
          "customfield_12900", "customfield_21401", "customfield_25801", 
          "customfield_20000", "customfield_10001", "customfield_10003"]
minimizeOutput = True
```

**For Stories in EPIC:**
```python
jql = f'"Epic Link" = {EPIC_ID}'
fields = ["key", "summary", "description", "issuetype"]
minimizeOutput = True
maxResults = 50  # Increase if needed
```

**For Comments (GitHub PRs):**
```python
mcp_Corp_Jira_get_jira_comments(issueIdOrKey = STORY_KEY)
# Parse for: https://git.corp.adobe.com/AdobeStock/*/pull/*
```

### 3. Use Consistent Confluence Searches

**Search 1: By Title**
```python
query = f"{EPIC_TITLE_KEYWORDS}"
space_key = "adobestock"
limit = 5
```

**Search 2: By EPIC ID**
```python
query = f"{EPIC_ID}"
space_key = "adobestock"
limit = 5
```

### 4. Template Adherence

**Detailed Mode - ALWAYS include these sections:**
- h3. Business Value
- h3. Success Metrics
- h3. Context
- h3. Implementation Scope
- h3. Key Documents (if available)
- h3. Related Work (if applicable)

**Short Mode - ALWAYS include these sections:**
- **Business Value**
- **Success Metrics**
- **Scope**
- **Context**
- **References**

### 5. Information Quality Indicators

**High Confidence (80-100%):**
- Found wiki pages with requirements
- Found multiple Stories with detailed descriptions
- Found GitHub PRs with implementation details
- Found Figma files or design docs

**Medium Confidence (50-79%):**
- Found some Stories but limited detail
- Found Confluence pages but not specific PRD
- Missing one or more key sources

**Low Confidence (<50%):**
- Only found basic EPIC description
- No wiki, Figma, or detailed Stories
- Limited context available

### 6. Handling Edge Cases

**EPIC has parent/child EPICs:**
- Note the relationship in Context section
- Reference parent EPIC ID
- List child EPICs if applicable

**EPIC is part of a program:**
- Note the program initiative
- Reference program EPIC
- Explain how this EPIC fits into larger picture

**EPIC has multiple phases:**
- Note the phase/sprint information
- Clarify what was delivered in this EPIC
- Reference follow-up work if applicable

**EPIC is blocked or dependent:**
- Note dependencies in Context
- Explain why blocked if status indicates it
- Reference blocking EPICs

### 7. Quality Assurance Checklist

Before creating HTML output, verify:
- [ ] All 6 sources were checked
- [ ] Correct custom fields used (cf[10003] for story points)
- [ ] Current description was read and preserved if needed
- [ ] Template structure followed (detailed or short mode)
- [ ] No assumed/fabricated data
- [ ] Sources are documented in HTML
- [ ] Copy button included in HTML
- [ ] Confidence level indicated

### 8. Troubleshooting Common Issues

**Issue: "Story points showing wrong numbers"**
- ✅ Fix: Use `cf[10003]` in JQL and `customfield_10003` in fields array
- ❌ Don't: Try to sum from child tickets

**Issue: "Can't find GitHub PRs"**
- ✅ Fix: Check Story/Bug/Task **comments**, not descriptions
- ✅ Look for bot user: "Adobe Stock Jira account to add PR links in comments"

**Issue: "Wiki pages not showing up"**
- ✅ Fix: Check "mentioned in" section of EPIC ticket
- ✅ Also search Confluence by EPIC ID and title keywords

**Issue: "Descriptions are inconsistent"**
- ✅ Fix: Follow the exact sequence and template every time
- ✅ Use the same JQL queries and field lists
- ✅ Always use `minimizeOutput: true` for cleaner results

**Issue: "Can't determine if description is empty or has data"**
- Empty = null, blank, or only section headers with no content
- Has data = actual sentences, bullet points, metrics, specific info
- When in doubt: Append with separator rather than replace

---

## Template Reference: STK-68219

Review this EPIC to understand the template structure that must be followed.

## Good Example: STK-129540

Review this EPIC to understand the level of detail and professionalism expected, but do not copy its format - use the template from STK-68219 instead.

---

## Version History

**v2.0 - October 17, 2025**
- ✅ Fixed: Story points field corrected to cf[10003] (was incorrectly using customfield_10016)
- ✅ Added: Jira Custom Fields Reference section with correct field IDs
- ✅ Added: "Ensuring Consistency Across Runs" section with detailed best practices
- ✅ Added: Troubleshooting section for common issues
- ✅ Enhanced: GitHub PR discovery instructions (check comments, not descriptions)
- ✅ Added: Quality assurance checklist
- ✅ Added: Edge case handling guidelines

**v1.0 - October 17, 2025**
- Initial release with detailed and short description modes
- Information gathering workflow from 6+ sources (Wiki, Figma, Stories, GitHub, Confluence, Other)
- HTML review file generation with Adobe branding
- Copy-to-clipboard functionality for easy Jira updates
- Template adherence (STK-68219 structure)
- GitHub PR discovery from Story/Bug/Task comments

