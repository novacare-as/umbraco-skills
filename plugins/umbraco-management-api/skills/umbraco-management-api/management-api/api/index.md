# Umbraco Management API — Index

This directory contains the structured API specification, broken down by domain.

## Overview

This shows all APIs available in this version of Umbraco - including all the legacy apis that are available for backward compatibility

## API metadata

| Field | Value |
|-------|-------|
| Version | `Latest` |

## Structure

```
api/
├── endpoints/
│   ├── culture.md
│   ├── data-type.md
│   ├── dictionary.md
│   ├── document-blueprint.md
│   ├── document-type.md
│   ├── document-version.md
│   ├── document.md
│   ├── dynamic-root.md
│   ├── health-check.md
│   ├── help.md
│   ├── imaging.md
│   ├── import.md
│   ├── indexer.md
│   ├── install.md
│   ├── language.md
│   ├── log-viewer.md
│   ├── manifest.md
│   ├── media-type.md
│   ├── media.md
│   ├── member-group.md
│   ├── member-type.md
│   ├── member.md
│   ├── models-builder.md
│   ├── news-dashboard.md
│   ├── object-types.md
│   ├── oembed.md
│   ├── package.md
│   ├── partial-view.md
│   ├── preview.md
│   ├── profiling.md
│   ├── property-type.md
│   ├── published-cache.md
│   ├── redirect-management.md
│   ├── relation-type.md
│   ├── relation.md
│   ├── script.md
│   ├── searcher.md
│   ├── security.md
│   ├── segment.md
│   ├── server.md
│   ├── static-file.md
│   ├── stylesheet.md
│   ├── tag.md
│   ├── telemetry.md
│   ├── template.md
│   ├── temporary-file.md
│   ├── upgrade.md
│   ├── user-data.md
│   ├── user-group.md
│   ├── user.md
│   └── webhook.md
└── schemas/
    ├── culture.md
    ├── data-type.md
    ├── dictionary.md
    ├── document-blueprint.md
    ├── document-type.md
    ├── document-version.md
    ├── document.md
    ├── dynamic-root.md
    ├── health-check.md
    ├── help.md
    ├── imaging.md
    ├── import.md
    ├── indexer.md
    ├── install.md
    ├── language.md
    ├── log-viewer.md
    ├── media-type.md
    ├── media.md
    ├── member-group.md
    ├── member-type.md
    ├── member.md
    ├── models-builder.md
    ├── news-dashboard.md
    ├── object-types.md
    ├── oembed.md
    ├── package.md
    ├── partial-view.md
    ├── profiling.md
    ├── published-cache.md
    ├── redirect-management.md
    ├── relation-type.md
    ├── relation.md
    ├── script.md
    ├── searcher.md
    ├── security.md
    ├── server.md
    ├── stylesheet.md
    ├── tag.md
    ├── telemetry.md
    ├── template.md
    ├── temporary-file.md
    ├── upgrade.md
    ├── user-data.md
    ├── user-group.md
    ├── user.md
    ├── webhook.md
    └── common/
```

## Authentication

- **Backoffice-User**: oauth2 — Umbraco Authentication

## Standard error responses

These apply to all endpoints and are not repeated per endpoint.

| Code | Meaning |
|------|---------|
| 400 | Validation error or invalid parameters |
| 401 | Missing, expired, or invalid token |
| 404 | Resource not found |
| 409 | Conflict (duplicate ID on create) |
| 429 | Rate limited — check `Retry-After` header |
| 500 | Server error |

## Endpoint files — what each covers

