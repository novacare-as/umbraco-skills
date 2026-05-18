# Custom Tools | AI in Umbraco

Create custom tools that AI models can invoke.

What Are Tools?

```
User: "What's the current inventory for product SKU-123?"

AI thinks: "I should use the inventory lookup tool"

AI requests: InventoryTool.Execute({ sku: "SKU-123" })

Tool returns: { quantity: 47, location: "Warehouse A" }

AI responds: "Product SKU-123 has 47 units in stock at Warehouse A."
```

Tool Architecture

Quick Start

Tool Without Arguments

Tool With Arguments

Registration

Key Concepts

Arguments Use Description Attributes

Tools Support Dependency Injection

Mark Destructive Tools

In This Section

Last updated

Was this helpful?

## Sub-topics

- [Creating a Tool | AI in Umbraco](tools/creating-a-tool.md)
