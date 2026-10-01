# Job search MCP server

New jobs from more than 13,000 company career sites, for Claude Code, Codex and any MCP client.

[Find your role first](https://findyourrolefirst.click) reads company career sites directly (Greenhouse, Lever, Ashby and Workday boards, plus Amazon, Apple, Google, Meta, Microsoft and Netflix) every two to six hours, and records the hour each role first appeared. This server lets your AI agent search those roles, newest first, and come back each morning for what's new.

No job boards in between, no reposts posing as new roles. Every result links to the company's own posting and application.

Also listed on [Smithery](https://smithery.ai/servers/yashnam15/find-your-role-first) and the [official MCP Registry](https://registry.modelcontextprotocol.io/v0/servers?search=findyourrolefirst) (`click.findyourrolefirst/jobfeed`).

**See it without signing up:** [new jobs posted in the last 24 hours](https://findyourrolefirst.click/jobs), by role, updated every few hours.

## Connect

You need an agent key from your [console](https://findyourrolefirst.click/account). Replace `YOUR_API_KEY` below.

**Claude Code**

```bash
claude mcp add --transport http --scope user jobfeed https://findyourrolefirst.click/mcp --header 'Authorization: Bearer YOUR_API_KEY'
```

**Codex CLI**

```bash
export JOBFEED_API_KEY=YOUR_API_KEY
codex mcp add jobfeed --url https://findyourrolefirst.click/mcp --bearer-token-env-var JOBFEED_API_KEY
```

**Any HTTP MCP client**

```json
{
  "mcpServers": {
    "jobfeed": {
      "type": "http",
      "url": "https://findyourrolefirst.click/mcp",
      "headers": { "Authorization": "Bearer YOUR_API_KEY" }
    }
  }
}
```

## Tools

| Tool | What it does |
|---|---|
| `search_jobs` | Search open roles by several titles and places at once, newest first. Filters for remote, posted within N hours, and the years of experience a posting asks for. |
| `count_jobs` | How many roles a search would return. Free, so your agent can narrow before it reads. |
| `get_changes` | New, updated, reopened and closed roles since your last check. The "what's new since yesterday" call. |
| `get_job` | One role's latest details and status. |
| `my_jobs` | Roles you've already seen this month. Re-reading them is free. |
| `get_usage` | Your remaining allowance. |

Records carry title, company, location, posted and first-seen dates, and the original posting and apply links. No description text: your agent opens the posting itself when it needs the details.

## Ask it things like

- "Find product manager roles in New York posted in the last 24 hours."
- "Any new forward deployed engineer jobs since yesterday? Skip senior and staff."
- "Count remote data scientist roles asking for 1 to 3 years of experience, then show me the newest ten."
- "Check what's new every morning and list anything at a company I haven't seen before."

## Pricing

- **Free:** sign in and search 200 roles in your first 30 days, then 100 a month, in the [web console](https://findyourrolefirst.click/account).
- **$9 a month:** 3,000 new roles a month (up to 1,000 a day) and agent access through this MCP server. Re-reading a role you've already seen that month is free. Cancel anytime.

## Links

- [Live: new jobs by role](https://findyourrolefirst.click/jobs)
- [Docs](https://findyourrolefirst.click/docs): tools, fields, REST API and limits
- [How to find jobs posted in the last 24 hours](https://findyourrolefirst.click/how-to-find-jobs-posted-in-the-last-24-hours)
- [Tools that pull jobs straight from company career pages](https://findyourrolefirst.click/tools-for-jobs-from-company-career-pages)

Questions or a company we're missing: support@findyourrolefirst.click
