# Best Practices | AI in Umbraco

Security, workflow, and configuration best practices for deploying AI entities across environments.

Security Best Practices

1. Always Use Configuration References

```
API Key: sk-prod-abc123def456...
```

```
API Key: $OpenAI:ApiKey
```

2. Separate Configuration by Environment

```
appsettings.json                  # Shared settings
appsettings.Development.json      # Dev secrets
appsettings.Staging.json          # Staging secrets
appsettings.Production.json       # Production secrets (not in git)
```

3. Use Secret Management for Production

4. Review Deployment Files Before Committing

5. Use .gitignore for Local Overrides

Workflow Best Practices

1. Test in Development First

2. Use Descriptive Names and Aliases

3. Version Control Everything

4. Deploy Dependencies First

5. Use Feature Branches

Configuration Best Practices

1. Group Related Settings

2. Use Consistent Key Paths

3. Document Configuration Keys

4. Validate Configuration References

Team Collaboration Best Practices

1. Coordinate AI Configuration Changes

2. Document AI Configuration

3. Review Deployment Files in Pull Requests

4. Test After Deployment

Monitoring Best Practices

1. Monitor Deployment Logs

2. Monitor API Usage

3. Set Up Alerts

Troubleshooting Best Practices

1. Check Deployment Files First

2. Compare Across Environments

3. Check Logs

4. Test Configuration References

Summary Checklist

Last updated

Was this helpful?