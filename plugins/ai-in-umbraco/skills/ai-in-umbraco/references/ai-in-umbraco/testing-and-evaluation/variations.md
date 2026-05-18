# Variations | AI in Umbraco

A/B testing with variations across models and configurations.

How Variations Work

Variation Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `Name` | string | Yes | Display name (for example, "GPT-4o", "Claude Sonnet") |
| `Description` | string | No | What this variation tests |
| `ProfileId` | guid | No | Profile override. Null inherits from the test. |
| `RunCount` | int | No | Run count override. Null inherits from the test. |
| `ContextIds` | guid[] | No | Context IDs override. Null inherits from the test. |
| `TestFeatureConfig` | JSON | No | Feature config override (deep-merged with the test's config). |

Deep Merge Behavior

Creating a Test with Variations

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-c98eced5bc82107b59d82f0ec2e2fd107cdaa567%252Fbackoffice-ai-test-variation-details.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=8a306b92&sv=2)

Reading Variation Results

Comparing Variations

Related

Last updated

Was this helpful?