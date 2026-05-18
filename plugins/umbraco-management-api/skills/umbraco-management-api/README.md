# Umbraco Management Api Skill

A Claude Code skill that provides Reference for the Umbraco Management API — the v1 REST surface that administers an Umbraco CMS instance (the headless backoffice / management plane, distinct from the Content Delivery API and from `umbraco-ai`). Use whenever the user mentions Umbraco Management API, backoffice REST, `/umbraco/management/api/v1/`, OpenAPI/Swagger for Umbraco admin, scripted provisioning, custom backoffice UIs, or integration tests against the Umbraco backoffice; or any management domain noun: Document, Document Type, Document Blueprint, Document Version, Media, Media Type, Member, Member Type, Member Group, Template, Partial View, Script, Stylesheet, Static File, Language, Dictionary, Data Type, Relation, Relation Type, Tag, Webhook, Redirect Management, Health Check, Indexer, Searcher, Log Viewer, Telemetry, Server, Upgrade, Install, Published Cache, Imaging, Models Builder, oEmbed, Package, Property Type, Preview, User, User Group, Security, Culture, or Dynamic Root.

## Structure

```
SKILL.md              # Skill definition and routing table (always in context)
management-api/api/   # Management Api API
```

## Installation

Add this skill to your Claude Code setup by placing it in your skills directory
or referencing it in your configuration.
