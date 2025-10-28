# EPIC Description Generation - Usage Examples

This document provides practical examples of how to use the EPIC Description Generation prompt.

## Basic Usage

### Single EPIC

**User Request:**
```
Generate description for STK-130000
```

**Expected Process:**
1. Retrieve EPIC STK-130000 from Jira
2. Check current description (empty/template/has real data)
3. Search for information:
   - Check "mentioned in" section for wiki links
   - Look for Figma attachments
   - Search for Stories with Epic Link = STK-130000
   - Check Stories for GitHub links
   - Search Confluence for "STK-130000" and EPIC title
   - Review attachments and comments
4. Aggregate findings
5. Generate description following STK-68219 template
6. Create HTML review file: `EPIC_Description_Review_STK-130000.html`
7. Present to user for approval

### Bulk EPICs

**User Request:**
```
Generate descriptions for all EPICs in STK 2025-Q4 that don't have descriptions
```

**Expected Process:**
1. Query Jira: `project = STK AND fixVersion = "STK 2025-Q4" AND issuetype = Epic AND description ~ "EPIC INFORMATION"`
2. For each EPIC, follow same process as single EPIC
3. Generate individual HTML files for each
4. Create summary report: `EPIC_Description_Bulk_Summary.html`

## Real-World Scenarios

### Scenario 1: EPIC with Wiki Page Only

**EPIC:** STK-130000 "New checkout flow"  
**Found Sources:**
- ✅ Wiki page in "mentioned in" section
- ❌ No Figma files
- ❌ No Stories yet
- ❌ No GitHub links
- ❌ No Confluence results

**Generated Description:**
```
*EPIC INFORMATION*
||What||Link/Description||
|*SWAG Breakdown*| TBD - Pending detailed estimation |
|*Summary of Work*| Implement new checkout flow to improve conversion rates. Based on requirements from [Wiki Link]. |
|*Requirements*| See [Wiki Link] for detailed requirements |
|*Definition of Done/Outcome of deliverable*| New checkout flow live in production with A/B test framework |
|*Acceptance criteria*| - Checkout flow implemented
- A/B test configured
- Analytics tracking in place
- Cross-browser testing completed |
|*Metrics*| CVR improvement, cart abandonment rate reduction |
|*Designs*| Not yet available |

*BUSINESS VALUE:*
Improve checkout conversion rates by reducing friction in the purchase flow.
[Additional details from wiki...]

*SUCCESS METRICS:*
- Primary: CVR increase of 5%
- Secondary: Reduced cart abandonment

*IMPLEMENTATION SCOPE:*
[Details from wiki...]

*Sign Offs:*
||Step||Owner||Status||Link||
|Product/Business Requirement Wiki| | In Progress | [Wiki Link] |
|Design Document (Figma)| | Not Started | |
|Architecture Wiki| | Not Started | |

*Team*
{panel}
EM : []  | Epic Lead (EL) :[ ]
PgM : []  | PM : [ ]  | QE : [ ]
{panel}

---
*Note: Limited information available. Description generated from wiki page only. Additional details should be added as Stories, Figma designs, and technical documentation become available.*
```

### Scenario 2: EPIC with Complete Information

**EPIC:** STK-130001 "Video player enhancements"  
**Found Sources:**
- ✅ Wiki page with PRD
- ✅ Figma file with designs
- ✅ 8 Stories with detailed descriptions
- ✅ GitHub PR links in 3 Stories
- ✅ 2 Confluence pages with technical specs
- ✅ Architecture diagram attachment

