# Supported Types | AI in Umbraco

circle-info These docs are AI-generated and human-refined. If the AI missed a detail or sounds a bit funky, give us a shout! Flag an error in our tracker. arrow-up-right

Umbraco Documentation

file-lines Docs Overview

folder-grid CMS

List entity types that support version history.

Returns a list of entity types that support version history.

hashtag

```
GET /umbraco/ai/management/api/v1/versions/supported-types
```

Returns an array of entity type identifiers.

```
[
    "connection",
    "profile",
    "context",
    "prompt",
    "agent"
]
```

Available types depend on which packages are installed. prompt and agent types are only available if those add-on packages are installed.

prompt

agent

Previous Versions chevron-left

Next Get History chevron-right

Last updated 13 days ago

Was this helpful?

```
curl -X GET "https://your-site.com/umbraco/ai/management/api/v1/versions/supported-types" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```