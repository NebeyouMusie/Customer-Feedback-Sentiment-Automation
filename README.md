# Customer Feedback Sentiment Automation with n8n

Automate customer feedback collection and sentiment analysis with n8n! This project captures feedback via a form, analyzes sentiment using Google Gemini AI, logs entries in Google Sheets, and instantly alerts Customer Success when negative feedback is detected.

![Customer Feedback Sentiment Automation Cover](./images/Customer%20Feedback%20Sentiment%20Automation%20Cover.png)

---

## Table of Contents

- [Overview](#overview)
- [How It Works](#how-it-works)
  - [Workflow Steps](#workflow-steps)
- [Benefits](#benefits)
- [Requirements](#requirements)
- [Setup Instructions](#setup-instructions)
  - [1. Clone or Import Workflow](#1-clone-or-import-workflow)
  - [2. Connect Google Gemini AI](#2-connect-google-gemini-ai)
  - [3. Connect Google Sheets](#3-connect-google-sheets)
  - [4. Connect Gmail](#4-connect-gmail)
  - [5. Customize Sentiment Categories and Prompts](#5-customize-sentiment-categories-and-prompts)
  - [6. Test the Workflow](#6-test-the-workflow)
- [Customization](#customization)
  - [Google Sheets Structure](#google-sheets-structure)
  - [Email Personalization](#email-personalization)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## Overview

**Customer Feedback Sentiment Automation** is an n8n workflow designed to streamline feedback processing. It:

- Collects customer feedback through an n8n form
- Analyzes sentiment using Google Gemini AI
- Appends feedback to Google Sheets for centralized tracking
- Sends an alert email to Customer Success for negative feedback

---

## How It Works

![Workflow – Positive Route](./images/Customer%20Feedback%20Sentiment%20Automation%20workflow%20positive%20route.png)

![Workflow – Negative Route](./images/Customer%20Feedback%20Sentiment%20Automation%20workflow%20negative%20route.png)

### Workflow Steps

1. **Trigger on Form Submission**
   - The `Form Trigger` node captures `Name`, `Email Address`, and `Your Feedback`.

2. **Analyze Sentiment via Gemini AI**
   - The `Sentiment Analysis` node uses the `Google Gemini Chat Model` as its language model.
   - The system prompt instructs the model to classify feedback sentiment and return structured JSON.

3. **Append Feedback to Google Sheets (Positive/Neutral)**
   - For positive or neutral sentiment, the workflow appends a row to Google Sheets and marks `Alert` as `No`.

4. **Append Feedback and Send Alert Email (Negative)**
   - For negative sentiment, the workflow appends a row to Google Sheets and sets `Alert` to `Yes`, then sends a detailed alert email via Gmail to the Customer Success team.

---

## Benefits

- **Automates feedback & sentiment analysis**
- **Enables quick negative feedback response**
- **Centralizes data in Google Sheets**
- **Seamless email alerts integration**

---

## Requirements

- [n8n](https://n8n.io/) installation or cloud account
- Google account with:
  - Access to Google Gemini AI (API credentials)
  - Access to Google Sheets (for logging feedback)
  - Access to Gmail (for sending alert emails)

---

## Setup Instructions

### 1. Clone or Import Workflow

- Import the attached `Customer Feedback Sentiment Automation.json` into your n8n instance (Desktop or Cloud).

### 2. Connect Google Gemini AI

- Add your Google/Gemini credentials in n8n.
- In `Google Gemini Chat Model`, select your credential (e.g., "Google Gemini(PaLM) Api account").

### 3. Connect Google Sheets

- Add and select your Google Sheets OAuth credential in both Sheets nodes.
- Set the target Spreadsheet and Sheet (the JSON references a sheet named `Customer Feedback`, `Sheet1`).

### 4. Connect Gmail

- Add your Gmail OAuth2 credential and select it in the Gmail node `Send alert message to Customer Success`.
- Confirm the recipient address for alerts (default in the JSON is a sample email).

### 5. Customize Sentiment Categories and Prompts

- In `Sentiment Analysis`, you can adjust the categories (e.g., Positive, Neutral, Negative) and prompt style.
- Ensure output remains structured JSON for downstream nodes to parse reliably.

### 6. Test the Workflow

- Open the workflow and execute the `Form Trigger` test URL to submit sample feedback.
- Verify rows appear in Google Sheets with correct `Sentiment` and `Alert` values.
- Submit a negative feedback sample to confirm an alert email is sent.

![Email Sent to Customer Success](./images/Email%20Sent%20to%20Customer%20Success.png)

---

## Customization

### Google Sheets Structure

Your sheet should resemble the example below.

![Customer Feedback Data](./images/Customer%20Feedback%20Data.png)

Recommended columns:

- **Timestamp**: When the feedback was received
- **Customer Name**: Name from the form
- **Email Address**: Email from the form
- **Feedback Text**: The full customer message
- **Sentiment**: Result from Gemini AI (e.g., Positive/Neutral/Negative)
- **Alert**: `Yes` for negative feedback, `No` otherwise

### Email Personalization

You can tailor the Gmail alert content with n8n expressions using the form payload. Example snippets used in the JSON:

**Subject**: `Urgent: Negative Customer Feedback Received — Immediate Attention Required`

**Body (excerpt)**:
```
Name: {{ $('On form submission').item.json.Name }}
Email: {{ $('On form submission').item.json['Email Address'] }}
Submitted On: {{ $now.format('yyyy-MM-dd HH:mm:ss') }}

Feedback:
{{ $('On form submission').item.json['Your Feedback'] }}
```

---

## Troubleshooting

- **Gemini node errors**: Verify API credentials and model access; check quotas.
- **Google Sheets append fails**: Confirm OAuth2 is connected and the sheet ID/name are correct.
- **Gmail send errors**: Re-authenticate Gmail and verify sending permissions.
- **Form not triggering**: Use the test URL provided by the `Form Trigger` node and keep the workflow active during testing.

---

## Contributing

Contributions and suggestions are welcome!
Fork the repo, submit issues, or open pull requests for workflow improvements.

---

## License

This project is licensed under the MIT License.

---

## Contact

- **Email:** nebeyoumusie@gmail.com
- **LinkedIn:** [LinkedIn](https://www.linkedin.com/in/nebeyou-musie)
- **X(Twitter):** [X](https://x.com/NebeyouMusie)
- **Upwork:** [Upwork](https://www.upwork.com/freelancers/~017ff01729e3cd26e0?mp_source=share)
- **My Agency:** [Fuzion Tech Website](https://fuzion-tech.com/) or [Fuzion Tech on Upwork](https://www.upwork.com/agencies/1948388369189366041/)

---

**Skills & Technologies:**  
`n8n`, `Automation`, `Sentiment Analysis`, `Customer Feedback Documentation`, `Gmail`, `Google Sheets Automation`

---

**Enjoy automated customer feedback processing and rapid sentiment-driven responses!**

---

> _For any issues, please contact the project maintainer or open an issue on your workflow repository._


