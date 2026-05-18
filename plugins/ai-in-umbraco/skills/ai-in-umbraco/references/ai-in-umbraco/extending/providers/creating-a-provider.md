# Creating a Provider | AI in Umbraco

Step-by-step guide to creating a custom AI provider.

Prerequisites

Step 1: Create the Project

```
dotnet new classlib -n MyCompany.Umbraco.AI.MyProvider -f net10.0
cd MyCompany.Umbraco.AI.MyProvider
dotnet add package Umbraco.AI.Core
```

Step 2: Create the Settings Class

```
using System.ComponentModel.DataAnnotations;
using Umbraco.AI.Core.EditableModels;

namespace MyCompany.Umbraco.AI.MyProvider;

public class MyProviderSettings
{
    [AIField(
        Label = "API Key",
        Description = "Your MyProvider API key. Use $Config:Key for config reference.",
        IsSensitive = true,
        SortOrder = 1)]
    [Required]
    public string? ApiKey { get; set; }

    [AIField(
        Label = "Base URL",
        Description = "API endpoint (leave empty for default)",
        SortOrder = 2)]
    public string? BaseUrl { get; set; }

    [AIField(
        Label = "Organization ID",
        Description = "Optional organization identifier",
        SortOrder = 3)]
    public string? OrganizationId { get; set; }
}
```

Step 3: Create the Chat Capability

Step 4: Create the Provider Class

Step 5: Implement IChatClient (If Needed)

Step 6: Package and Install

Verification

Next Steps

Last updated

Was this helpful?