| File | API tags covered | Key operations |
|------|-----------------|----------------|
| `endpoints/culture.md` | Culture | Gets a paginated collection of cultures available for creating languages. |
| `endpoints/data-type.md` | Data Type | Creates a new data type., Gets a data type., Deletes a data type., Updates a data type., Copies a data type. |
| `endpoints/dictionary.md` | Dictionary | Gets a paginated collection of dictionary items., Creates a new dictionary., Gets a dictionary., Deletes a dictionary., Updates a dictionary. |
| `endpoints/document.md` | Document | Gets a document collection., Creates a new document., Gets a document., Deletes a document., Updates a document. |
| `endpoints/document-blueprint.md` | Document Blueprint | Creates a new document blueprint., Gets a document blueprint., Deletes a document blueprint., Updates a document blueprint., Moves a document blueprint. |
| `endpoints/document-type.md` | Document Type | Creates a new document type., Gets a document type., Deletes a document type., Updates a document type., Gets allowed child document types. |
| `endpoints/document-version.md` | Document Version | Gets a paginated collection of versions for a specific document., Gets a specific document version., Sets the prevent clean up status for a document version., Rolls back a document to a specific version. |
| `endpoints/dynamic-root.md` | Dynamic Root | Gets dynamic roots., Gets dynamic root query steps. |
| `endpoints/health-check.md` | Health Check | Gets a collection of health check groups., Gets a health check group by name., Executes all health checks in a group., Executes a health check action. |
| `endpoints/help.md` | Help | Gets help information. |
| `endpoints/imaging.md` | Imaging | Gets URLs for image resizing. |
| `endpoints/import.md` | Import | Analyzes an import file. |
| `endpoints/indexer.md` | Indexer | Gets a collection of indexers., Gets indexer details., Rebuilds an indexer. |
| `endpoints/install.md` | Install | Gets install settings., Performs installation setup., Validates database connection. |
| `endpoints/language.md` | Language | Gets a collection of language items., Gets the default language., Gets a paginated collection of languages., Creates a new language., Gets a language by ISO code. |
| `endpoints/log-viewer.md` | Log Viewer | Gets a collection of log sink levels., Gets log level counts., Gets a paginated collection of log entries., Gets a collection of log message templates., Gets a collection of saved log searches. |
| `endpoints/manifest.md` | Manifest | Gets all manifests., Gets private manifests., Gets public manifests. |
| `endpoints/media.md` | Media | Gets a collection of media items., Gets a collection of media items., Gets ancestors for a collection of media items., Searches media items., Creates a new media. |
| `endpoints/media-type.md` | Media Type | Gets a collection of media type items., Gets a collection of media type items., Gets ancestors for a collection of media type items., Gets a collection of media type folder items., Searches media type items. |
| `endpoints/member.md` | Member | Gets a filtered collection of members., Gets a collection of member items., Gets ancestors for a collection of member items., Searches member items., Creates a new member. |
| `endpoints/member-group.md` | Member Group | Gets a collection of member group items., Gets a paginated collection of member groups., Creates a new member group., Gets a member group., Deletes a member group. |
| `endpoints/member-type.md` | Member Type | Gets a collection of member type items., Gets ancestors for a collection of member type items., Searches member type items., Creates a new member type., Gets a member type. |
| `endpoints/models-builder.md` | Models Builder | Builds models., Gets models builder dashboard data., Gets models builder status. |
| `endpoints/news-dashboard.md` | News Dashboard | Gets news dashboard content. |
| `endpoints/object-types.md` | Object Types | Gets a paginated collection of allowed object types. |
| `endpoints/oembed.md` | oEmbed | Queries OEmbed information. |
| `endpoints/package.md` | Package | Runs pending package migrations., Gets the package configuration., Gets a paginated collection of created packages., Creates a new package., Gets a package. |
| `endpoints/partial-view.md` | Partial View | Gets a collection of partial view items., Creates a new partial view., Gets a partial view by path., Deletes a partial view., Updates a partial view. |
| `endpoints/preview.md` | Preview | Exits preview mode., Enters preview mode. |
| `endpoints/profiling.md` | Profiling | Gets profiling status., Updates the web profiling status. |
| `endpoints/property-type.md` | Property Type | Checks if a property type is used. |
| `endpoints/published-cache.md` | Published Cache | Rebuilds the published content cache., Gets the rebuild cache status., Reloads the published content cache. |
| `endpoints/redirect-management.md` | Redirect Management | Gets a paginated collection of redirect URLs., Gets a redirect URL., Deletes a redirect URL., Gets the current redirect URL management status., Sets the redirect URL tracking status. |
| `endpoints/relation.md` | Relation | Gets relations by relation type. |
| `endpoints/relation-type.md` | Relation Type | Gets a collection of relation type items., Gets a paginated collection of relation types., Gets a relation type. |
| `endpoints/script.md` | Script | Gets a collection of script items., Creates a new script., Gets a script by path., Deletes a script., Updates a script. |
| `endpoints/searcher.md` | Searcher | Gets a collection of searchers., GetSearcherBySearcherNameQuery |
| `endpoints/security.md` | Security | Gets the security configuration., Requests a password reset., Initiates password reset., Verifies a password reset token. |
| `endpoints/segment.md` | Segment | Gets a paginated collection of segments. |
| `endpoints/server.md` | Server | Gets the server configuration., Gets server information., Gets server status., Gets server troubleshooting information., Checks for available upgrades. |
| `endpoints/static-file.md` | Static File | Gets a collection of static file items., Gets a collection of ancestor static file items., Gets a collection of static file tree child items., Gets a collection of static file items from the root of the tree. |
| `endpoints/stylesheet.md` | Stylesheet | Gets a collection of stylesheet items., Creates a new stylesheet., Gets a stylesheet by path., Deletes a stylesheet., Updates a stylesheet. |
| `endpoints/tag.md` | Tag | Gets a collection of tags. |
| `endpoints/telemetry.md` | Telemetry | Gets telemetry data., Gets telemetry information., Sets telemetry consent level. |
| `endpoints/template.md` | Template | Gets a collection of template items., Gets ancestors for a collection of template items., Searches template items., Creates a new template., Gets a template. |
| `endpoints/temporary-file.md` | Temporary File | Creates a temporary file., Gets a temporary file., Deletes a temporary file., Gets the temporary file configuration. |
| `endpoints/upgrade.md` | Upgrade | Authorizes the upgrade., Gets upgrade settings. |
| `endpoints/user.md` | User | Gets a filtered collection of users., Gets a collection of user items., Creates a new user., Deletes multiple users., Gets a paginated collection of users. |
| `endpoints/user-data.md` | User Data | Creates user data., Gets user data., Updates user data., Gets user data., Deletes user data. |
| `endpoints/user-group.md` | User Group | Gets a filtered collection of user groups., Gets a collection of user group items., Deletes multiple user groups., Creates a new user group., Gets a paginated collection of user groups. |
| `endpoints/webhook.md` | Webhook | Gets a collection of webhook items., Gets a paginated collection of webhooks., Creates a new webhook., Gets a webhook., Deletes a webhook. |

