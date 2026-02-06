# summarize-me

When this command is invoked, use the Atlassian MCP Server to generate a sprint summary.

## Default Configuration
- Project: WUTANG
- Space: Wu-Tang-LAN

## Instructions

When user types `/summarize-me [sprint-name]`:

1. **Get Atlassian Resources**
   - Call `mcp_Atlassian-MCP-Server_getAccessibleAtlassianResources()` to get cloud ID
   - Call `mcp_Atlassian-MCP-Server_atlassianUserInfo()` to get current user info

2. **Search for Sprint Issues**
   - Use `mcp_Atlassian-MCP-Server_searchJiraIssuesUsingJql()` with:
     - JQL: `project = WUTANG AND sprint = "[sprint-name]" ORDER BY status, priority DESC`
     - Fields: `['summary', 'description', 'status', 'issuetype', 'priority', 'created', 'assignee', 'reporter', 'resolution', 'resolutiondate', 'timespent', 'storypoints', 'labels']`
     - maxResults: 100

3. **Organize and Analyze Issues**
   - Group issues by assignee (displayName)
   - Categorize by status:
     - Done: status.name = "Done" or resolution != null
     - In Progress: status.name contains "In Progress" or "In Review"
     - Backlog: status.name = "Backlog" or statusCategory.name = "To Do"
   - Count completed vs in-progress items
   - Identify key themes/categories from issue summaries

4. **Generate Summary Document**
   - Use the exact format provided by the user:
     - Executive Summary with key highlights
     - Work Summary by User (with Completed, In Progress, Backlog sections)
     - Work Summary by Category
     - Metrics table
     - Key Achievements
     - Next Sprint Priorities
     - Notes

## Output Format

Follow this exact format:

```markdown
# Sprint Summary: Wu-Tang - Sprint X (CW Y-Z)

**Sprint Period**: Calendar Weeks Y-Z  
**Team**: Infrastructure Security (Wu-Tang)  
**Generated**: [Date]

## Executive Summary
[Summary text with completion counts]

### Key Highlights
- ✅ [Achievement]
- 🔄 [In progress item]

## Work Summary by User

### [Name]
**X Completed | Y In Progress**

#### Completed Work
- **[Issue Key]**: [Summary]

#### In Progress
- **[Issue Key]**: [Summary]

## Work Summary by Category
[Organized by themes]

## Metrics
[Table with counts]

## Key Achievements
[Bulleted list]

## Next Sprint Priorities
[Prioritized list]

## Notes
[Additional context]
```

