# Workflow Export Checklist

Before publishing any n8n workflow export, check that it does not expose private data.

## Replace These Values

| Private value | Public placeholder |
| --- | --- |
| Apify API token | `YOUR_APIFY_API_TOKEN` |
| Google Sheet ID | `YOUR_GOOGLE_SHEET_ID` |
| Google Sheet tab ID | `YOUR_SHEET_TAB_ID` |
| Google credential ID | `YOUR_GOOGLE_CREDENTIAL_ID` |
| Mistral credential ID | `YOUR_MISTRAL_CREDENTIAL_ID` |
| n8n workflow ID | `YOUR_N8N_WORKFLOW_ID` |
| n8n instance ID | `YOUR_N8N_INSTANCE_ID` |

## Safe To Keep

- Node names
- Placeholder URLs
- Prompt templates without private client data
- Code-node parsing logic
- Sheet column names
- Sample data using fake companies

## Search Before Publishing

Search the exported JSON for:

```text
token
secret
api_key
access_token
refresh_token
client_secret
@gmail.com
AIza
sk-
docs.google.com/spreadsheets/d/
```

If any real token, account, or private Sheet ID appears, replace it before committing.
