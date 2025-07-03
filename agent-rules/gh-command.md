# Managing GitHub Issues with the `gh` Command Line Tool

## Installation

```bash
# Authenticate with GitHub
gh auth login
```

## Basic Issue Commands

### Listing Issues

```bash
# List all open issues in current repository
gh issue list

# List all issues (open and closed)
gh issue list --state all

# List issues assigned to you
gh issue list --assignee @me

# List issues with specific label
gh issue list --label "bug"

# List issues in JSON format
gh issue list --json number,title,state
```

### Creating Issues

```bash
# Create issue interactively
gh issue create

# Create issue with title and body
gh issue create --title "Issue Title" --body "Issue description"

# Create issue with labels and assignees
gh issue create --title "Bug Report" --body "Description" --label bug --assignee username
```

### Viewing Issues

```bash
# View issue details
gh issue view 123

# View issue in JSON format
gh issue view 123 --json number,title,body,assignees

# View issue in web browser
gh issue view 123 --web
```

## Editing Issues

### Editing Issue Title and Body

```bash
# Edit issue title
gh issue edit 123 --title "New Title"

# Edit issue body with inline text
gh issue edit 123 --body "New description for the issue"

# Edit issue body with formatted text (with line breaks and markdown)
gh issue edit 123 --body $'# Issue Title\n\n## Problem\nDescription here\n\n## Solution\n- Step 1\n- Step 2'
```

### Managing Labels and Assignees

```bash
# Add labels
gh issue edit 123 --add-label "bug,priority:high"

# Remove labels
gh issue edit 123 --remove-label "priority:low"

# Change assignees
gh issue edit 123 --add-assignee "username1,username2"
gh issue edit 123 --remove-assignee "username3"
```

### Setting Milestone and Project

```bash
# Set milestone
gh issue edit 123 --milestone "Q3 2023"

# Set project
gh issue edit 123 --project "Project Name"
```

## Closing and Reopening Issues

```bash
# Close an issue
gh issue close 123

# Close with comment
gh issue close 123 --comment "Closing this as it's fixed in PR #456"

# Reopen an issue
gh issue reopen 123
```

## Working with Comments

```bash
# List comments on an issue
gh issue view 123 --comments

# Add a comment
gh issue comment 123 --body "This is a new comment"
```

## Managing Issue Status

```bash
# Mark issue as duplicate
gh issue close 123 --comment "Duplicate of #456" --reason duplicate

# Pin an issue to repository
gh issue pin 123

# Unpin an issue
gh issue unpin 123
```

## Batch Operations

```bash
# Close multiple issues
gh issue close 123 456 789

# Add same label to multiple issues
gh issue edit 123 456 --add-label "needs-review"
```

## Tips and Tricks

### Using Body Files

For longer issue descriptions or comments:

```bash
# Create issue with body from file
echo "# Issue Description" > body.md
echo "Detailed problem information" >> body.md
gh issue create --title "Complex Issue" --body-file body.md

# Extract current body, modify it, and update
gh issue view 123 --json body | jq -r '.body' > current_body.md
# Edit current_body.md with your editor
gh issue edit 123 --body-file current_body.md
```

### Using Filters

```bash
# Find issues with specific text
gh issue list --search "authentication error"

# Find issues created by specific user
gh issue list --author "username"

# Find recent issues
gh issue list --created-after "2023-01-01"
```

### Working with Other Repositories

```bash
# Specify repository explicitly
gh issue list --repo owner/repo-name

# Create issue in another repository
gh issue create --repo owner/repo-name --title "Issue in another repo"
```

## Automation and Scripting

```bash
# Get issue details for scripting
ISSUE_NUM=$(gh issue list --json number --jq '.[0].number')
gh issue view $ISSUE_NUM --json assignees --jq '.assignees[].login'

# Automatically assign issues with certain label
for issue in $(gh issue list --label "needs-triage" --json number --jq '.[].number'); do
  gh issue edit $issue --add-assignee "username"
done
```

Remember that to use formatted text with line breaks and markdown in the command line, you can use the `$'string'` syntax in bash, which preserves escape sequences like `\n` for newlines.
