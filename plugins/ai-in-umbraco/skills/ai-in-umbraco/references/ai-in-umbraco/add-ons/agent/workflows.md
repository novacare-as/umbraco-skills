# Workflows | AI in Umbraco

Create custom workflows for orchestrated agents.

Overview

Creating a Workflow

Step 1: Define the Workflow Class

```
using System.Text.Json;
using Microsoft.Agents.AI;
using Microsoft.Agents.AI.Workflows;
using Umbraco.AI.Agent.Core.Chat;
using Umbraco.AI.Agent.Core.Workflows;
using Umbraco.AI.Core.Chat;
using Umbraco.AI.Core.Models;
using Umbraco.AI.Core.Profiles;
using UmbracoAIAgent = Umbraco.AI.Agent.Core.Agents.AIAgent;

[AIAgentWorkflow("research-and-summarize", "Research and Summarize",
    Description = "A researcher gathers information, then a summarizer condenses it.")]
public class ResearchAndSummarizeWorkflow : AIAgentWorkflowBase
{
    private readonly IAIChatClientFactory _chatClientFactory;
    private readonly IAIProfileService _profileService;

    public ResearchAndSummarizeWorkflow(
        IAIChatClientFactory chatClientFactory,
        IAIProfileService profileService)
    {
        _chatClientFactory = chatClientFactory;
        _profileService = profileService;
    }

    protected override async Task<Workflow> BuildWorkflowAsync(
        UmbracoAIAgent agent,
        JsonElement? settings,
        CancellationToken cancellationToken)
    {
        // Resolve the AI profile
        var profile = agent.ProfileId.HasValue
            ? await _profileService.GetProfileAsync(agent.ProfileId.Value, cancellationToken)
                ?? throw new InvalidOperationException($"Profile '{agent.ProfileId}' not found.")
            : await _profileService.GetDefaultProfileAsync(AICapability.Chat, cancellationToken);

        var chatClient = await _chatClientFactory.CreateClientAsync(profile, cancellationToken);

        // Create sub-agents
        var researcher = new ChatClientAgent(
            chatClient,
            instructions: "You are a researcher. Gather detailed information about the topic.",
            name: "Researcher");

        var summarizer = new ChatClientAgent(
            chatClient,
            instructions: "You are a summarizer. Condense the research into a clear, concise summary.",
            name: "Summarizer");

        // Build sequential workflow: researcher → summarizer
        return AgentWorkflowBuilder.BuildSequential("research-and-summarize", [researcher, summarizer]);
    }
}
```

Step 2: Create an Orchestrated Agent

Workflows with Settings

Step 1: Define the Settings Class

Step 2: Create a Typed Workflow

Step 3: Create Agent with Settings

Related

Last updated

Was this helpful?