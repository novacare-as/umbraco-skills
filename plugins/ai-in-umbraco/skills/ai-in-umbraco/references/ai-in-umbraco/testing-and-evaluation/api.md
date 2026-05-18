# Api

## Contents

- [Compare | AI in Umbraco](#compare-ai-in-umbraco)
- [Create | AI in Umbraco](#create-ai-in-umbraco)
- [Delete | AI in Umbraco](#delete-ai-in-umbraco)
- [Get | AI in Umbraco](#get-ai-in-umbraco)
- [List | AI in Umbraco](#list-ai-in-umbraco)
- [Run Batch | AI in Umbraco](#run-batch-ai-in-umbraco)
- [Run by Tags | AI in Umbraco](#run-by-tags-ai-in-umbraco)
- [Run | AI in Umbraco](#run-ai-in-umbraco)
- [List Runs | AI in Umbraco](#list-runs-ai-in-umbraco)
- [Update | AI in Umbraco](#update-ai-in-umbraco)

---

## Compare | AI in Umbraco

Compare test runs and variations for regression detection.

Compare Test Runs

Request

```
POST /umbraco/ai/management/api/v1/test-runs/compare
```

Request Body

```
{
    "baselineTestRunId": "b2c3d4e5-f6a7-8901-bcde-f12345678901",
    "comparisonTestRunId": "c3d4e5f6-a7b8-9012-cdef-123456789012"
}
```

Request Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `baselineTestRunId` | guid | Yes | The baseline run ID |
| `comparisonTestRunId` | guid | Yes | The comparison run ID |

Response

```
{
    "baselineRun": {
        "id": "b2c3d4e5-f6a7-8901-bcde-f12345678901",
        "testId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "status": "Passed",
        "durationMs": 1250,...
    },
    "comparisonRun": {
        "id": "c3d4e5f6-a7b8-9012-cdef-123456789012",
        "testId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "status": "Failed",
        "durationMs": 1480,...
    },
    "isRegression": true,
    "isImprovement": false,
    "durationChangeMs": 230,
    "graderComparisons": [
        {
            "graderId": "a1b2c3d4-0000-0000-0000-000000000001",
            "graderName": "Has bullet points",
            "baselineResult": {
                "graderId": "a1b2c3d4-0000-0000-0000-000000000001",
                "passed": true,
                "score": 1.0,
                "severity": "Error"
            },
            "comparisonResult": {
                "graderId": "a1b2c3d4-0000-0000-0000-000000000001",
                "passed": false,
                "score": 0.0,
                "failureMessage": "Expected output to contain '- ' but it was not found",
                "severity": "Error"
            },
            "changed": true,
            "scoreChange": -1.0
        }
    ]
}
```

Response Properties

| Property | Type | Description |
|---|---|---|
| `baselineRun` | object | Full baseline run details |
| `comparisonRun` | object | Full comparison run details |
| `isRegression` | bool | True if comparison failed where baseline passed |
| `isImprovement` | bool | True if comparison passed where baseline failed |
| `durationChangeMs` | long | Duration change (positive = slower) |
| `graderComparisons` | array | Per-grader comparison results |

Grader Comparison Properties

| Property | Type | Description |
|---|---|---|
| `graderId` | guid | The grader ID |
| `graderName` | string | The grader display name |
| `baselineResult` | object | Grader result from the baseline run |
| `comparisonResult` | object | Grader result from the comparison run |
| `changed` | bool | Whether the grader result changed |
| `scoreChange` | double | Score difference (positive = improvement) |

Error Responses

Compare Variations

Request

Request Body

Request Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `executionId` | guid | Yes | Execution containing both variations |
| `sourceVariationId` | guid | No | Source variation (null = default config) |
| `comparisonVariationId` | guid | Yes | Variation to compare against |

Response

Response Properties

| Property | Type | Description |
|---|---|---|
| `sourceVariationName` | string | Source variation name ("Default" or name) |
| `sourceMetrics` | object | Metrics for the source variation |
| `comparisonVariationName` | string | Comparison variation name |
| `comparisonMetrics` | object | Metrics for the comparison variation |
| `passRateDelta` | double | Difference in pass rate (comparison - source) |
| `averageDurationDeltaMs` | double | Difference in average duration (positive = slower) |
| `isRegression` | bool | Whether the comparison is a regression |
| `isImprovement` | bool | Whether the comparison is an improvement |

Examples

Compare Against Baseline

Compare Default vs Variation

Related

Last updated

Was this helpful?

---

## Create | AI in Umbraco

Create a new test.

Request

```
POST /umbraco/ai/management/api/v1/tests
```

Request Body

```
{
    "alias": "test-summarize-quality",
    "name": "Summarization Quality",
    "description": "Validates summarization output quality and format",
    "testFeatureId": "prompt",
    "testTargetId": "d290f1ee-6c54-4b01-90e6-d701748f0851",
    "profileId": "e401f2ff-7d65-5c12-a1f7-e812859a1962",
    "contextIds": [],
    "testFeatureConfig": {
        "variables": {
            "content": "Umbraco is a flexible CMS built on .NET..."
        }
    },
    "graders": [
        {
            "graderTypeId": "contains",
            "name": "Has bullet points",
            "config": { "searchPattern": "- ", "ignoreCase": true },
            "severity": "Error",
            "weight": 1.0
        },
        {
            "graderTypeId": "llm-judge",
            "name": "Quality check",
            "config": {
                "evaluationCriteria": "Is the summary concise and accurate?",
                "passThreshold": 0.7
            },
            "severity": "Error",
            "weight": 1.0
        }
    ],
    "variations": [
        {
            "name": "Claude Sonnet",
            "profileId": "CLAUDE_PROFILE_GUID"
        }
    ],
    "runCount": 3,
    "tags": ["quality", "summarization"]
}
```

Request Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `alias` | string | Yes | Unique alias (URL-safe) |
| `name` | string | Yes | Display name |
| `testFeatureId` | string | Yes | Test feature: `prompt` or `agent` |
| `testTargetId` | guid | Yes | ID of the prompt or agent to test |
| `graders` | array | Yes | At least one grader (see below) |
| `description` | string | No | Optional description |
| `profileId` | guid | No | Default AI profile |
| `contextIds` | guid[] | No | Default AI contexts |
| `testFeatureConfig` | object | No | Feature-specific configuration (JSON) |
| `variations` | array | No | A/B testing overrides |
| `runCount` | int | No | Number of runs per execution (default: 1) |
| `tags` | string[] | No | Organization tags |

Grader Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `graderTypeId` | string | Yes | Grader type (for example, `exact-match` , `llm-judge` ) |
| `name` | string | Yes | Display name for the grader instance |
| `description` | string | No | What the grader validates |
| `config` | object | No | Grader-specific configuration (JSON) |
| `negate` | bool | No | Invert the result (default: false) |
| `severity` | string | No | `Info` , `Warning` , or `Error` (default: Error) |
| `weight` | double | No | Weight for scoring, 0 to 1 (default: 1.0) |

Variation Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `name` | string | Yes | Display name |
| `description` | string | No | What the variation tests |
| `profileId` | guid | No | Profile override |
| `runCount` | int | No | Run count override |
| `contextIds` | guid[] | No | Context IDs override |
| `testFeatureConfig` | object | No | Feature config override (deep-merged) |

Response

Success

Validation Error

Examples

Last updated

Was this helpful?

---

## Delete | AI in Umbraco

Delete a test.

Request

```
DELETE /umbraco/ai/management/api/v1/tests/{idOrAlias}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `idOrAlias` | string | Test GUID or alias |

Response

Success

```
(empty response body)
```

Not Found

```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    "title": "Not Found",
    "status": 404,
    "detail": "The requested test could not be found."
}
```

Examples

Last updated

Was this helpful?

Was this helpful?

```
curl -X DELETE "https://your-site.com/umbraco/ai/management/api/v1/tests/3fa85f64-5717-4562-b3fc-2c963f66afa6" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

---

## Get | AI in Umbraco

Get a test by ID or alias.

Request

```
GET /umbraco/ai/management/api/v1/tests/{idOrAlias}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `idOrAlias` | string | Test GUID or alias |

Response

Success

```
{
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "alias": "test-summarize-quality",
    "name": "Summarization Quality",
    "description": "Validates summarization output quality and format",
    "testFeatureId": "prompt",
    "testTargetId": "d290f1ee-6c54-4b01-90e6-d701748f0851",
    "profileId": "e401f2ff-7d65-5c12-a1f7-e812859a1962",
    "contextIds": [],
    "testFeatureConfig": {
        "variables": {
            "content": "Sample article text for testing..."
        }
    },
    "graders": [
        {
            "id": "a1b2c3d4-0000-0000-0000-000000000001",
            "graderTypeId": "contains",
            "name": "Has bullet points",
            "config": { "searchPattern": "- ", "ignoreCase": true },
            "negate": false,
            "severity": "Error",
            "weight": 1.0
        },
        {
            "id": "a1b2c3d4-0000-0000-0000-000000000002",
            "graderTypeId": "llm-judge",
            "name": "Quality check",
            "config": {
                "evaluationCriteria": "Is the summary concise and accurate?",
                "passThreshold": 0.7
            },
            "negate": false,
            "severity": "Error",
            "weight": 1.0
        }
    ],
    "variations": [],
    "runCount": 3,
    "tags": ["quality", "summarization"],
    "baselineRunId": null,
    "version": 1,
    "dateCreated": "2024-06-15T10:30:00Z",
    "dateModified": "2024-06-15T10:30:00Z"
}
```

Not Found

Examples

Last updated

Was this helpful?

Was this helpful?

```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    "title": "Not Found",
    "status": 404,
    "detail": "The requested test could not be found."
}
```

```
# By ID
curl -X GET "https://your-site.com/umbraco/ai/management/api/v1/tests/3fa85f64-5717-4562-b3fc-2c963f66afa6" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"

# By alias
curl -X GET "https://your-site.com/umbraco/ai/management/api/v1/tests/test-summarize-quality" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

---

## List | AI in Umbraco

List all tests.

Request

```
GET /umbraco/ai/management/api/v1/tests
```

Query Parameters

| Parameter | Type | Default | Description |
|---|---|---|---|
| `skip` | int | 0 | Number of items to skip |
| `take` | int | 100 | Number of items to return |
| `filter` | string | null | Filter by name or alias (contains) |

Response

Success

```
{
    "items": [
        {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "alias": "test-summarize-quality",
            "name": "Summarization Quality",
            "description": "Validates summarization output quality and format",
            "testFeatureId": "prompt",
            "tags": ["quality", "summarization"],
            "runCount": 3,
            "dateCreated": "2024-06-15T10:30:00Z",
            "dateModified": "2024-06-15T10:30:00Z",
            "version": 1
        },
        {
            "id": "b4c96a75-6828-5673-c4ad-3d074a77bfb7",
            "alias": "test-seo-length",
            "name": "SEO Description Length",
            "description": "Validates meta descriptions are 50-160 characters",
            "testFeatureId": "prompt",
            "tags": ["seo", "format"],
            "runCount": 1,
            "dateCreated": "2024-06-10T08:00:00Z",
            "dateModified": "2024-06-12T14:20:00Z",
            "version": 2
        }
    ],
    "total": 2
}
```

Examples

Filter by Name

Last updated

Was this helpful?

---

## Run Batch | AI in Umbraco

Execute multiple tests in a batch.

Request

```
POST /umbraco/ai/management/api/v1/tests/run-batch
```

Request Body

```
{
    "testIds": [
        "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "b4c96a75-6828-5673-c4ad-3d074a77bfb7"
    ],
    "profileIdOverride": null,
    "contextIdsOverride": null,
    "guardrailIdsOverride": null
}
```

Request Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `testIds` | guid[] | Yes | Test IDs to execute (at least one) |
| `profileIdOverride` | guid | No | Override profile for all tests |
| `contextIdsOverride` | guid[] | No | Override context IDs for all tests |
| `guardrailIdsOverride` | guid[] | No | Override guardrail IDs for all tests |

Response

Success

Validation Error

Examples

Related

Last updated

Was this helpful?

---

## Run by Tags | AI in Umbraco

Execute all tests matching specified tags.

Request

```
POST /umbraco/ai/management/api/v1/tests/run-by-tags
```

Request Body

```
{
    "tags": ["quality", "summarization"],
    "profileIdOverride": null,
    "contextIdsOverride": null,
    "guardrailIdsOverride": null
}
```

Request Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `tags` | string[] | Yes | Tags to filter by (all must match) |
| `profileIdOverride` | guid | No | Override profile for all matching tests |
| `contextIdsOverride` | guid[] | No | Override context IDs for all tests |
| `guardrailIdsOverride` | guid[] | No | Override guardrail IDs for all tests |

Response

Success

Validation Error

Examples

Run All Quality Tests

Run SEO Tests with Profile Override

Related

Last updated

Was this helpful?

---

## Run | AI in Umbraco

Execute a single test and get results with metrics.

Request

```
POST /umbraco/ai/management/api/v1/tests/{idOrAlias}/run
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `idOrAlias` | string | Test GUID or alias |

Request Body

```
{
    "profileIdOverride": "e401f2ff-7d65-5c12-a1f7-e812859a1962",
    "contextIdsOverride": ["f512a3aa-8e76-6d23-b2a8-f923960a2073"],
    "guardrailIdsOverride": ["a623a4aa-9f87-7e34-c3a9-a034071a3184"]
}
```

Request Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `profileIdOverride` | guid | No | Override profile for all runs |
| `contextIdsOverride` | guid[] | No | Override context IDs for all runs |
| `guardrailIdsOverride` | guid[] | No | Override guardrail IDs for all runs |

Execution Flow

Response

Success

Response Properties

| Property | Type | Description |
|---|---|---|
| `testId` | guid | The test that was executed |
| `executionId` | guid | Groups all runs from this execution |
| `batchId` | guid | Batch ID (null for single runs) |
| `defaultMetrics` | object | Metrics from the default configuration runs |
| `variationMetrics` | array | Metrics for each variation |
| `aggregateMetrics` | object | Metrics across all runs (default + variations) |

Metrics Object

| Property | Type | Description |
|---|---|---|
| `testId` | guid | The test ID |
| `totalRuns` | int | Total runs executed |
| `passedRuns` | int | Runs where all Error-severity graders passed |
| `passAtK` | double | `PassedRuns / TotalRuns` |
| `passToTheK` | double | `1.0` if all passed, `0.0` otherwise |
| `runIds` | guid[] | IDs of the runs (for detail retrieval) |

Not Found

Examples

Run with Default Settings

Run with Profile Override

Related

Last updated

Was this helpful?

---

## List Runs | AI in Umbraco

List test runs with filtering.

Request

```
GET /umbraco/ai/management/api/v1/test-runs
```

Query Parameters

| Parameter | Type | Default | Description |
|---|---|---|---|
| `skip` | int | 0 | Number of items to skip |
| `take` | int | 20 | Number of items to return |
| `testId` | guid | null | Filter by test ID |
| `batchId` | guid | null | Filter by batch ID |
| `status` | string | null | Filter by status: `Running` , `Passed` , `Failed` , `Error` |
| `executionId` | guid | null | Filter by execution ID |
| `variationId` | guid | null | Filter by variation ID |

Response

Success

```
{
    "total": 3,
    "items": [
        {
            "id": "b2c3d4e5-f6a7-8901-bcde-f12345678901",
            "testId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "testName": "Summarization Quality",
            "testVersion": 1,
            "runNumber": 1,
            "profileId": "e401f2ff-7d65-5c12-a1f7-e812859a1962",
            "contextIds": [],
            "executedAt": "2024-06-15T11:00:00Z",
            "executedByUserId": "user-guid",
            "status": "Passed",
            "durationMs": 1250,
            "transcriptId": "t1-guid",
            "outcome": {
                "outputType": "Text",
                "outputValue": "- Point one\n- Point two\n- Point three",
                "finishReason": "stop",
                "tokenUsage": {
                    "inputTokens": 150,
                    "outputTokens": 45,
                    "totalTokens": 195
                }
            },
            "graderResults": [
                {
                    "graderId": "a1b2c3d4-0000-0000-0000-000000000001",
                    "graderName": "Has bullet points",
                    "graderTypeId": "contains",
                    "graderType": "CodeBased",
                    "weight": 1.0,
                    "negate": false,
                    "passed": true,
                    "score": 1.0,
                    "actualValue": "- Point one\n- Point two\n- Point three",
                    "expectedValue": "- ",
                    "failureMessage": null,
                    "metadata": null,
                    "severity": "Error"
                }
            ],
            "error": null,
            "batchId": null,
            "isBaseline": false,
            "baselineRunId": null,
            "executionId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
            "variationId": null,
            "variationName": null
        }
    ]
}
```

Run Response Properties

| Property | Type | Description |
|---|---|---|
| `id` | guid | Run unique identifier |
| `testId` | guid | The test that was run |
| `testName` | string | Test name at time of execution |
| `testVersion` | int | Test version at time of execution |
| `runNumber` | int | Run number within the execution (1 to N) |
| `profileId` | guid | Profile used for the run |
| `contextIds` | guid[] | Contexts used for the run |
| `executedAt` | date | Execution timestamp (UTC) |
| `status` | string | `Running` , `Passed` , `Failed` , or `Error` |
| `durationMs` | long | Execution duration in milliseconds |
| `transcriptId` | guid | Transcript ID for the full execution trace |
| `outcome` | object | The test output (type, value, tokens) |
| `graderResults` | array | Per-grader results |
| `error` | object | Error details if the run failed with an exception |
| `batchId` | guid | Batch ID if part of a batch |
| `isBaseline` | bool | Whether this run is the baseline |
| `executionId` | guid | Groups all runs from one execution |
| `variationId` | guid | Variation ID (null for default config) |
| `variationName` | string | Variation display name (null for default) |

Examples

List All Runs for a Test

List Failed Runs

List Runs by Batch

List Runs for an Execution

List Variation-Specific Runs

Related

Last updated

Was this helpful?

---

## Update | AI in Umbraco

Update an existing test.

Request

```
PUT /umbraco/ai/management/api/v1/tests/{idOrAlias}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `idOrAlias` | string | Test GUID or alias |

Request Body

```
{
    "alias": "test-summarize-quality",
    "name": "Summarization Quality (Updated)",
    "description": "Validates summarization output with stricter criteria",
    "testFeatureId": "prompt",
    "testTargetId": "d290f1ee-6c54-4b01-90e6-d701748f0851",
    "profileId": "e401f2ff-7d65-5c12-a1f7-e812859a1962",
    "runCount": 5,
    "graders": [
        {
            "graderTypeId": "contains",
            "name": "Has bullet points",
            "config": { "searchPattern": "- ", "ignoreCase": true },
            "severity": "Error",
            "weight": 1.0
        },
        {
            "graderTypeId": "llm-judge",
            "name": "Quality check",
            "config": {
                "evaluationCriteria": "Is the summary concise, accurate, and under 200 words?",
                "passThreshold": 0.8
            },
            "severity": "Error",
            "weight": 1.0
        }
    ],
    "tags": ["quality", "summarization", "updated"]
}
```

Response

Success

Not Found

Examples

Last updated

Was this helpful?

Was this helpful?

```
(empty response body)
```

```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    "title": "Not Found",
    "status": 404,
    "detail": "The requested test could not be found."
}
```

```
curl -X PUT "https://your-site.com/umbraco/ai/management/api/v1/tests/3fa85f64-5717-4562-b3fc-2c963f66afa6" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "alias": "test-summarize-quality",
    "name": "Summarization Quality (Updated)",
    "testFeatureId": "prompt",
    "testTargetId": "d290f1ee-6c54-4b01-90e6-d701748f0851",
    "runCount": 5,
    "graders": [
      {
        "graderTypeId": "contains",
        "name": "Has bullet points",
        "config": { "searchPattern": "- ", "ignoreCase": true },
        "severity": "Error"
      }
    ]
  }'
```

---
