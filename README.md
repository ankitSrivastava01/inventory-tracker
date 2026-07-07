# State Dataset Linkage Tool

Streamlit mock-data app for linking state datasets across public and restricted paths.

The app demonstrates:

- public statistical linkage with shared keys
- private/public linkage with pseudonymized private references
- restricted private/private linkage using Python PPRL methods
- 12 built-in demo scenarios: 4 public, 4 private encrypted, and 4 mixed
- dropdown selection for left and right datasets
- CSV upload for any client-provided left and right datasets
- dropdown selection for the linkage method, including direct public linkage, LLM-assisted linkage, and PPRL methods
- metadata-only dataset previews so source records are not displayed by default
- login page for BrightQuery/developer and State Owner roles
- State Owner login with submitted request and code review
- approval decisions for submitted code packages
- linked cross-reference records in results
- PPRL-style privacy controls and privacy-safe output release
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

- **Developer / BrightQuery:** sees only **Request** and **Results**. The Request page captures dataset scope, the request form, and a Git repository link for the code package. Results stay locked until State Owner approval.
- **State Owner:** sees submitted requests, Git link/code package metadata, evidence, requested outputs, attestations, and a review checklist. The State Owner can approve, request changes, reject submitted code packages, and run any available linkage method directly.

## Developer Instructions

1. Login as **Developer / BrightQuery** with any user name.
2. Open **Request**.
3. For mock data, choose one of the demo scenarios or choose **Custom pair**.
4. For uploaded files, classify each dataset as `public` or `restricted`.
5. Complete the request form and add the Git repository link, branch, commit/tag, and code path.
6. Submit the request.
7. Open **Results** to see status and approved outputs after State Owner approval.

## State Owner Instructions

1. Login as **State Owner** with any user name.
2. Open **Review Requests**.
3. Review the submitted request summary, requested outputs, evidence, attestations, and Git link/code package metadata.
4. Choose **approve**, **request_changes**, or **reject**.
5. Add reviewer notes and save the decision.
6. Open **Run Linkage** to select datasets and run direct public, mixed private/public, LLM-assisted, PPRL, secure enclave, honest broker, SMC, or asymmetric-key linkage methods.

For non-restricted public data such as public person/geography records, O*NET, LEHD-style, CPS-style, geography, or program statistics, the app uses direct shared-key linkage only. No encryption or PPRL is required for the public demo path.

## State Owner Review Workflow

For restricted person-level data, the app separates request submission from State Owner approval.

1. Researcher submits the project purpose, datasets, requested fields, linkage goal, and output contract.
2. State owner reviews the request, legal basis, disclosure rules, and approved metadata.
3. Researcher develops PPRL and analytics code against mock or proxy data only.
4. Researcher submits the versioned code package, thresholds, privacy controls, dependencies, and test evidence.
5. State owner reviews the code for approved use, identifier handling, PPRL risk, and release safety.
6. Approved code runs near the private data in a controlled code-to-data workspace.
7. State owner reviews generated outputs for small cells, linked ID exposure, match-score risk, and disclosure policy.
8. Only approved aggregate, pseudonymous, or otherwise privacy-safe outputs are released, with request/review/execution history retained for audit.

## Built-In Demo Scenarios

Public / no encryption:

- Public person geography + geography
- LEHD + CPS
- Program statistics + O*NET
- LEHD + geography

Private encrypted / PPRL:

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

Then turn on **Use AI to enhance linkage** in the Request or Run Linkage page.

## Run

```bash
pip install -r requirements.txt
streamlit run streamlit_app.py
```
