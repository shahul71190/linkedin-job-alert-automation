# LinkedIn Job Alert Automation

An automated job-search workflow built with **n8n, Apify, and Google Sheets**. It accepts job-search parameters through a webhook, runs the Apify LinkedIn Jobs Scraper, monitors the actor run, retrieves the results, and saves job information to Google Sheets.

## Project Overview

Searching for relevant jobs manually can take time. This workflow automates job discovery and organizes the results in a Google Sheet for easier tracking.

### Features

- Webhook-based job search requests
- Job-title and location-based search
- Apify actor execution
- Actor run-status monitoring
- Dataset retrieval and job-data processing
- Google Sheets integration
- Error handling for unsuccessful actor runs
- Optional AI-generated hiring trend summary

> The optional AI summary is only included when the AI node has been implemented and tested.

## Tech Stack

- **n8n** — workflow automation
- **Apify** — LinkedIn job scraping
- **Google Sheets** — job storage
- **HTTP Request / REST API** — API communication
- **Webhook** — workflow trigger
- **Groq or another supported LLM** — optional hiring trend analysis

## Workflow Architecture

1. Receive job-search parameters through the webhook.
2. Build a LinkedIn job-search URL from the requested job title and location.
3. Start the Apify LinkedIn Jobs Scraper actor.
4. Check the actor run status until it finishes or fails.
5. Retrieve the results from the actor's dataset.
6. Map the returned data into the required fields.
7. Save the jobs to Google Sheets.
8. Optionally generate a short AI summary of hiring trends.

## Google Sheets Columns

The Google Sheet should contain these column headers:

| Column | Description |
|---|---|
| Job Title | Position title |
| Company Name | Hiring company |
| Location | Job location |
| Posted Time | When the job was posted |
| Job URL | Link to the job posting |
| Company URL | Company page URL, when available |

## Sample Webhook Payload

Send a `POST` request with a JSON body such as:

```json
{
  "jobTitle": "Python Developer",
  "location": "Remote",
  "limit": 20
}
```

- `jobTitle`: Job title to search for.
- `location`: Desired job location.
- `limit`: Maximum number of jobs requested, subject to the scraper's capabilities.

Use the **n8n test webhook URL** while testing and the production webhook URL after activating the workflow.

## Setup Instructions

### 1. Configure Apify

1. Create or sign in to your Apify account.
2. Open the `curious_coder/linkedin-jobs-scraper` actor.
3. Generate an API token in your Apify account settings.
4. Store the token securely in n8n credentials or an appropriate secret configuration.
5. Never publish your API token in this repository.

### 2. Configure Google Sheets

1. Create a Google Sheet for job results.
2. Add the six column headers listed above.
3. Connect Google Sheets to n8n using the supported Google authentication method.
4. Select the correct spreadsheet and worksheet in the Google Sheets node.

### 3. Import the Workflow

1. Download the sanitized workflow JSON from this repository.
2. Open n8n and import the JSON workflow.
3. Configure your Apify and Google Sheets credentials.
4. Select the correct spreadsheet.
5. Review the webhook, actor status-checking, dataset retrieval, and error-handling steps.

### 4. Test the Workflow

1. Start the webhook in test mode.
2. Send the sample JSON payload using Postman or another HTTP client.
3. Confirm that the actor completes successfully.
4. Verify that job results appear in Google Sheets.
5. Test the unsuccessful-run path if error handling is implemented.
6. Activate the workflow only after successful testing.

## Error Handling

The workflow should detect unsuccessful actor runs and avoid treating failed runs as successful results. Review API errors, authentication permissions, actor status, and dataset availability when troubleshooting.

## Repository Contents

```text
linkedin-job-alert-automation/
├── README.md
├── workflow/
│   └── linkedin-job-alert-automation.json
├── screenshots/
│   └── workflow-overview.png
└── docs/
    └── google-sheets-output.png
```

Optional folders and screenshots can be added as the project develops.

## Security Notes

- Do not commit API tokens, passwords, cookies, or private credentials.
- Use n8n credentials for connected services.
- Remove sensitive execution data from exported workflows and screenshots.
- Use placeholder values in public examples.
- Rotate any API token that has been exposed publicly or shared insecurely.

## Project Status

**Status:** Update this section to reflect the current implementation and testing status.

## Author

**MD Shahul Chowdhury**  
AI Automation Specialist

GitHub: [Add your GitHub profile URL]  
LinkedIn: [Add your LinkedIn profile URL]

## Disclaimer

This is an automation project for job-search assistance. LinkedIn and third-party scraping access may be subject to their respective terms, policies, and technical limitations.
