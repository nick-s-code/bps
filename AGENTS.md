# AI Agent Instructions for Brass Plumbing Solutions

## Repository overview
- Static marketing website for Brass Plumbing Solutions.
- No build tools, package managers, or frontend frameworks are used.
- Source files are authored directly in HTML, CSS, and small inline JavaScript.
- Main site pages are `index.html`, `gallery-page.html`, and `contact-page.html`.
- Styling lives in `style.css`.
- Contact form backend is implemented as AWS Lambda functions in `lamda/`.

## Key files
- `index.html` - homepage content, services, testimonials, and anchor navigation.
- `gallery-page.html` - service gallery page.
- `contact-page.html` - contact form with inline JavaScript, Google reCAPTCHA v3, and an encoded Lambda endpoint.
- `style.css` - global styling and responsive layout.
- `lamda/lambda_function_dev.py` - development Lambda handler with local origin and dev SNS defaults.
- `lamda/lambda_function_prod.py` - production Lambda handler with production origin and SNS settings.
- `lamda/test.py` - local test helper and reCAPTCHA scoring example.

## What matters most
- Preserve the simple static HTML/CSS design unless the user explicitly requests a redesign.
- Keep JavaScript minimal and self-contained in `contact-page.html`; avoid introducing heavy frontend tooling or build systems.
- Form submission is handled in-browser and sent as JSON to the Lambda endpoint.
- Backend logic is focused on form validation, reCAPTCHA verification, and publishing messages to AWS SNS.
- Lambda handlers use `boto3`, `requests`, standard Python logging, and environment variables.

## Important conventions
- The repo is a static site plus a lightweight serverless contact endpoint.
- No frontend framework, bundler, or package manager should be added unless the user requests a larger modernization.
- `contact-page.html` stores the Lambda endpoint as a base64-encoded string and executes reCAPTCHA with a site key.
- `contact-page.html` expects the Lambda endpoint to accept `POST` JSON and return a JSON response.
- `lamda/*` relies on environment variables for sensitive configuration: `SNS_TOPIC_ARN`, `AWS_REGION`, `ALLOWED_ORIGIN`, `RECAPTCHA_SECRET_KEY`.
- Do not add secrets or keys directly to source files; keep them in environment configuration.
- Preserve CORS headers and OPTIONS handling in Lambda when updating backend logic.

## How to be helpful
- For layout or content changes, edit HTML/CSS directly and keep the existing plumbing-brand aesthetic.
- For contact form updates, keep validation in sync with `contact-page.html` fields and Lambda `validate_form_data`.
- For backend changes, preserve the Lambda structure and the SNS publish path unless improving delivery or error handling.
- Avoid adding new third-party frontend libraries; use native DOM and fetch APIs.
- If asked about deployment, focus on static hosting for HTML/CSS and AWS Lambda configuration for the contact endpoint.

## Suggested next customizations
- Add a dedicated skill for contact-form updates, form validation, and Lambda SNS publishing.
- Add a prompt or hook for mobile-friendly static content edits and service copy improvements.
