# Data Access And State Dataset Linkage Tool User Manual

Version: 1.0
Date: July 20, 2026

## Purpose

The Data Access and Linkage Tool supports a two-role workflow for linking state datasets. The main requirement is public/non-restricted statistical linkage; restricted encrypted linkage is optional when needed.

The portal has two login roles:

- Developer / BrightQuery
- State Owner

Any user name is accepted in this demo. The selected role controls what the user can see.

## Role Summary

### Developer / BrightQuery

The Developer / BrightQuery user can only see:

- Linkage
- Info
- Request
- Request / Approval

The developer runs linkage from the Linkage tab, uses Info to understand linkage methods, and submits a PySyft-style data/code request from the Request tab. Request / Approval is separate and shows only approval status and State Owner decision.

### State Owner

The State Owner can:

- Review submitted requests
- Review Git repository and code package metadata
- Approve, request changes, or reject requests
- Run all available linkage methods
- Use Info to compare linkage methods
- View submitted request summaries

## Login

1. Open the Streamlit app.
2. On the login page, choose a role.
3. Enter any user name.
4. Select Login.

After login, the sidebar shows the signed-in user and role. Use Logout to return to the login page.

## Main Streamlit Screen Headings

The app headings are written in detailed workflow language:

- **Data Access And State Dataset Linkage Tool**
- **BrightQuery Developer Portal For Dataset Linkage Requests**
- **Developer Dataset Linkage Workspace**
- **Detailed Linkage Method Information And Selection Guide**
- **Submit Dataset And Code Request For State Owner Review**
- **Developer Request Status And State Owner Approval**
- **State Owner Portal For Linkage Review, Approval, And Execution**
- **State Owner Dataset Linkage Workspace**
- **State Owner Request Review And Approval**
- **State Linkage Results From Selected Datasets**

## Developer / BrightQuery Workflow

### Submit A Request

1. Login as Developer / BrightQuery.
2. Open the Request tab.
3. Choose the dataset source:
   - Mock datasets
   - Upload CSVs
4. If using mock data, choose a demo request scenario or custom pair.
5. Choose the linkage method and thresholds for the request.
6. If uploading CSVs, upload both files and classify each as public/non-restricted or restricted.
7. Complete the PySyft-style request form:
   - Request name
   - Data asset / dataset details
   - Code package name
   - Git repository link
   - Git branch
   - Git commit, tag, or artifact ID
   - Code entrypoint path
   - Code request details
   - Execution context
   - Output policy
   - Reviewer notes / request details
8. Select Submit request and code.

The request is saved for State Owner review.

### Developer Visibility Rules

The developer can see:

- Linkage method selector
- Match thresholds

The developer does not see:

- State Owner linkage controls
- State Owner approval controls

The developer sees linkage output in Linkage and approval status in Request / Approval.

### Developer Dataset Linkage Workspace

1. Open the Linkage tab.
2. Choose the dataset source:
   - Mock datasets
   - Upload CSVs
3. Select the dataset pair.
4. Choose the linkage method and thresholds.
5. Select Run linkage.
6. Review **State Linkage Results**, including linked record output and aggregate summaries.

### Detailed Linkage Method Information And Selection Guide

The Info tab explains which linkage method to use:

- Direct public key linkage for public/non-restricted state statistical data
- LLM-assisted metadata planning for unclear schemas
- PPRL/PPRS methods for restricted identifiers
- SMC, honest broker, asymmetric keys, or secure enclave for stronger multi-party controls
- PySyft-style governance for request, code review, controlled execution, and release review

### Developer Request Status And State Owner Approval

1. Open the Request / Approval tab.
2. Review request status.
3. Review the State Owner decision.
4. Use the separate Linkage tab to run or review linked output.

## State Owner Workflow

### State Owner Request Review And Approval

1. Login as State Owner.
2. Open Request / Approval.
3. Review the request summary:
   - Status
   - Submitted by
   - Researcher
   - Organization
   - Project
   - Dataset pair
   - Classification
   - Code package name
   - Git repository
   - Branch
   - Commit or artifact
   - Code path
4. Review the execution request.
5. Review requested release outputs.
6. Open the Git repository link if needed.
7. Review the checklist.
8. Choose one decision:
   - approve
   - request_changes
   - reject
9. Add reviewer notes.
10. Save the State Owner decision.

### State Owner Dataset Linkage Workspace

State Owners can run the state dataset linkage flow directly. Direct public statistical linkage is the main path; encrypted methods are available only when sensitivity requires them.

1. Open Linkage.
2. Choose dataset source:
   - Mock datasets
   - Upload CSVs