**Generated Description:**
```
*EPIC INFORMATION*
||What||Link/Description||
|*SWAG Breakdown*| 13 story points across 8 stories. Estimated 3 sprints. |
|*Summary of Work*| Enhance video player with new controls, improved performance, and accessibility features. Full redesign based on user research showing 40% of users struggle with current controls. |
|*Requirements*| [PRD Wiki Link] - Detailed requirements including performance benchmarks, accessibility standards (WCAG 2.1 AA), and feature specifications |
|*Definition of Done/Outcome of deliverable*| New video player live in production across all markets with performance improvements validated and accessibility audit completed |
|*Acceptance criteria*| 
- New player controls implemented per Figma specs
- Video load time reduced by 30%
- WCAG 2.1 AA compliance achieved
- All automated tests passing
- Performance monitoring in place
- Documentation updated |
|*Metrics*| Video engagement time, playback error rate, accessibility compliance score, page load time |
|*Designs*| [Figma Link] - Complete design system with component specs, interaction patterns, and responsive breakpoints |

Is PAR required? No - No pricing changes

*BUSINESS VALUE:*

*User Experience & Engagement:*
- Addresses user research findings showing 40% struggle with current controls
- Modern, intuitive interface increases video consumption
- Accessibility improvements expand addressable market

*Technical Performance:*
- 30% improvement in video load times
- Reduced server costs through optimized streaming
- Better mobile performance on low-bandwidth connections

*Competitive Positioning:*
- Brings video player to parity with industry leaders
- Supports 4K streaming capability for premium content

*SUCCESS METRICS:*
- Primary: 20% increase in video engagement time, 30% reduction in load time
- Secondary: 50% reduction in playback errors, WCAG 2.1 AA compliance

*STRATEGIC CONTEXT:*
Supports Adobe Stock's strategic shift toward premium video content. Critical enabler for upcoming video-focused campaigns and partnerships. Addresses top customer complaint in Q3 NPS survey.

*IMPLEMENTATION SCOPE:*

*In Scope:*
- New player UI components (play/pause, volume, timeline, quality selector, fullscreen)
- Performance optimizations (lazy loading, adaptive bitrate streaming)
- Accessibility features (keyboard navigation, screen reader support, captions)
- Mobile responsive design
- Analytics instrumentation

*Out of Scope:*
- Live streaming support (future roadmap)
- Interactive video features (future roadmap)
- Backend transcoding changes (handled by separate team)

*TECHNICAL REQUIREMENTS:*
- React-based component architecture
- Integration with existing CDN infrastructure
- Support for HLS and DASH streaming protocols
- Browser support: Chrome 90+, Firefox 88+, Safari 14+, Edge 90+
- Mobile: iOS 14+, Android 10+
- Performance budget: Initial load < 2s on 3G

*USER STORIES:*
1. As a customer, I want intuitive video controls so I can easily navigate video content
2. As a customer using assistive technology, I want full keyboard navigation and screen reader support
3. As a customer on mobile, I want smooth video playback even on slower connections

*TIMELINE & DEPENDENCIES:*
- Sprint 1: Core player component and basic controls
- Sprint 2: Performance optimizations and mobile responsiveness
- Sprint 3: Accessibility features and testing
- Dependency: CDN team must complete HLS migration by Sprint 2

*SUCCESS CRITERIA:*
- All acceptance criteria met
- A/B test shows statistically significant improvement in engagement
- Zero critical or high-severity bugs in first 2 weeks post-launch
- Accessibility audit passes with no blockers

*REFERENCES:*
- Parent Initiative: STK-129000 (Video Experience Modernization)
- Related EPICs: STK-129500 (4K Video Support)
- PRD: [Wiki Link]
- Technical Spec: [Confluence Link]
- Designs: [Figma Link]
- Architecture: [Diagram attachment]

*Sign Offs:*
||Step||Owner||Status||Link||
|Product/Business Requirement Wiki| Jane Smith | Complete | [Wiki Link] |
|Design Document (Figma)| Design Team | Complete | [Figma Link] |
|Architecture Wiki| John Doe | Complete | [Confluence Link] |
|Solution Design Wiki| John Doe | Complete | [Confluence Link] |
|Analytics Requirements| Analytics Team | In Progress | [Link TBD] |
|Test Plan Wiki| QE Team | Not Started | |

*Team*
{panel}
EM : [John Doe]  | Epic Lead (EL) : [Jane Smith]
PgM : [Project Manager]  | PM : [Jane Smith]  | QE : [QE Lead]
{panel}
```

### Scenario 3: EPIC with Existing Description (Append Mode)

