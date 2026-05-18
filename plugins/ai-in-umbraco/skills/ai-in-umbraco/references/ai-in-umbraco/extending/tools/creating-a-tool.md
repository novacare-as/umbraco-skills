# Creating a Tool | AI in Umbraco

Step-by-step guide to creating a custom AI tool.

Step 1: Define Arguments (Optional)

```
using System.ComponentModel;

namespace MyProject.Tools;

/// <summary>
/// Arguments for the content search tool.
/// </summary>
public record ContentSearchArgs(
    [property: Description("The search query")] string Query,
    [property: Description("Content type to filter by (optional)")] string? ContentType = null,
    [property: Description("Maximum results (1-50, default 10)")] int MaxResults = 10);
```

Step 2: Create the Tool Class

Step 3: Configure the AITool Attribute

Step 4: Test Your Tool

Tool Without Arguments

Handling Errors

Best Practices

Last updated

Was this helpful?