# Property Editors | CMS

Guide on how to work with and create Property Editors in Umbraco

[This tutorial](/umbraco-cms/tutorials/creating-a-property-editor) contains step-by-step instructions for building a custom Property Editor.

This section describes how to work with and create Property Editors. A Property Editor is the editor used to insert content into Umbraco. [See the Property Editors overview for a detailed definition](/umbraco-cms/fundamentals/backoffice/property-editors).

Custom Property Editors are registered in the [ umbraco-package.json](/umbraco-cms/customizing/umbraco-package) file. This manifest file declares your Property Editor UI extension and links it to a Property Editor Schema. Learn more about the

[package manifest format and registration](/umbraco-cms/customizing/umbraco-package).

Add validation rules to your custom Property Editors to ensure data integrity. Learn how to implement client-side validation using the Form Control Mixin and create custom validation logic for your Property Editor UI.

A Property Editor is composed of two key extensions: [Property Editor Schema](/umbraco-cms/customizing/property-editors/composition/property-editor-schema) and [Property Editor UI](/umbraco-cms/customizing/property-editors/composition/property-editor-ui). These components work together to define the data structure and user interface for content entry in the Umbraco backoffice.

Optionally, you can use a [Property Editor Data Source](/umbraco-cms/customizing/property-editors/composition/property-editor-data-source) to provide data to your Property Editor UI. This will allow the same UI to work with different data sources.

Convert the stored property data value to a useful, strongly-typed object returned by the [Published Content APIs](/umbraco-cms/reference/querying). This allows you to work with rich data types in your views and controllers instead of raw stored values.

Use Property Actions to add additional functionality to your custom Property Editors. This could include custom buttons or actions that appear alongside the editor in the backoffice.

Learn how to integrate and use Property Editors anywhere in the Umbraco backoffice using the `umb-property`

and `umb-property-dataset`

components. This guide covers implementing Property Editors in custom interfaces and scenarios.

Learn how to extend Property Editors to track entity references within the Property Editor. This enables Umbraco to understand relationships between content and helps with features like dependency tracking and content deletion warnings.

Understand how to use the Property Dataset Context API to manage data for multiple properties. This is essential when integrating Property Editors into custom views, workspaces, or scenarios outside of standard content editing.

[Built-in Property Editors](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors)- Explore the Property Editors that come out of the box with Umbraco.[Creating a Property Editor Tutorial](/umbraco-cms/tutorials/creating-a-property-editor)- Step-by-step guide to building your first custom Property Editor.[Adding Configuration](/umbraco-cms/tutorials/creating-a-property-editor/adding-configuration-to-a-property-editor)- Learn how to add configurable settings to your Property Editor.[Adding Server-side Validation](/umbraco-cms/tutorials/creating-a-property-editor/adding-server-side-validation)- Implement server-side validation for your Property Editor.[Custom Value Conversion](/umbraco-cms/tutorials/creating-a-property-editor/custom-value-conversion-for-rendering)- Create Property Value Converters for custom rendering.[Integrating Context](/umbraco-cms/tutorials/creating-a-property-editor/integrating-context-with-a-property-editor)- Work with Umbraco's Context API in your Property Editor.[Default Property Editor Schema Aliases](/umbraco-cms/tutorials/creating-a-property-editor/adding-server-side-validation/default-property-editor-schema-aliases)- Reference list of available Property Editor Schemas.[Full Property Value Converter Examples](/umbraco-cms/customizing/property-editors/full-examples-value-converters)- Complete code examples for implementing Property Value Converters.[Development Flow](/umbraco-cms/customizing/development-flow)- Learn about the development workflow for building Umbraco extensions.

Last updated

Was this helpful?

## Sub-topics

- [Composition](property-editors/composition.md)
- [Property Value Converter Example | CMS](property-editors/full-examples-value-converters.md)
- [Integrate Property Editors | CMS](property-editors/integrate-property-editors.md)
- [Property Actions | CMS](property-editors/property-actions.md)
- [Property Dataset | CMS](property-editors/property-dataset.md)
- [Property Editor Data Source Types | CMS](property-editors/property-editor-data-source-types.md)
- [Sortable Property Values | CMS](property-editors/property-editor-sortable-values.md)
- [Property Editor Validation | CMS](property-editors/property-editor-validation.md)
- [Property Value Converters | CMS](property-editors/property-value-converters.md)
- [Tracking References | CMS](property-editors/tracking.md)