**EPIC:** STK-130002 has existing description:
```
We need to add pagination to search results.
Technical spike completed. Using infinite scroll pattern.
```

**Generated Output:**
The system recognizes this has real data (not empty template), so it APPENDS:

```
We need to add pagination to search results.
Technical spike completed. Using infinite scroll pattern.

---

## Updated Information (Generated 2025-10-17)

*EPIC INFORMATION*
||What||Link/Description||
|*SWAG Breakdown*| 5 story points across 3 stories |
|*Summary of Work*| Implement infinite scroll pagination for search results based on completed technical spike. Replaces current static pagination with progressive loading for improved UX. |
[... rest of template with gathered information ...]
```

## Example HTML Review File

When you run the generation, you'll get an HTML file like this:

**Filename:** `EPIC_Description_Review_STK-130000.html`

**Displays:**
- EPIC metadata (ID, title, status, priority, team)
- Information sources with checkmarks (✓ found, ✗ not found)
- Confidence indicator (High/Medium/Low with colored bar)
- Current description (or "Empty" if none)
- Proposed description (full formatted text)
- Summary of changes table
- Action buttons section asking for approval

## Command Examples

### Single EPIC
```
Generate description for STK-130000
```

### Multiple Specific EPICs
```
Generate descriptions for STK-130000, STK-130001, STK-130002
```

### Query-Based Bulk
```
Generate descriptions for all EPICs in Q4 2025 without descriptions
```

### Update Existing
```
Update description for STK-130000 (append new information)
```

## Error Handling Examples

### Authentication Failure
**Response:**
```
❌ Jira authentication failed. Please update your credentials before proceeding.
Unable to retrieve EPIC STK-130000.
```

### No Information Found
**Response:**
```
⚠️ EPIC STK-130000: Could not find enough information to generate description

Sources Checked:
- ✗ Wiki Pages: None found in "mentioned in" section
- ✗ Figma Files: No attachments found
- ✗ Stories: No stories linked to this EPIC
- ✗ GitHub Links: No GitHub links in Stories
- ✗ Confluence: No results for "STK-130000" or "New Feature Title"
- ✗ Other Sources: No additional attachments or comments

Action: Adding empty template to EPIC for future population.
```

### Partial Information
**Response:**
```
✓ Generated description for STK-130000 with MEDIUM confidence

Found Information:
- ✓ Wiki Pages: 1 page with basic requirements
- ✗ Figma Files: None
- ✓ Stories: 2 stories with partial descriptions
- ✗ GitHub Links: None
- ✗ Confluence: None
- ✗ Other Sources: None

Missing Sections:
- Designs: No Figma files found
- Technical Requirements: No architecture docs found
- Success Metrics: Not specified in available sources

Recommendation: Review HTML file and add missing information manually, or provide additional sources.
```

## Best Practices

### When to Use This Tool

✅ **Good Use Cases:**
- New EPICs that need initial descriptions
- EPICs with outdated descriptions needing updates
- Bulk update of EPICs after requirements are documented
- Standardizing EPIC format across a sprint or quarter

❌ **Avoid Using For:**
- EPICs with complete, well-maintained descriptions
- EPICs that are closed/archived
- Quick updates that don't need full template

### Tips for Best Results

1. **Ensure Sources Exist**: The more sources available (Wiki, Figma, Stories, Confluence), the better the output
2. **Review Before Updating**: Always review the HTML file before approving Jira updates
3. **Provide Context**: If the tool can't find information, provide links to relevant documentation
4. **Iterative Updates**: You can re-run the process as more information becomes available
5. **Bulk Processing**: For large batches, process in groups of 10-20 to avoid timeouts

## Troubleshooting

### "Information Not Found"
- Check if EPIC has any linked Stories, wiki pages, or attachments
- Verify Confluence access permissions
- Ensure GitHub links are properly formatted

### "Empty Description Generated"
- This is expected when no information is available
- The template structure is still added for future population
- Add sources manually and re-run the generation

### "Authentication Error"
- Update Jira credentials
- Check MCP connections
- Verify Confluence/GitHub access

---

For the complete prompt specification, see: `EPIC_Description_Generation_Prompt.md`