3. Select or upload datasets.
4. Choose the linkage method:
   - Direct public key linkage
   - LLM-assisted linkage
   - PPRL/PPRS Bloom filter / hash embeddings
   - PPRL/PPRS salted hash + q-grams
   - Secure Multi-Party Computation (SMC)
   - Linkage Honest Broker (LHB)
   - Asymmetric key cryptography
   - PPRL/PPRS secure enclave / eyes-off execution
5. Set match thresholds when applicable.
6. Enable AI enhancement if desired and configured.
7. Select Run selected linkage.
8. Review linked records and aggregate summaries.
9. Download outputs if appropriate.

## How The App Reflects A PySyft-Style Architecture

The app is designed as a state dataset linkage tool. PySyft-style governance can be used when code-to-data review, audit, or controlled execution is required.

### Architecture Mapping

- Developer / BrightQuery represents the external researcher or developer.
- State Owner represents the data owner and reviewer.
- The Request tab represents the access request and code submission step.
- The developer Linkage tab represents user-side dataset linkage.
- The Git repository link represents the submitted code package.
- Request / Approval represents request status and State Owner decision.
- Linkage represents state dataset linkage execution and linked output.
- Request summaries represent the audit record for request, review, and release.

### PySyft-Style Boundary

In a PySyft-style architecture, public statistical data can be linked directly. If restricted data is included, the developer should not directly access raw restricted data. Instead:

1. The developer prepares code in a Git repository.
2. The developer submits a PySyft-style request with data asset, code asset, execution context, output policy, and review notes.
3. The State Owner reviews the request and code package.
4. The State Owner approves, rejects, or asks for changes.
5. Approved code is run directly for public statistical data or in the controlled owner environment for restricted data.
6. Request approval decisions are tracked separately from linkage output.

This app reflects that pattern by keeping request submission, code review, linkage execution, and result release as separate screens and responsibilities.

### Developer Linkage Method Visibility

The developer can choose the requested linkage method in the Request tab. This keeps the request complete while keeping the main focus on state dataset linkage:

- Developers describe the analytical need.
- Developers provide the Git link to the code.
- Developers select the requested linkage method and thresholds.
- State Owners review the requested method when approval or governed execution is required.
- State Owners control whether outputs are released.

## How Developers Link Data Using The Same App

Developers use the same app to run linkage in the Linkage tab and separately submit a PySyft-style data/code request for approval when approval is required.

### Developer Steps

1. Login as Developer / BrightQuery.
2. Open Request.
3. Select the dataset scope or upload public/request files for review.
4. Choose the linkage method and thresholds. Use direct public linkage for non-restricted statistical datasets.
5. Fill out the data asset, code asset, execution context, output policy, and review notes.
6. Add the Git repository link, branch, commit or tag, and code path.
7. Submit the request.
8. Open Linkage to run the selected dataset linkage.
9. Wait for State Owner approval only when governed execution or restricted release is required.
10. Open Request / Approval after submission to review decision status.

### What Happens After Submission

After the developer submits the request:

- The State Owner sees the request and Git code package metadata.
- The State Owner reviews the data asset, code asset, execution context, output policy, and review notes.
- The State Owner reviews the requested linkage method and can use Linkage for owner-controlled execution.
- The State Owner records the request approval decision when review is required.
- Linkage output remains in the separate Linkage tab.

### Developer Outcome

From the developer perspective, the app provides a complete linkage workflow:

- Submit data linkage request
- Run linkage from the user-side Linkage tab
- Attach code through Git
- Track approval status
- Review approval status separately from linkage output

The developer can see the requested linkage method, while State Owner approval still controls execution and release.

## Output Controls

Public statistical outputs can be released directly when allowed. Restricted outputs should remain privacy-safe. The app is designed to support:

- Pseudonymous IDs
- Aggregate summaries
- Match quality summaries
- Disclosure review before release
- Suppression or withholding of unsafe outputs when required

## Optional AI Setup

AI enhancement is optional and metadata-only. It should not receive raw restricted rows or direct identifiers.

To enable AI, create `.streamlit/secrets.toml`:

```toml
OPENAI_API_KEY = "your-new-key"
OPENAI_MODEL = "gpt-4.1-mini"
```

Then turn on Use AI to enhance linkage in the Linkage or Request page.

## Troubleshooting

### No request is visible to the State Owner

Login as Developer / BrightQuery and submit a request first.

### Developer results are locked

Login as State Owner and approve the request.

### AI enhancement is unavailable

Check that `OPENAI_API_KEY` exists in Streamlit secrets and that dependencies are installed.

### Uploaded CSVs do not link

Confirm that both files have compatible shared fields or that the selected State Owner linkage method is appropriate for the uploaded data.