## Schema files — what each covers

| File | Key schemas |
|------|------------|
| `schemas/common/index.md` | AllowedDocumentTypeModel, AllowedMediaTypeItemResponseModel, AllowedMediaTypeModel, AuditLogResponseModel, AuditTypeModel |
| `schemas/culture.md` | PagedCultureReponseModel |
| `schemas/data-type.md` | BatchResponseModelDataTypeResponseModel, CopyDataTypeRequestModel, CreateDataTypeRequestModel, DataTypeResponseModel, DatatypeConfigurationResponseModel |
| `schemas/dictionary.md` | CreateDictionaryItemRequestModel, DictionaryItemResponseModel, ImportDictionaryRequestModel, MoveDictionaryRequestModel, PagedDictionaryOverviewResponseModel |
| `schemas/document.md` | CopyDocumentRequestModel, CreateDocumentRequestModel, DocumentConfigurationResponseModel, DocumentResponseModel, DocumentUrlInfoModel |
| `schemas/document-blueprint.md` | CreateDocumentBlueprintFromDocumentRequestModel, CreateDocumentBlueprintRequestModel, DocumentBlueprintResponseModel, MoveDocumentBlueprintRequestModel, PagedDocumentBlueprintTreeItemResponseModel |
| `schemas/document-type.md` | BatchResponseModelDocumentTypeResponseModel, CopyDocumentTypeRequestModel, CreateDocumentTypeRequestModel, CreateDocumentTypeTemplateRequestModel, DocumentTypeAllowedParentsResponseModel |
| `schemas/document-version.md` | DocumentVersionResponseModel, PagedDocumentVersionItemResponseModel |
| `schemas/dynamic-root.md` | DynamicRootRequestModel, DynamicRootResponseModel |
| `schemas/health-check.md` | HealthCheckActionRequestModel, HealthCheckGroupPresentationModel, HealthCheckGroupWithResultResponseModel, HealthCheckResultResponseModel, PagedHealthCheckGroupResponseModel |
| `schemas/help.md` | PagedHelpPageResponseModel |
| `schemas/imaging.md` | ImageCropModeModel |
| `schemas/import.md` | EntityImportAnalysisResponseModel |
| `schemas/indexer.md` | IndexResponseModel, PagedIndexResponseModel |
| `schemas/install.md` | DatabaseInstallRequestModel, InstallRequestModel, InstallSettingsResponseModel |
| `schemas/language.md` | CreateLanguageRequestModel, LanguageItemResponseModel, LanguageResponseModel, PagedLanguageResponseModel, UpdateLanguageRequestModel |
| `schemas/log-viewer.md` | LogLevelCountsReponseModel, LogLevelModel, PagedLogMessageResponseModel, PagedLogTemplateResponseModel, PagedLoggerResponseModel |
| `schemas/media.md` | CreateMediaRequestModel, MediaConfigurationResponseModel, MediaResponseModel, MoveMediaRequestModel, PagedMediaCollectionResponseModel |
| `schemas/media-type.md` | BatchResponseModelMediaTypeResponseModel, CopyMediaTypeRequestModel, CreateMediaTypeRequestModel, ImportMediaTypeRequestModel, MediaTypeAllowedParentsResponseModel |
| `schemas/member.md` | CreateMemberRequestModel, MemberConfigurationResponseModel, MemberKindModel, MemberResponseModel, PagedMemberResponseModel |
| `schemas/member-group.md` | CreateMemberGroupRequestModel, MemberGroupResponseModel, PagedMemberGroupResponseModel, UpdateMemberGroupRequestModel |
| `schemas/member-type.md` | BatchResponseModelMemberTypeResponseModel, CopyMemberTypeRequestModel, CreateMemberTypeRequestModel, ImportMemberTypeRequestModel, MemberTypeCompositionRequestModel |
| `schemas/models-builder.md` | ModelsBuilderResponseModel, OutOfDateStatusResponseModel, OutOfDateTypeModel |
| `schemas/news-dashboard.md` | NewsDashboardResponseModel |
| `schemas/object-types.md` | PagedObjectTypeResponseModel |
| `schemas/oembed.md` | OEmbedResponseModel |
| `schemas/package.md` | CreatePackageRequestModel, PackageConfigurationResponseModel, PackageDefinitionResponseModel, PagedPackageDefinitionResponseModel, PagedPackageMigrationStatusResponseModel |
| `schemas/partial-view.md` | CreatePartialViewFolderRequestModel, CreatePartialViewRequestModel, PagedPartialViewSnippetItemResponseModel, PartialViewFolderResponseModel, PartialViewResponseModel |
| `schemas/profiling.md` | ProfilingStatusRequestModel, ProfilingStatusResponseModel |
| `schemas/published-cache.md` | RebuildStatusModel |
| `schemas/redirect-management.md` | PagedRedirectUrlResponseModel, RedirectStatusModel, RedirectUrlStatusResponseModel |
| `schemas/relation.md` | PagedRelationResponseModel |
| `schemas/relation-type.md` | PagedRelationTypeResponseModel, RelationTypeResponseModel |
| `schemas/script.md` | CreateScriptFolderRequestModel, CreateScriptRequestModel, RenameScriptRequestModel, ScriptFolderResponseModel, ScriptResponseModel |
| `schemas/searcher.md` | PagedSearchResultResponseModel, PagedSearcherResponseModel |
| `schemas/security.md` | ResetPasswordRequestModel, ResetPasswordTokenRequestModel, SecurityConfigurationResponseModel, VerifyResetPasswordResponseModel, VerifyResetPasswordTokenRequestModel |
| `schemas/server.md` | RuntimeLevelModel, RuntimeModeModel, ServerConfigurationResponseModel, ServerInformationResponseModel, ServerStatusResponseModel |
| `schemas/stylesheet.md` | CreateStylesheetFolderRequestModel, CreateStylesheetRequestModel, RenameStylesheetRequestModel, StylesheetFolderResponseModel, StylesheetResponseModel |
| `schemas/tag.md` | PagedTagResponseModel |
| `schemas/telemetry.md` | PagedTelemetryResponseModel, TelemetryLevelModel, TelemetryRequestModel, TelemetryResponseModel |
| `schemas/template.md` | CreateTemplateRequestModel, PagedModelTemplateItemResponseModel, SubsetNamedEntityTreeItemResponseModel, TemplateConfigurationResponseModel, TemplateQueryExecuteModel |
| `schemas/temporary-file.md` | TemporaryFileConfigurationResponseModel, TemporaryFileResponseModel |
| `schemas/upgrade.md` | UpgradeSettingsResponseModel |
| `schemas/user.md` | CalculatedUserStartNodesResponseModel, ChangePasswordCurrentUserRequestModel, ChangePasswordUserRequestModel, CreateInitialPasswordUserRequestModel, CreateUserClientCredentialsRequestModel |
| `schemas/user-data.md` | CreateUserDataRequestModel, PagedUserDataResponseModel, UpdateUserDataRequestModel, UserDataModel |
| `schemas/user-group.md` | CreateUserGroupRequestModel, DeleteUserGroupsRequestModel, PagedUserGroupResponseModel, UpdateUserGroupRequestModel, UserGroupResponseModel |
| `schemas/webhook.md` | CreateWebhookRequestModel, PagedWebhookEventModel, PagedWebhookLogResponseModel, PagedWebhookResponseModel, UpdateWebhookRequestModel |
