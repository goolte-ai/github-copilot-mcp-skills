---
name: incident-analyst
description: Orchestrates Jira+Splunk incidents using cloud inference
model: claude-3-5-sonnet-20241022  # Cloud model selection
mcp-servers: 
  - atlassian-jira
  - splunk-mcp
tools: 
  - read
  - write
  - bash
target: vscode
---

# How Copilot Uses Cloud Models (VS Code Agent Mode)

## Architecture Flow (Local → Cloud → Local)
