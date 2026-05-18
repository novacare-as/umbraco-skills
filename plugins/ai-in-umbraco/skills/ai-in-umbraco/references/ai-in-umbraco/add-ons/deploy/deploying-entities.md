# Deploying Entities | AI in Umbraco

Deploy AI connections, profiles, prompts, and agents between environments using Umbraco Deploy.

Deployment Workflow

What Gets Deployed

Connections

```
data/Revision/umbraco-ai-connection__openai-production_abcd1234.uda
```

Profiles

Contexts

Guardrails

Settings

Prompts (Requires Umbraco.AI.Prompt.Deploy)

Agents (Requires Umbraco.AI.Agent.Deploy)

Step-by-Step: Deploying a Connection

1. Create Connection in Development

2. Verify Deployment File

3. Commit to Version Control

4. Configure Target Environment

5. Deploy to Target Environment

Step-by-Step: Deploying a Profile

1. Create Profile in Development

2. Verify Deployment Files

3. Commit and Deploy

Multi-Environment Example

Development Environment

Staging Environment

Production Environment

Deployment File (Same for All Environments)

Deployment Order

Troubleshooting

Deployment Fails: "Connection not found"

Deployment Fails: "Provider not found"

API Keys Not Resolving

User Group Permissions Missing on Agents

Next Steps

Last updated

Was this helpful?