# Setup Guide

This guide explains how to import and run the AI B2B Lead Qualification & Google Maps Scraper workflow.

## 1. Create Accounts

You need:

- n8n Cloud or self-hosted n8n
- Apify account
- Mistral AI account
- Google account with Sheets access

## 2. Create the Google Sheet

Create a Google Sheet tab called `Leads` with this header row:

```text
company_name | city | address | phone | email | website | category | rating | reviews_count | fit_score | fit_reason | outreach_message | status
```

Recommended formatting:

- Set `phone` and `email` columns to plain text.
- Add a dropdown for `status`: `New`, `Contacted`, `Demo Booked`, `Not Interested`, `Closed Won`.

## 3. Import the Workflow

1. Open n8n.
2. Create a new workflow.
3. Choose `Import from file`.
4. Select `workflow.json`.

## 4. Add Credentials

### Apify

In the HTTP Request node URL, replace:

```text
YOUR_APIFY_API_TOKEN
```

with your Apify API token.

### Mistral

Create a Mistral Cloud credential in n8n and select it in the Mistral Cloud Chat Model node.

### Google Sheets

Create a Google Sheets OAuth2 credential in n8n and select it in the final Google Sheets node.

## 5. Configure the Search

In the `Edit Fields` node:

| Field | Meaning | Example |
| --- | --- | --- |
| `city` | Target city | `London` |
| `sector_keyword` | Business type | `dentist` |
| `max_results` | Number of Google Maps places to crawl | `25` |
| `country` | Country code for Apify search | `GB` |

## 6. Customize the AI Prompt

In the AI Agent node, replace the target-offer sentence with your actual product or service.

Example:

```text
We sell appointment-setting automation for local dental clinics.
```

## 7. Run and Verify

Run the workflow manually and confirm:

- Apify returns business listings.
- The first Code node outputs clean company fields.
- Mistral returns valid JSON.
- The second Code node merges company data with AI output.
- Google Sheets receives rows with `fit_score`, `fit_reason`, and `outreach_message`.

## 8. Troubleshooting

- If Apify returns no rows, test with a broader search keyword.
- If Mistral output fails to parse, lower prompt creativity and keep the JSON-only instruction.
- If Google Sheets does not update, confirm the sheet headers match exactly.
- If duplicate rows appear, confirm `company_name` is selected as the matching column.
