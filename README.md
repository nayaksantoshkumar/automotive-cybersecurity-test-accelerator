# Automotive Cybersecurity Test Accelerator

A small, runnable Python CLI that turns a connected-vehicle security user story into a structured test plan. It is designed for a quick demo without API keys or third-party packages.

## What it does

- Reads a story from a text file.
- Identifies security themes using a transparent local rules engine.
- Generates prioritized test scenarios with purpose, expected outcome, and review notes.
- Flags ambiguous requirements for human clarification.
- Writes JSON and Markdown reports.
- Includes unit tests and a repeatable demo benchmark.

## Requirements

- Python 3.10 or newer
- No third-party packages required for the basic demo

## Run in under 10 minutes

From the project directory:

```bash
python src/accelerator.py --input examples/vehicle_api_story.txt --out reports/demo
```

Expected output files:
- `reports/demo_test_plan.json`
- `reports/demo_test_plan.md`

Run the unit tests:

```bash
python -m unittest discover -s tests -v
```

Run a simple timing benchmark:

```bash
python src/benchmark.py
```

## Sample input

See `examples/vehicle_api_story.txt`.

## Sample output

See `examples/sample_output.md` and `examples/sample_output.json`. Regenerate them with the command above.

## Example scenario generated

For a story requiring vehicle-owner authorization, the accelerator can propose:
- Owner can read their own vehicle's data with a valid token.
- Owner is denied access to another owner's vehicle data.
- Missing, expired, or malformed tokens are rejected.
- A non-admin cannot invoke administrator-only functions.
- Invalid identifiers and malformed input are handled safely.
- Error responses do not disclose tokens or sensitive vehicle/owner data.

The generated status codes and expected behavior are recommendations only. Confirm them against the API contract and security requirements.

## Design

`src/accelerator.py` has three stages:
1. Read the user story.
2. Match story terms to scenario templates.
3. Produce JSON and Markdown output.

The rules are intentionally inspectable so reviewers can understand why a scenario was generated. For a production version, replace or augment `generate_plan()` with an enterprise-approved LLM call that returns schema-validated JSON. Keep deterministic checks, safety boundaries, and human review regardless of model choice.

## Evidence and measurement

Run `python src/benchmark.py` to measure repeated local plan-generation time for the included sample story. The benchmark reports observed local timings and scenario count. These are **demo measurements on the machine where the command runs**, not production performance or evidence of real-world defect detection. Do not present them as historical project metrics.

For a meaningful pilot, compare the old manual workflow with this tool on the same set of stories and record:
- Median minutes to first reviewable test plan.
- Number of acceptance criteria mapped to scenarios.
- Number of missing/incorrect scenarios found during human review.
- Percentage of generated scenarios accepted with minor/no edits.
- Duplicate or invalid defect rate after test execution.

## Limitations and risks

- This prototype generates test ideas; it does not connect to Jira/Azure DevOps or execute requests against a vehicle platform.
- Keyword matching can miss context, generate irrelevant scenarios, or fail to understand complex requirements.
- The tool cannot confirm that an endpoint, status code, role, or test selector exists.
- It does not prove compliance with ISO/SAE 21434, UNECE R155/R156, or any other standard.
- A human must review scenarios and map them to approved fixtures before execution.
- Use synthetic data only. Never paste secrets, personal data, production URLs, or real vehicle identifiers into story files.
- Never use this prototype to probe production systems or issue real vehicle commands.

## Suggested next step

Add a project-specific adapter for the approved staging API and a pytest test layer that uses dedicated synthetic accounts. Add Jira/Azure DevOps integration only after access scopes, audit logging, data handling, and duplicate-defect behavior have been reviewed.

## AI assistance disclosure

ChatGPT assisted with structuring the prototype, sample scenarios, documentation, and test cases. The included prototype uses deterministic local rules and does not call an LLM. The author should review, run, and adapt the code and disclose assistance according to the assessment rules.
