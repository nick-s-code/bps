# AI Agent Instructions for Brass Plumbing Solutions

## Repository overview
- Static marketing website for Brass Plumbing Solutions.
- No build tools, package managers, or frontend frameworks are used.
- Main site pages are `index.html` and `contact-page.html`.
- Styling lives in `style.css`.
- Contact form backend is implemented as AWS Lambda functions in `lamda/`.

## Key files
- `index.html` - homepage content and navigation.
- `contact-page.html` - contact form, inline JavaScript, and Google reCAPTCHA v3 integration.
- `style.css` - global styling and section layout.
- `lamda/lambda_function_dev.py` - development Lambda handler with local origin and dev SNS topic defaults.
- `lamda/lambda_function_prod.py` - production Lambda handler with production origin and SNS settings.
- `lamda/test.py` - local test helper and reCAPTCHA scoring example.

## What matters most
- Preserve the simple static HTML/CSS design unless the user explicitly requests a redesign.
- Keep JavaScript minimal and self-contained in `contact-page.html`; avoid introducing heavy frontend tooling.
- Backend logic is focused on form validation, reCAPTCHA verification, and publishing messages to AWS SNS.
- The Lambda code currently uses `boto3`, `requests`, and AWS environment variables.

## Important conventions
- This repo is a small static site plus a simple serverless contact endpoint.
- The site is not built with React/Vue/Angular; updates should generally be made directly in `*.html` and `style.css`.
- `contact-page.html` uses a base64-encoded endpoint URL and a Google reCAPTCHA site key.
- `lamda/*` uses environment variables for security-sensitive values: `SNS_TOPIC_ARN`, `AWS_REGION`, `ALLOWED_ORIGIN`, `RECAPTCHA_SECRET_KEY`.
- Do not add new secrets directly into source files.

## How to be helpful
- When modifying content, keep layout and branding consistent with the existing plumbing-services theme.
- When editing the backend, preserve the Lambda function structure and logging style.
- When improving form handling, make sure validation matches the fields used in `contact-page.html` and the Lambda handlers.
- If the user asks for deployment or environment changes, focus on Lambda / static hosting integration rather than adding a new build pipeline.

## Suggested next customizations
- A dedicated skill for contact-form updates, form validation, and Lambda SNS publishing.
- A small prompt or hook for static content edits and mobile-friendly layout improvements.
