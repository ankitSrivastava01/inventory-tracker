# Data Access And State Dataset Linkage Tool

Streamlit mock-data app for linking state datasets, with public/non-restricted statistical linkage as the main path.

The app demonstrates:

- public statistical linkage with shared state dataset keys
- direct linkage for non-restricted education, workforce, geography, program, O*NET, LEHD-style, and CPS-style data
- optional private/public linkage with pseudonymized private references
- optional restricted private/private linkage using Python PPRL/PPRS-style encryption methods
- 12 built-in demo scenarios: 4 public, 4 private encrypted, and 4 mixed
- dropdown selection for left and right datasets
- CSV upload for any client-provided left and right datasets
- dropdown selection for the linkage method, including direct public linkage, LLM-assisted metadata review, and optional PPRL/PPRS encryption methods
- metadata-only dataset previews so source records are not displayed by default
- login page for BrightQuery/developer and State Owner roles
- State Owner login with submitted request and code review
- approval decisions for submitted code packages
- state linked record output and aggregate summaries under State Linkage Results
- optional PPRL/PPRS-style privacy controls for restricted data and privacy-safe output release
- optional AI metadata plan using `st.secrets`
- optional AI-assisted linkage enhancement using metadata only

Mock testing datasets include person, geography, education, employment, wage, observed transition, public person/geography records, public program statistics, public O*NET-style skill scores, public LEHD-style workforce statistics, and public CPS-style labor force statistics.

The mock CSV files are stored parallel to `streamlit_app.py` in the app folder:

- `person.csv`
- `education.csv`
- `employment.csv`
- `wage.csv`
- `observed_transition.csv`
- `geography.csv`
- `public_person_geo.csv`
- `program_stats.csv`
- `onet_skills.csv`
- `lehd_public.csv`
- `cps_public.csv`

## Login Roles

The app starts with a demo login page. Any user name is accepted.

- **Developer / BrightQuery:** sees **Linkage**, **Info**, **Request**, and **Request / Approval**. The Linkage tab is separate and produces **State Linkage Results** with linked record output and aggregate summaries. Info explains each linkage method. The Request page is PySyft-style and captures the data asset, code asset, execution context, output policy, and review notes. Request / Approval shows request status and State Owner decision only.
- **State Owner:** sees **Linkage**, **Info**, and **Request / Approval**. Info explains direct public linkage, PySyft-style governance, PPRL/PPRS, SMC, honest broker, asymmetric keys, and secure enclave options. The State Owner can approve, request changes, reject submitted code packages, and run any available linkage method directly.

## Current Streamlit App Headings

The Streamlit app uses detailed page headings so client users can understand each workflow area:

- **BrightQuery Developer Portal For Dataset Linkage Requests**
- **Developer Dataset Linkage Workspace**
- **Detailed Linkage Method Information And Selection Guide**
- **Submit Dataset And Code Request For State Owner Review**
- **Developer Request Status And State Owner Approval**
- **State Owner Portal For Linkage Review, Approval, And Execution**
- **State Owner Dataset Linkage Workspace**
- **State Owner Request Review And Approval**
- **State Linkage Results From Selected Datasets**

## Developer Instructions

1. Login as **Developer / BrightQuery** with any user name.
2. Open **Linkage** as the main tab when you want to run dataset linkage.
3. Open **Info** to understand which linkage method fits the data situation.
4. Open **Request** when you need to submit a PySyft-style data/code request.
5. For mock data, choose one of the demo scenarios or choose **Custom pair**.
6. Choose the linkage method and thresholds for the request.
7. For uploaded files, classify each dataset as `public/non-restricted` or `restricted`.
8. Complete the PySyft-style request sections: data asset, code asset, execution context, output policy, and review notes.
9. Submit the request.
10. Open **Request / Approval** to see request status and State Owner decision.

## State Owner Instructions

1. Login as **State Owner** with any user name.
2. Open **Request / Approval**.
3. Review the submitted PySyft-style request packet and code/Git metadata.
4. Choose **approve**, **request_changes**, or **reject**.
5. Add reviewer notes and save the decision.
6. Open **Linkage** to select datasets and run direct public statistical linkage first, with LLM-assisted metadata review or optional PPRL/PPRS, secure enclave, honest broker, SMC, or asymmetric-key methods when needed.

For non-restricted public statistical data such as public person/geography records, O*NET, LEHD-style, CPS-style, geography, or program statistics, the app uses direct shared-key linkage. No encryption, PPRL, or PPRS is required for the public demo path.

## State Owner Review Workflow

For state dataset linkage, the app starts with public/non-restricted statistical linkage. If restricted person-level data is introduced, the app separates request submission from State Owner approval and optional encrypted linkage.

1. Researcher submits the data asset, code asset, execution context, output policy, and review notes.
2. State owner reviews the request, legal basis, disclosure rules, and approved metadata.
3. Researcher develops linkage and analytics code against mock or proxy data; PPRL/PPRS encryption is added only when restricted identifiers are required.
4. Researcher submits the versioned code package, linkage method, execution context, and output policy.
5. State owner reviews the code for approved use, linkage keys, optional encryption, and release safety.
6. Approved code runs directly for public statistical data or in a controlled code-to-data workspace for restricted data.
7. State owner reviews generated outputs for small cells, linked ID exposure, match-score risk, and disclosure policy.
8. Only approved aggregate, pseudonymous, or otherwise privacy-safe outputs are released, with request/review/execution history retained for audit.

## Built-In Demo Scenarios

Public / no encryption:

- Public person geography + geography
- LEHD + CPS
- Program statistics + O*NET
- LEHD + geography

Optional restricted encrypted / PPRL-PPRS:

- Education + wage
- Person + wage
- Education + employment
- Person + education

Mixed private/public:

- Education + O*NET
- Wage + LEHD
- Employment + geography
- Education + program statistics

## Optional AI Setup

The app can generate an AI-assisted metadata plan, but only from schemas and classifications. Do not send raw restricted rows or direct identifiers.

When AI is enabled, the model recommends geography/info linkage keys from metadata only. Python then performs the local linkage on the selected datasets.

Create `.streamlit/secrets.toml` locally:

```toml
OPENAI_API_KEY = "your-new-key"
OPENAI_MODEL = "gpt-4.1-mini"
```

You can copy `.streamlit/secrets.toml.example` as a starting point. Never commit a real API key.

Then turn on **Use AI to enhance linkage** in the Linkage or Request page.

## Run

```bash
pip install -r requirements.txt
streamlit run streamlit_app.py
```
