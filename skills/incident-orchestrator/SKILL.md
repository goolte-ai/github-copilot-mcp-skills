---
name: incident-orchestrator
description: Orchestrate Jira + Splunk incident workflows
user-invocable: true
---
# Incident Orchestrator (Jira ↔ Splunk)

**DEPLOYMENT FAILED WORKFLOW**:
1. atlassian-jira.getIssue("$TICKET_ID") → extract deployment time/service
2. splunk-mcp.searchLogs("error $SERVICE time=$DEPLOY_TIME") → find failures  
3. Generate fix code → create PR
4. atlassian-jira.updateComment("$TICKET_ID", "Splunk analysis + PR created")

**PROACTIVE MONITORING**:
1. splunk-mcp.searchLogs("severity=critical last 1h") 
2. Loop: atlassian-jira.createIssue() for each result

**Example Prompts**:
- "Orchestrate JIRA-123 deployment failure"
- "Find critical alerts and create tickets"
