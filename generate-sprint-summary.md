# How to Generate Sprint Summary

## Steps Taken

1. **Get Atlassian Resources**
   - Call `getAccessibleAtlassianResources()` to get cloud ID
   - Call `atlassianUserInfo()` to get current user info

2. **Search for Sprint Issues**
   - Use `searchJiraIssuesUsingJql()` with JQL query: `sprint ~ "Wu-Tang" OR sprint ~ "Spring 21"`
   - Request fields: `['summary', 'description', 'status', 'issuetype', 'priority', 'created', 'assignee', 'reporter', 'resolution', 'resolutiondate', 'timespent', 'storypoints', 'labels']`
   - Set `maxResults` to 200

3. **Organize and Analyze**
   - Group issues by assignee
   - Categorize by status (Done, In Progress, Backlog)
   - Count completed vs in-progress items
   - Identify key themes and categories

4. **Generate Summary Document**
   - Create markdown file with:
     - Executive summary
     - Work breakdown by user
     - Work summary by category
     - Metrics and completion rates
     - Key achievements
     - Next sprint priorities

## Cursor Slash Command Usage

To use this as a Cursor slash command, you can:

1. Add to `.cursorrules` or create a custom command
2. Use the pattern: `/sprint-summary [sprint-name]`
3. The command will automatically:
   - Connect to Atlassian
   - Search for sprint issues
   - Generate the summary document

