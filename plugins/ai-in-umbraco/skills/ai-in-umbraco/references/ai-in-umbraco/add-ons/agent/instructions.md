# Instructions | AI in Umbraco

circle-info These docs are AI-generated and human-refined. If the AI missed a detail or sounds a bit funky, give us a shout! Flag an error in our tracker. arrow-up-right

Umbraco Documentation

file-lines Docs Overview

folder-grid CMS

Configuring agent instructions for optimal behavior.

Instructions define how a standard agent behaves. Well-crafted instructions lead to better, more consistent responses.

Instructions apply to standard agents only. Orchestrated agents use workflows where sub-agent instructions are defined in code.

hashtag

A good instruction set includes:

Role definition - What the agent is

Capabilities - What it can do

Guidelines - How it should behave

Constraints - What it should avoid

Examples - Sample interactions (optional)

```
You are a content editing assistant for a news website.

## Role
You help journalists and editors improve their articles by providing suggestions for clarity, grammar, and style.

## Capabilities
- Improve grammar and punctuation
- Enhance readability and flow
- Suggest stronger word choices
- Identify unclear or ambiguous passages
- Check consistency in tone and style

## Guidelines
- Maintain the author's unique voice
- Preserve factual accuracy - never change facts
- Explain your suggestions briefly
- Ask for clarification when the intent is unclear
- Be encouraging and constructive

## Constraints
- Do not add opinions or editorializing
- Do not change quotes or attributed statements
- Do not make content longer unless asked
- Do not use complex jargon

## Style
- Professional but friendly tone
- Concise responses
- Use bullet points for multiple suggestions
```

Combine agent instructions with AI Contexts for brand voice:

Concepts - Agent types and fundamentals

Workflows - Orchestrated agent workflows

AI Contexts - Brand voice injection

Previous Getting Started chevron-left

Next Workflows chevron-right

Last updated 12 days ago

Was this helpful?

```
var agent = new AIAgent
{
    Alias = "brand-writer",
    Name = "Brand Writer",
    AgentType = AIAgentType.Standard,
    Config = new AIStandardAgentConfig
    {
        Instructions = @"You are a content writer for our brand.

## Your task
Write engaging content that follows our brand guidelines.

## Format
- Use headings and bullet points
- Keep paragraphs short
- Include calls to action",
        ContextIds = new[] { brandVoiceContextId, styleGuideContextId }
    }
};
```