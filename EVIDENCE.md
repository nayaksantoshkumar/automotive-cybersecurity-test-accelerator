# Evidence and Measurement

## Prototype run evidence

The included CLI was executed locally against `examples/vehicle_api_story.txt`. The generated output is saved in `reports/` and copied to `examples/sample_output.*`.

### Automated checks
```
Spreadsheet runtime warmup failed during python startup
Traceback (most recent call last):
  File "/tmp/tmp.QlpUkOUI9D/artifact_tool_v2-2.8.66/artifact_tool/patches/warm_spreadsheet_runtime_on_startup.py", line 26, in warm_spreadsheet_runtime_on_startup
  File "/tmp/tmp.QlpUkOUI9D/artifact_tool_v2-2.8.66/artifact_tool/spreadsheet_warmup.py", line 785, in warm_spreadsheet_runtime
  File "/tmp/tmp.QlpUkOUI9D/artifact_tool_v2-2.8.66/artifact_tool/spreadsheet_warmup.py", line 718, in _warm_feature_flows
  File "/tmp/tmp.QlpUkOUI9D/artifact_tool_v2-2.8.66/artifact_tool/spreadsheet_warmup.py", line 509, in _warm_drawing_and_image_flows
  File "/tmp/tmp.QlpUkOUI9D/artifact_tool_v2-2.8.66/artifact_tool/generated/interface/models.py", line 32861, in bring_to_front
  File "/tmp/tmp.QlpUkOUI9D/artifact_tool_v2-2.8.66/artifact_tool/rpc/remote.py", line 764, in __call__
  File "/tmp/tmp.QlpUkOUI9D/artifact_tool_v2-2.8.66/artifact_tool/rpc/client.py", line 175, in call
artifact_tool.rpc.client.RemoteError: Element ordering requires an owning element collection.
test_markdown_contains_safety_notice (test_accelerator.AcceleratorTests.test_markdown_contains_safety_notice) ... ok
test_unclear_story_requests_clarification (test_accelerator.AcceleratorTests.test_unclear_story_requests_clarification) ... ok
test_vehicle_story_generates_authz_scenario (test_accelerator.AcceleratorTests.test_vehicle_story_generates_authz_scenario) ... ok

----------------------------------------------------------------------
Ran 3 tests in 0.001s

OK
```

### Local generation benchmark
```
Benchmark: local rule-based generation only; no network or LLM call
Input: examples/vehicle_api_story.txt (895 characters)
Runs: 30
Scenarios generated: 6
Median generation time: 0.043 ms
Minimum generation time: 0.041 ms
Maximum generation time: 0.245 ms
Interpretation: timing measures only local draft generation, not human review or test execution.
```

## What these numbers do and do not mean

These are measured results from the included prototype run on the machine used to package this submission. They measure only deterministic local plan generation and unit checks. They are not measurements from an automotive customer project, do not compare against a recorded manual baseline, and do not prove that generated scenarios detect real vulnerabilities.

## Pilot measurement plan

For a fair comparison, select 10–20 representative automotive security stories. Have a tester complete the existing manual workflow and the accelerator-assisted workflow on the same stories. Record:

| Metric | Baseline | Accelerator |
|---|---|---|
| Minutes to first reviewable test plan | Measure during pilot | Measure during pilot |
| Acceptance criteria mapped to test scenarios | Count after review | Count after review |
| Scenarios accepted without major edits | Count after review | Count after review |
| Missing or incorrect scenarios | Count after review | Count after review |
| Defects confirmed after execution | Count after triage | Count after triage |

Do not fill baseline values from estimates. Use actual timed runs and reviewed outputs.
