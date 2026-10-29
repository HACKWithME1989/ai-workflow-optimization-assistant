# ai-workflow-optimization-assistant
AI-powered workflow analysis and optimization automation built with Make, OpenAI, and Google Sheets.


# AI Workflow Optimization Assistant

An AI-powered business process analysis and workflow optimization system built using **Make.com, OpenAI GPT-4.1 mini, Google Sheets, and REST webhooks**.

The system accepts business process information, identifies potential inefficiencies, generates prioritized automation recommendations, stores the resulting analysis, and returns a structured report through an API response.

## Project Overview

Organizations often rely on manual workflows that introduce delays, repetitive tasks, inconsistent processing, and operational inefficiencies.

This project demonstrates how AI can be integrated into an automated workflow to analyze business processes and recommend practical improvements.

### Key Capabilities

- Accept structured business process information through an HTTP webhook.
- Authenticate incoming requests using API keys.
- Validate required inputs before invoking OpenAI.
- Generate AI-powered workflow optimization reports.
- Identify bottlenecks, manual tasks, and automation opportunities.
- Provide three prioritized improvement recommendations.
- Recommend tools, implementation steps, and measurable success indicators.
- Automatically store reports in Google Sheets.
- Return analysis results through an HTTP API response.
- Handle invalid and unauthorized requests.

## Technology Stack

| Technology | Purpose |
|---|---|
| Make.com | Workflow orchestration and automation |
| OpenAI GPT-4.1 mini | AI-powered business process analysis |
| Google Sheets | Persistent report storage |
| Webhooks | HTTP request intake and response delivery |
| Postman | API integration and functional testing |
| JSON | Structured data exchange |

## System Architecture

```text
              HTTP POST Request
                      |
                      v
           Authenticated Webhook
                      |
                      v
                   Router
                  /      \
                 /        \
          Valid Input   Invalid Input
               |             |
               v             v
        OpenAI GPT-4.1   HTTP 400 Response
             mini
               |
               v
       Google Sheets Storage
               |
               v
        HTTP 200 Response
               |
               v
            API Client
```

Authentication is enforced at the webhook level before processing. The router directs valid requests through the analysis workflow and rejects requests that fail the validation conditions.

## Workflow Design

### 1. Request Intake

The system receives an HTTP POST request containing four fields:

- `processName`
- `processDescription`
- `monthlyVolume`
- `mainProblem`

### 2. Authentication and Validation

The webhook uses API key authentication.

The workflow also applies validation conditions to check that the three text fields are not empty and the monthly volume is greater than zero.

Requests that fail these conditions receive HTTP `400 Bad Request` without invoking OpenAI.

Unauthorized requests are rejected with HTTP `401 Unauthorized`.

### 3. AI Analysis

Valid requests are submitted to OpenAI GPT-4.1 mini with a structured analysis prompt.

The model generates a report containing:

1. Executive Summary
2. Current Workflow Analysis
3. Top Three Recommendations
4. Proposed Automated Workflow
5. Success Metrics
6. Risks and Limitations
7. Implementation Roadmap

The prompt instructs the model to distinguish known facts from assumptions, avoid inventing performance measurements, and recommend AI only where it provides a meaningful advantage.

### 4. Report Storage

Each completed analysis is automatically saved to Google Sheets.

The stored fields include:

- Analysis ID
- Date
- Process Name
- Process Description
- Monthly Volume
- Main Problem
- AI Analysis

This provides a persistent record of the submitted business process and generated recommendations.

### 5. Response Delivery

After the report has been stored, the system returns the generated analysis through an HTTP `200 OK` response.

## Functional Testing

The workflow was tested using Postman and Make.com's execution monitoring.

| Test Scenario | Expected Behavior | Result |
|---|---|---|
| Valid business process submission | Generate and return AI analysis | Passed |
| Google Sheets storage | Save report and request details | Passed |
| Missing required text fields | Reject request before OpenAI | Passed |
| Monthly volume of zero | Reject request before OpenAI | Passed |
| Invalid request handling | Return HTTP 400 | Passed |
| Valid API key | Allow authenticated request | Passed |
| Invalid API key | Return HTTP 401 | Passed |
| Valid request after adding error handling | Complete original workflow | Passed |

Test cases included invoice processing, IT help desk routing, employee expense reimbursement, and purchase order approval.

## Security Considerations

The project uses webhook API key authentication to restrict access and reduce unauthorized API usage.

Additional security considerations include:

- Keeping API credentials out of public repositories.
- Avoiding sensitive or confidential information in test requests.
- Validating inputs before executing AI operations.
- Restricting access to stored reports.
- Monitoring API usage and associated costs.

**Important:** This project is a portfolio demonstration, not a production-hardened application. Current validation does not comprehensively enforce data types, maximum input lengths, or all malformed-input scenarios. Production use would require additional security, privacy, monitoring, and resilience controls.

## Future Improvements

Potential enhancements include:

- Stronger JSON schema and data-type validation.
- Input length limits and request rate limiting.
- Structured JSON responses for downstream integrations.
- Automated cost and usage monitoring.
- Improved error handling for OpenAI and Google Sheets failures.
- A web interface for submitting workflow descriptions.
- Report retrieval and comparison features.
- Integration with task management and business process platforms.

## Skills Demonstrated

This project demonstrates practical experience with:

- AI workflow integration
- Business process analysis
- Automation design and orchestration
- API and webhook integration
- Conditional routing and error handling
- API key authentication
- Data mapping and persistent storage
- Functional testing and troubleshooting
- Technical documentation

## Project Purpose

This project was developed as a hands-on automation engineering portfolio project, with an emphasis on identifying operational inefficiencies and designing practical AI-assisted solutions.

The goal was to create a functioning end-to-end system rather than a conceptual demonstration.

**Project Status:** Functional prototype — core automation, validation, storage, authentication, and API response testing completed.
