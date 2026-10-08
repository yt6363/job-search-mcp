---
name: find-your-role-first
description: Find newly posted jobs straight from company career sites (Greenhouse, Lever, Ashby, Workday, Amazon, Google, Apple, Meta, Microsoft, Netflix and more) through the Find your role first MCP server. Use when the user asks for new or recent job openings, roles posted in the last day or hours, jobs at specific companies, a daily job check, or help preparing an application. Never applies on the user's behalf.
---

# Find your role first

A jobs feed for agents. It reads more than 15,000 company career sites directly, every hour or two, and returns roles newest first: title, company, location, dates, the experience the posting asks for, and the link to apply. It never returns posting text; open the link to read a posting in full.

## Setup

The user needs a Find your role first plan ($9 a month) and an agent key from https://findyourrolefirst.click/account. Add the server once:

```
claude mcp add --scope user --transport http jobfeed https://findyourrolefirst.click/mcp --header "Authorization: Bearer YOUR_API_KEY"
```

Other clients: add a streamable HTTP MCP server at `https://findyourrolefirst.click/mcp` with the header `Authorization: Bearer YOUR_API_KEY`. The user supplies the key; never ask them to paste it into chat if their client can read it from an environment variable or secret store.

## Which tool, when

| The user wants | Call |
|---|---|
| "What's new for me?" or a daily check | `get_my_profile` once, then `get_new_for_me` (pass the `checked_at` from the last reply as `since` next time, so nothing repeats) |
| A search ("PM roles in New York posted today") | `search_jobs` with `roles`, `locations`, `posted_within_hours`, `experience`, `remote` |
| "How many are there?" before spending credits | `count_jobs` with the same filters (free) |
| Details on one role | `get_job` with its id |
| Help applying to one role | `get_apply_kit`: apply link, the form's questions when the site publishes them, the role's facts and a checklist |
| Roles they've already seen this month | `list_my_jobs` (free) |
| Everything that changed since last time | `get_changes` with the saved `next_cursor` |
| Remaining allowance | `get_usage` (free) |

## How to search well

- `roles` takes several titles at once and matches any of them; titles that mean the same work are matched too. Whole fields work as roles: "Product & adjacent", "Software engineering", "AI & machine learning", "Data & analytics", "Design".
- `locations` takes countries, states or cities. A country includes its remote roles. `remote: true` adds remote roles to the places (in their countries or open anywhere); on its own it means remote roles only.
- `experience` filters by the years a posting asks for ("0-1", "1-3", "3-5", "5-8", "8+"). Add "not_stated" and "unchecked" unless the user wants only postings that state a number; a third of postings don't.
- Results are newest first. `posted_within_hours: 24` is the fastest way to "today".
- Each role newly shown in a month uses one credit (3,000 a month, up to 1,000 a day). Re-reading a role already seen that month is free. Use `count_jobs` before broad searches.

## Rules

- Never submit an application or fill a form for the user. `get_apply_kit` exists so you can draft answers and tailor a résumé; the user opens `apply_url` and submits it themselves.
- Check `closed_at` is empty before recommending a role; closed roles stay visible for a while.
- Answer work-authorization and sponsorship questions only with what the user tells you.
- Don't invent salary, experience or location details; say "not stated" when the feed doesn't have them.

## Example prompts

- "Show me product roles in New York or remote posted in the last 24 hours."
- "Check for new roles that fit my profile since yesterday."
- "Help me apply to gh:stripe:1234567: what does the form ask?"
- "How many forward deployed engineer roles opened in the US this week?"
