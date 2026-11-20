# Deployment & Cloud Integration Guide

This document provides deployment guidelines for hosting the BFSI Financial Decision-Making Web Platform across popular hosting providers and configuring Google Sheets synchronization.

---

## 1. Cloud Run / Docker Container Deployment (Standard Full-Stack)

The application includes an Express backend bundled with `esbuild` and Vite static assets.

### Build & Run
```bash
# 1. Compile client assets and server bundle
npm run build

# 2. Start production server
npm start
```
The server binds to `0.0.0.0:3000` and serves both the API endpoints (`/api/*`) and SPA static frontend.

### Environment Variables
Configure these in your Cloud Run or container environment:
- `GEMINI_API_KEY`: Google Gemini API key.
- `ANTHROPIC_API_KEY`: (Optional) Claude 3.5 Sonnet API key.
- `GOOGLE_SHEET_ID`: (Optional) Google Spreadsheet ID.
- `GOOGLE_SERVICE_ACCOUNT_EMAIL`: (Optional) Service account email.
- `GOOGLE_PRIVATE_KEY`: (Optional) Service account private key.

---

## 2. Netlify Deployment (Frontend + Serverless Functions)

The codebase includes standalone serverless API endpoints in `/api`:
- `/api/ai-advisor.js`
- `/api/save-record.js`
- `/api/records.js`

### Configuration (`netlify.toml`)
Create a `netlify.toml` in the project root:
```toml
[build]
  command = "npm run build"
  publish = "dist"
  functions = "api"

[[redirects]]
  from = "/api/*"
  to = "/.netlify/functions/:splat"
  status = 200

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

### Steps:
1. Connect your repository to Netlify.
2. In Site Settings > Build & Deploy > Environment, add your environment variables (`ANTHROPIC_API_KEY` or `GEMINI_API_KEY`).
3. Deploy site.

---

## 3. Vercel Deployment

1. Import the project repository into the Vercel dashboard.
2. Framework Preset: **Vite**.
3. Build Command: `npm run build`.
4. Output Directory: `dist`.
5. Under **Environment Variables**, add:
   - `ANTHROPIC_API_KEY`
   - `GEMINI_API_KEY`
   - `GOOGLE_SHEET_ID`
6. Vercel automatically maps `/api/*.js` files to Serverless Functions.

---

## 4. Google Sheets API Integration Setup

To sync financial records directly to a Google Sheet:

1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. Create a new project or select an existing one.
3. Enable the **Google Sheets API**.
4. Navigate to **IAM & Admin > Service Accounts** and create a service account (e.g., `bfsi-sheets-sync@your-project.iam.gserviceaccount.com`).
5. Create and download a JSON key for the service account.
6. Create a Google Spreadsheet in Google Drive:
   - Set column headers in Row 1:
     `Record ID | Timestamp | Applicant Name | Monthly Income | Expenses | Credit Score | Employment | Desired Loan | Tenure (Mo) | Eligible Amount | EMI | Status | Risk Category`
7. Click **Share** on your Google Sheet and invite your service account email with **Editor** permissions.
8. Copy the spreadsheet ID from the URL:
   `https://docs.google.com/spreadsheets/d/<SPREADSHEET_ID>/edit`
9. Set environment variables:
   - `GOOGLE_SHEET_ID=<SPREADSHEET_ID>`
   - `GOOGLE_SERVICE_ACCOUNT_EMAIL=<YOUR_SERVICE_ACCOUNT_EMAIL>`
   - `GOOGLE_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\n..."`
