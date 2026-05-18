# Built In Umbraco Property Editors — Part 2: Date Time Editor → Media Picker | CMS

## Date Time Editor

### Contents

- [Date Only | CMS](#date-only-cms)
- [Date Time (Unspecified) | CMS](#date-time-unspecified-cms)
- [Date Time (with Time Zone) | CMS](#date-time-with-time-zone-cms)
- [Time Only | CMS](#time-only-cms)

---

### Date Only | CMS

Configuration

Editing experience

Adding or editing a value

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a25a76605acb4ec09a2591b6947689f954bead18%252Fdate-only-editor-open.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=5928e31f&sv=2)

Rendering

Display the value

Add values programmatically

Storage format

Last updated

Was this helpful?

`Schema Alias: Umbraco.DateOnly`


`UI Alias: Umb.PropertyEditorUi.DateOnlyPicker`


`Returns: DateOnly?`


The Date Only property editor provides an interface for selecting dates without including time or time zone information. It focuses purely on date selection and returns a `DateOnly`

value.

Configuration

You can configure this property editor in the same way as any standard property editor, using the *Data Types* admin interface.

To set up a property using this editor, create a new *Data Type* and select **Date Only** from the list of available property editors.

This editor has no configuration options.

Editing experience

Adding or editing a value

You will be presented with a date input.

Rendering

The value returned will have the type `DateOnly?`.


Display the value

With Models Builder:

Without Models Builder:

Add values programmatically

This property editor stores values as a JSON object. The object contains the date as an ISO 8601 string with midnight time and UTC offset.

Storage format

The property editor stores values in this JSON format:

The property editor handles date-only values. Time is set to 00:00:00 and offset to +00:00 for storage consistency. These time components are ignored in the Date Only context.

Create a C# model that matches the JSON schema.

Convert your existing date value to

`DateTimeOffset`

for storage.If you have a

`DateOnly`

:If you have a

`DateTime`

:Create an instance of the class with the

`DateTimeOffset`

value.Inject the

`IJsonSerializer`

and use it to serialize the object.Inject the

`IContentService`

to retrieve and update the value of a property of the desired content item.

Last updated

Was this helpful?

Was this helpful?

```
@Model.EventDate
```

```
@Model.Value<DateOnly?>("eventDate")
```

```
{
    "date": "2025-01-01T00:00:00+00:00"
}
```

```
using System.Text.Json.Serialization;

namespace UmbracoProject;

public class DateOnlyValue
{
    /// <summary>
    /// The date value, represented as a <see cref="DateTimeOffset"/> for storage compatibility.
    /// </summary>
    [JsonPropertyName("date")]
    public DateTimeOffset Date { get; init; }
}
```

```
DateOnly dateOnly = DateOnly.FromDateTime(DateTime.Today); // Your existing DateOnly value
DateTimeOffset dateTimeOffset = dateOnly.ToDateTime(TimeOnly.MinValue);
```

```
DateTime dateTime = DateTime.Today; // Your existing DateTime value
DateOnly dateOnly = DateOnly.FromDateTime(dateTime);
DateTimeOffset dateTimeOffset = dateOnly.ToDateTime(TimeOnly.MinValue);
```

```
DateOnlyValue value = new DateOnlyValue
{
    Date = dateTimeOffset
};
```

```
string jsonValue = _jsonSerializer.Serialize(value);
```

```
IContent content = _contentService.GetById(contentKey) ?? throw new Exception("Content not found");

// Set the value of the property with alias 'eventDate'. 
content.SetValue("eventDate", jsonValue);

// Save the change
_contentService.Save(content);
```

---

### Date Time (Unspecified) | CMS

Configuration

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b9427a4e10d72b046bf64157f0e1ae0ece589085%252Fdate-time-unspecified-property-editor-config.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e2af3843&sv=2)

Time format

Editing experience

Adding or editing a value

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-84d794f636ba1a407e90eecf820d003a188709a7%252Fdate-time-unspecified-editor.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f357f264&sv=2)

Rendering

Display the value

Add values programmatically

Storage format

Last updated

Was this helpful?

`Schema Alias: Umbraco.DateTimeUnspecified`


`UI Alias: Umb.PropertyEditorUi.DateTimePicker`


`Returns: DateTime?`


The Date Time (Unspecified) property editor provides an interface for selecting dates and times without including time zone information.

Configuration

You can configure this property editor in the same way as any standard property editor, using the *Data Types* admin interface.

To set up a property using this editor, create a new *Data Type* and select **Date Time (Unspecified)** from the list of available property editors.

You will see the configuration options as shown below.

**Time format**- Specifies the level of precision for time values shown and stored by the editor.

Time format

**HH:mm**- Displays hours and minutes (e.g.,`14:30`

). Suitable for most general use cases.![Date Time Unspecified property editor showing time format in HH:mm format (hours and minutes only)](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-37bdce336f37f42a66a669a6a83d5bc74140eecb%252Fdate-time-time-format-hhmm.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=db399d9b&sv=2)

**HH:mm:ss**- Displays hours, minutes, and seconds (e.g.,`14:30:45`

). Use this when you need more precise timing.![Date Time Unspecified property editor showing time format in HH:mm:ss format (hours, minutes, and seconds)](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f0398d8c07b13376fa782b7fbdb48619ddbd8e45%252Fdate-time-time-format-hhmmss.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=8c6b6039&sv=2)


Editing experience

Adding or editing a value

You will be presented with a date and time input. This editor focuses only on the date and time components, unlike the time zone version.

Rendering

The value returned will have the type `DateTime?`.


Display the value

With Models Builder:

Without Models Builder:

Add values programmatically

This property editor stores values as a JSON object. The object contains the date as an ISO 8601 string.

Storage format

The property editor stores values in this JSON format:

The property editor handles unspecified date and time values without time zone information. The value is stored with offset +00:00 for consistency. The offset is ignored unless you replace this editor with the Date Time (with time zone) version.

Create a C# model that matches the JSON schema.

Convert your existing DateTime value to

`DateTimeOffset`

for storage.Create an instance of the class with the

`DateTimeOffset`

value.Inject the

`IJsonSerializer`

and use it to serialize the object.Inject the

`IContentService`

to retrieve and update the value of a property of the desired content item.

Last updated

Was this helpful?

Was this helpful?

```
@Model.EventDateTime.Value
```

```
@Model.Value<DateTime?>("eventDateTime")
```

```
{
    "date": "2025-01-01T00:00:00+00:00"
}
```

```
using System.Text.Json.Serialization;

namespace UmbracoProject;

public class DateTimeUnspecified
{
    /// <summary>
    /// The date and time value, represented as a <see cref="DateTimeOffset"/> for storage compatibility.
    /// </summary>
    [JsonPropertyName("date")]
    public DateTimeOffset Date { get; init; }
}
```

```
DateTime dateTime = DateTime.Now; // Your existing DateTime value
DateTimeOffset dateTimeOffset = dateTime; // Explicit conversion
```

```
var value = new DateTimeUnspecified
{
    Date = dateTimeOffset
};
```

```
string jsonValue = _jsonSerializer.Serialize(value);
```

```
IContent content = _contentService.GetById(contentKey) ?? throw new Exception("Content not found");

// Set the value of the property with alias 'eventDateTime'. 
content.SetValue("eventDateTime", jsonValue);

// Save the change
_contentService.Save(content);
```

---

### Date Time (with Time Zone) | CMS

Configuration

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-eacc15fb90a26511d98bcdac0de5e73c873a6670%252Fdate-time-with-time-zone-property-editor-config.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=cec106c5&sv=2)

Time format

Time zones

Editing experience

Adding or editing a value

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-c8f435f18686f4d57c4c4d50dfd403efd0164e0d%252Fdate-time-with-time-zone-filtering.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a7a81f95&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e6c7d96577e4f53d83a838b663a502be52632078%252Fdate-time-with-time-zone-single-time-zone.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4cd1ffcd&sv=2)

Rendering

Display the value

Value conversions

Add values programmatically

Storage format

Last updated

Was this helpful?

`Schema Alias: Umbraco.DateTimeWithTimeZone`


`UI Alias: Umb.PropertyEditorUi.DateTimeWithTimeZonePicker`


`Returns: DateTimeOffset?`


The Date Time with Time Zone property editor provides a comprehensive interface for selecting dates, times, and time zones. It stores values as ISO 8601 date/time strings with time zone information. This makes it ideal for applications that need accurate date handling across different time zones.

Configuration

You can configure this property editor in the same way as any standard property editor, using the *Data Types* admin interface.

To set up a property using this editor, create a new *Data Type*. Select **Date Time (with time zone)** from the list of available property editors.

You will see the configuration options as shown below.

**Time format**- Specifies the level of precision for time values shown and stored by the editor.**Time zones**- Controls how time zones are available in the property editor.

Time format

**HH:mm**- Displays hours and minutes (e.g.,`14:30`

). Suitable for most general use cases.![Date Time with Time Zone property editor showing time format in HH:mm format (hours and minutes only)](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-37bdce336f37f42a66a669a6a83d5bc74140eecb%252Fdate-time-time-format-hhmm.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=db399d9b&sv=2)

**HH:mm:ss**- Displays hours, minutes, and seconds (e.g.,`14:30:45`

). Use this when you need more precise timing.![Date Time with Time Zone property editor showing time format in HH:mm:ss format (hours, minutes, and seconds)](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f0398d8c07b13376fa782b7fbdb48619ddbd8e45%252Fdate-time-time-format-hhmmss.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=8c6b6039&sv=2)


Time zones

**All**- Displays the full list of time zones (for example,`America/New_York`

,`Europe/Stockholm`

).**Local**- Displays only the local time zone of the user's browser/computer. Useful for simplifying the UI when time entries should always be based on the user’s local context.**Custom**- Allows you to define a list of time zones. When you select this option, a dropdown appears. You can search and select from the full IANA time zone list. Add multiple zones to restrict user selection to only the zones you specify.Example: Selecting the following time zones:

`Coordinated Universal Time (UTC)`

`Europe/Copenhagen`

Will result in the following editing experience:![Date Time with Time Zone property editor showing custom time zone selection with UTC and Europe/Copenhagen options](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6a87e18702993d5c98c0a92302dc454e07ef8054%252Fdate-time-with-time-zone-custom.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=72d9f218&sv=2)




The selected time zone affects how the date/time is displayed and stored.
When you select a time zone, the value will be saved with the corresponding offset (e.g., `2025-01-01T14:30:00+01:00`

).
Daylight saving time is also taken into account.

Editing experience

Adding or editing a value

You will be presented with date, time, and time zone inputs. The time zone input allows typing, which filters the list of presented time zones.

If your browser time zone appears in the list and no date is stored yet, it will be pre-selected by default.

When you select a time zone different from your browser's local time zone, the editor displays a helpful conversion message. This shows what the selected date and time would be equivalent to in your local time zone, making it easier to understand the time difference.

If only one time zone is available, you will see a label with the time zone name instead.

Rendering

The value returned will have the type `DateTimeOffset?`

. This allows you to work with the date/time value while preserving time zone information.

Display the value

With Models Builder:

Without Models Builder:

Value conversions

Convert to local time:

Convert to UTC time:

Convert to DateTime:

Add values programmatically

This property editor stores values as a JSON object. The object contains both the date (as an ISO 8601 string) and the selected time zone identifier.

Storage format

The property editor stores values in this JSON format:

Create a C# model that matches the JSON schema.

Create an instance of the created class with the desired values.

Inject the

`IJsonSerializer`

and use it to serialize the object.Inject the

`IContentService`

to retrieve and update the value of a property of the desired content item.

Last updated

Was this helpful?

Was this helpful?

```
@Model.EventDateTime.Value
```

```
@Model.Value<DateTimeOffset?>("eventDateTime")
```

```
DateTimeOffset? localTime = Model.EventDateTime?.ToLocalTime();
```

```
DateTimeOffset? utcTime = Model.EventDateTime?.ToUniversalTime();
```

```
DateTime? dateTime = Model.EventDateTime?.DateTime;
DateTime? utcDateTime = Model.EventDateTime?.UtcDateTime;
```

```
{
    "date": "2025-01-01T00:01:00+01:00",
    "timeZone": "Europe/Copenhagen"
}
```

```
using System.Text.Json.Serialization;

namespace UmbracoProject;

public class DateTimeWithTimeZone
{
    /// <summary>
    /// The date and time value, represented as a <see cref="DateTimeOffset"/>.
    /// </summary>
    [JsonPropertyName("date")]
    public DateTimeOffset Date { get; init; }

    /// <summary>
    /// The identifier of the time zone to pre-select in the editor. E.g., "Europe/Copenhagen".
    /// </summary>
    [JsonPropertyName("timeZone")]
    public string TimeZone { get; init; }
}
```

```
var value = new DateTimeWithTimeZone
{
    Date = DateTimeOffset.Now, // The date and time value to store.
    TimeZone = "Europe/Copenhagen" // The time zone to pre-select in the editor.
};
```

```
var jsonValue = _jsonSerializer.Serialize(value);
```

```
IContent content = _contentService.GetById(contentKey) ?? throw new Exception("Content not found");

// Set the value of the property with alias 'eventDateTime'. 
content.SetValue("eventDateTime", jsonValue);

// Save the change
_contentService.Save(content);
```

---

### Time Only | CMS

Configuration

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-79f019ba97093dcf5878504f74cb7170d4c934a4%252Ftime-only-property-editor-config.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=188100b4&sv=2)

Time format

Editing experience

Adding or editing a value

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-18a9b790957943cc90a189ece43216cd95ce1f58%252Ftime-only-editor.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=38285045&sv=2)

Rendering

Display the value

Add values programmatically

Storage format

Last updated

Was this helpful?

`Schema Alias: Umbraco.TimeOnly`


`UI Alias: Umb.PropertyEditorUi.TimeOnlyPicker`


`Returns: TimeOnly?`


The Time Only property editor provides an interface for selecting times. It excludes date and time zone information, and returns strongly-typed `TimeOnly`

values.

Configuration

You can configure this property editor in the same way as any standard property editor, using the *Data Types* admin interface.

To set up a property using this editor, create a new *Data Type* and select **Time Only** from the list of available property editors.

You will see the configuration options as shown below.

**Time format**- Specifies the level of precision for time values shown and stored by the editor.

Time format

**HH:mm**- Displays hours and minutes (e.g.,`14:30`

). Suitable for most general use cases.![Time Only property editor showing time format in HH:mm format (hours and minutes only)](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-7d71ed9c6a46b7f5446385f958669f0d8eafc430%252Ftime-only-time-format-hhmm.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=ade6dc68&sv=2)

**HH:mm:ss**- Displays hours, minutes, and seconds (e.g.,`14:30:45`

). Use this when you need more precise timing.![Time Only property editor showing time format in HH:mm:ss format (hours, minutes, and seconds)](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-324eccfee37d58159af64ccd5720f7ad2f5526a7%252Ftime-only-time-format-hhmmss.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=e3b4e153&sv=2)


Editing experience

Adding or editing a value

You will be presented with a time input. Unlike date-time editors, this editor focuses only on the time component.

Rendering

The value returned will have the type `TimeOnly?`.


Display the value

With Models Builder:

Without Models Builder:

Add values programmatically

This property editor stores values as a JSON object. The object contains the time as an ISO 8601 string with a default date and UTC offset.

Storage format

The property editor stores values in this JSON format:

The property editor handles time-only values. Date is set to a default value (0001-01-01) and offset to +00:00 for storage consistency. The date component is ignored in the Time Only context.

Create a C# model that matches the JSON schema.

Convert your existing time value to

`DateTimeOffset`

for storage.If you have a

`TimeOnly`

:If you have a

`DateTime`

:Create an instance of the class with the

`DateTimeOffset`

value.Inject the

`IJsonSerializer`

and use it to serialize the object.Inject the

`IContentService`

to retrieve and update the value of a property of the desired content item.

Last updated

Was this helpful?

Was this helpful?

```
@Model.StartHours
```

```
@Model.Value<TimeOnly?>("startHours")
```

```
{
    "date": "0001-01-01T14:30:00+00:00"
}
```

```
using System.Text.Json.Serialization;

namespace UmbracoProject;

public class TimeOnlyValue
{
    /// <summary>
    /// The time value, represented as a <see cref="DateTimeOffset"/> for storage compatibility.
    /// </summary>
    [JsonPropertyName("date")]
    public DateTimeOffset Date { get; init; }
}
```

```
TimeOnly timeOnly = TimeOnly.FromDateTime(DateTime.Now); // Your existing TimeOnly value
DateTimeOffset dateTimeOffset = new DateTimeOffset(DateOnly.MinValue, timeOnly, TimeSpan.Zero);
```

```
DateTime dateTime = DateTime.Now; // Your existing DateTime value
TimeOnly timeOnly = TimeOnly.FromDateTime(dateTime);
DateTimeOffset dateTimeOffset = new DateTimeOffset(DateOnly.MinValue, timeOnly, TimeSpan.Zero);
```

```
TimeOnlyValue value = new TimeOnlyValue
{
    Date = dateTimeOffset
};
```

```
string jsonValue = _jsonSerializer.Serialize(value);
```

```
IContent content = _contentService.GetById(contentKey) ?? throw new Exception("Content not found");

// Set the value of the property with alias 'startHours'. 
content.SetValue("startHours", jsonValue);

// Save the change
_contentService.Save(content);
```

---

---


## DateTime | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-2ab6abcd37ca1c7591acec4da2fcd1502b87ddfa%252FDate-time-picker-v16.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=23fbe9af&sv=2)

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-799a7ed00ba724f5d4220efd161914707bb5b849%252FDate-picker-with-content-v16.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1594e689&sv=2)

MVC View Example - displays a datetime

With Models Builder

Without Models Builder

Add values programmatically

Last updated

Was this helpful?

`Schema Alias: Umbraco.DateTime`


`UI Alias: Umb.PropertyEditorUi.DatePicker`


`Returns: DateTime`


Displays a calendar UI for selecting dates which are saved as a DateTime value.

New [Date Time property editors](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/date-time-editor) are available. They offer more focused functionality and time zone support. These editors will eventually replace the current Date Time property editor, so consider using them for new implementations.

Data Type Definition Example

There is one setting available for manipulating the DateTime property.

The setting involves defining the format. The default date format in the Umbraco backoffice is `YYYY-MM-DD HH:mm:ss`

, but you can change it to a different format. See for the supported formats.

Content Example

MVC View Example - displays a datetime

With Models Builder

Without Models Builder

Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of a property editor you need the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

Although the use of a GUID is preferable, you can also use the numeric ID to get the page:

If Models Builder is enabled you can get the alias of the desired property without using a magic string:

Last updated

Was this helpful?

Was this helpful?

```
@Model.DatePicker
```

```
@Model.Value("datePicker")
```

```
@using Umbraco.Cms.Core.Services
@inject IContentService ContentService
@{
    // Create a variable for the GUID of the page you want to update
    var guid = new Guid("32e60db4-1283-4caa-9645-f2153f9888ef");

    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page

    // Set the value of the property with alias 'datePicker'
    content.SetValue("datePicker", DateTime.Now);

    // Save the change
    ContentService.Save(content);
}
```

```
@{
    // Get the page using it's id
    var content = ContentService.GetById(1234); 
}
```

```
@using Umbraco.Cms.Core.PublishedCache
@inject IPublishedContentTypeCache PublishedContentTypeCache
@{

    // Set the value of the property with alias 'datePicker'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.DatePicker).Alias, DateTime.Now);
}
```

---


## Decimal | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-98474c0599911c5cd003dd0de497e1f82920688b%252Fcontent-example.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=889800fe&sv=2)

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-43de1d230578f944bf519972ed79e6606ac37bc7%252Fcontent-example.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4ea5e97b&sv=2)

MVC View Example

With Models Builder

Without Models Builder

Add values programmatically

Last updated

Was this helpful?

`Schema Alias: Umbraco.Decimal`


`UI Alias: Umb.PropertyEditorUi.Decimal`


`Returns: decimal`


Data Type Definition Example

In the example above the possible values for the input field would be [8, 8.5, 9, 9.5, 10]

*All other values will be removed in the content editor when saving or publishing.*

If the value of **Step Size** is not set then all decimal values between 8 and 10 is possible to input in the content editor.

Content Example

MVC View Example

With Models Builder

Without Models Builder

Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of a property editor you need the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

Although the use of a GUID is preferable, you can also use the numeric ID to get the page:

If Models Builder is enabled you can get the alias of the desired property without using a magic string:

Last updated

Was this helpful?

Was this helpful?

```
@Model.MyDecimal
```

```
@Model.Value("MyDecimal")
```

```
@using Umbraco.Cms.Core.Services
@inject IContentService ContentService
@{
    // Create a variable for the GUID of the page you want to update
    var guid = Guid.Parse("32e60db4-1283-4caa-9645-f2153f9888ef");

    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page

    // Set the value of the property with alias 'myDecimal'. 
    content.SetValue("myDecimal", 3);

    // Save the change
    ContentService.Save(content);
}
```

```
@{
    // Get the page using it's id
    var content = ContentService.GetById(1234); 
}
```

```
@using Umbraco.Cms.Core.PublishedCache
@inject IPublishedContentTypeCache PublishedContentTypeCache
@{
    // Set the value of the property with alias 'myDecimal'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.MyDecimal).Alias, 3);
}
```

---


## Document Picker | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-18573dd59d25e5ec35e0810c0077be302c41d3da%252FDocument-Picker-DataType.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a78b68ea&sv=2)

Document Picker Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-7a5462d5c5f1a627ca5e6080df8923d65ab4f47a%252FContent-Picker-Content-v10.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=89f22b0e&sv=2)

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

Last updated

Was this helpful?

`Schema Alias: Umbraco.ContentPicker`


`UI Alias: Umb.PropertyEditorUi.DocumentPicker`


`Returns: IPublishedContent`


The Document Picker opens a panel to pick a specific page from the content structure. The value saved is the selected nodes [UDI](/umbraco-cms/reference/querying/udi-identifiers).

The Document Picker was formerly known as the **Content Picker** in version 13 and below.

The renaming is purely a client-side UI change, meaning the property editor still uses the `Umbraco.ContentPicker`

schema alias.

The change was made as the word **Content** in the backoffice acts as an umbrella term covering the terms Document, Media, and Member.

Data Type Definition Example

Document Picker Example

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of a property editor you need the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

Although the use of a GUID is preferable, you can also use the numeric ID to get the page:

If Models Builder is enabled you can get the alias of the desired property without using a magic string:

Last updated

Was this helpful?

Was this helpful?

```
@{
    IPublishedContent typedContentPicker = Model.Value<IPublishedContent>("featurePicker");
    if (typedContentPicker != null)
    {
        <p>@typedContentPicker.Name</p>
    }
}
```

```
@{
    IPublishedContent typedContentPicker = Model.FeaturePicker;
    if (typedContentPicker != null)
    {
        <p>@typedContentPicker.Name</p>
    }
}
```

```
@using Umbraco.Cms.Core
@using Umbraco.Cms.Core.Services
@inject IContentService ContentService
@{
    // Create a variable for the GUID of the page you want to update
    var guid = Guid.Parse("32e60db4-1283-4caa-9645-f2153f9888ef");

    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page

    // Get the page you want to assign to the document picker
    var page = Umbraco.Content("665d7368-e43e-4a83-b1d4-43853860dc45");

    // Create an Udi of the page
    var udi = Udi.Create(Constants.UdiEntityType.Document, page.Key);

    // Set the value of the property with alias 'featurePicker'.
    content.SetValue("featurePicker", udi.ToString());

    // Save the change
    ContentService.Save(content);
}
```

```
@{
    // Get the page using it's id
    var content = ContentService.GetById(1234);
}
```

```
@using Umbraco.Cms.Core.PublishedCache
@inject IPublishedContentTypeCache PublishedContentTypeCache
@{
    // Set the value of the property with alias 'featurePicker'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.FeaturePicker).Alias, udi.ToString());
}
```

---


## Dropdown | CMS

Settings

Enable multiple choice

Add options

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ea1da4a3cfcd980698811835cbcf4c0c0f02d385%252FDropdown-DataType.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=61c087ef&sv=2)

Content Example

Single Value

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-be48cc06e30eb4c5e2610d24173186389e3d6461%252FDropdownSingle-Content.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c253dfed&sv=2)

Multiple Values

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9d2fd30a993190ebb91d47162ce0ca9ed4ec5937%252FDropdownMultiple-Content.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=35b22db3&sv=2)

MVC View Example

Single item - without Models Builder

Multiple items - without Models Builder

Single item - with Models Builder

Multiple items - with Models Builder

Add values programmatically

Last updated

Was this helpful?

---


## Email Address | CMS

In this article you can learn how to use the build in email property editor

Settings

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6806c536bb234da652a6b905905818a1c6f488b2%252Femailaddress-datatype.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f08d26d5&sv=2)

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-71b57446e232dd9f5be1e543718d47969bd825ad%252FEmailAddress-Content-v10.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7c1a6a95&sv=2)

MVC View Example

Without Modelsbuilder

With Modelsbuilder

Add value programmatically

Last updated

Was this helpful?

In this article you can learn how to use the build in email property editor

`Schema Alias: Umbraco.EmailAddress`


`UI Alias: Umb.PropertyEditorUi.EmailAddress`


`Returns: String`


Displays an email address.

Settings

The Email Address Property Editor does not come with any further configuration. The property can be configured once it has been added to a Document Type.

Content Example

MVC View Example

Without Modelsbuilder

With Modelsbuilder

Add value programmatically

See the example below to learn how a value can be added or changed programmatically to an Email-address property. To update a value of a property editor you need the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

The value sent to an EmailAddress property needs to be a correct email address, For example: .

It is recommended that you set up validation on this property, in order to verify whether the value added is in the correct format.

Last updated

Was this helpful?

Was this helpful?

```
@if (Model.HasValue("email"))
{
    var emailAddress = Model.Value<string>("email");
    <p>@emailAddress</p>
}
```

```
@if (!string.IsNullOrWhiteSpace(Model.Email))
{
    <p>@Model.Email</p>
}
```

```
@using Umbraco.Cms.Core.Services;

@inject IContentService Services;
@{
    // Get access to ContentService
    var contentService = Services;

    // Create a variable for the GUID of your page
    var guid = new Guid("796a8d5c-b7bb-46d9-bc57-ab834d0d1248");

    // Get the page using the GUID you've just defined
    var content = contentService.GetById(guid);
    // Set the value of the property with alias 'email'
    content.SetValue("email", "[email protected]");

    // Save the change
    contentService.Save(content);
}
```

---


## Entity Data Picker | CMS

Last updated

Was this helpful?

`Schema Alias: Umbraco.EntityDataPicker`


`UI Alias: Umb.PropertyEditorUi.EntityDataPicker`


`Returns: Umbraco.Cms.Core.Models.EntityDataPickerValue`


`Supported Data Source Types:`

[Picker](/umbraco-cms/customizing/property-editors/property-editor-data-source-types/picker)

The Entity Data Picker property editor allows editors to pick one or more entities from a configurable data source. The selected entities are stored as an array of strings, where each string represents the ID of the selected entity.

With Models Builder

```
@inherits Umbraco.Cms.Web.Common.Views.UmbracoViewPage<EntityDataPickerTest>
@{
    Layout = null;
}
<html lang="en">
<head>
    <title>Entity Data Picker</title>
</head>
<body>
@if (Model.MyEntityPicker is null)
{
    <p>No entity picker value found</p>
}
else
{
    <p>Data source: <strong>@Model.MyEntityPicker.DataSource</strong></p>
    <p>Picked IDs:</p>
    <ul>
        @foreach (string id in Model.MyEntityPicker.Ids)
        {
            <li>@id</li>
        }
    </ul>
}
</body>
</html>
```

Without Models Builder

Last updated

Was this helpful?

Was this helpful?

```
@using Umbraco.Cms.Core.Models
@inherits Umbraco.Cms.Web.Common.Views.UmbracoViewPage
@{
    Layout = null;
    var entityDataPickerValue = Model.Value<EntityDataPickerValue>("myEntityPicker");
}
<html lang="en">
<head>
    <title>Entity Data Picker</title>
</head>
<body>
@if (entityDataPickerValue is null)
{
    <p>No entity picker value found</p>
}
else
{
    <p>Data source: <strong>@entityDataPickerValue.DataSource</strong></p>
    <p>Picked IDs:</p>
    <ul>
        @foreach (string id in @entityDataPickerValue.Ids)
        {
            <li>@id</li>
        }
    </ul>
}
</body>
</html>
```

---


## Eye Dropper Color Picker | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-0f1fb36893afa0a783cba65468e1d92bbe2830fc%252FEye-Dropper-Color-Picker-DataType.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=450c7493&sv=2)

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d8ce4de3f88e90c037928e28fdd5c3c104523835%252FEye-Dropper-Color-Picker-Content.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a80e6e8e&sv=2)

Example with Models Builder

Example without Models Builder

Add values programmatically

Last updated

Was this helpful?

`Schema Alias: Umbraco.ColorPicker.EyeDropper`


`UI Alias: Umb.PropertyEditorUi.EyeDropper`


`Returns: string`


The Eye Dropper Color picker allows you to choose a color from the full color spectrum using HEX and RGBA.

Data Type Definition Example

Content Example

Example with Models Builder

Example without Models Builder

Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of a property editor you need the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

Although the use of a GUID is preferable, you can also use the numeric ID to get the page:

If Models Builder is enabled you can get the alias of the desired property without using a magic string:

Last updated

Was this helpful?

Was this helpful?

```
@{
    var color = Model.Color?.ToString();

    if (color != null)
    {
        <body style="background-color: @color"></body>
    }
}
```

```
@{
    var color = Model.Value<string>("Color");

    if (color != null)
    {
        <body style="background-color: @color"></body>
    }
}
```

```
@using Umbraco.Cms.Core.Services
@inject IContentService ContentService
@{
    // Create a variable for the GUID of the page you want to update
    var guid = Guid.Parse("32e60db4-1283-4caa-9645-f2153f9888ef");

    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page

    // Set the value of the property with alias 'color'.
    content.SetValue("color", "#6fa8dc");
    
    // Save the change
    ContentService.Save(content);
}
```

```
@{
    // Get the page using it's id
    var content = ContentService.GetById(1234); 
}
```

```
@using Umbraco.Cms.Core.PublishedCache
@inject IPublishedContentTypeCache PublishedContentTypeCache
@{
    // Set the value of the property with alias 'color'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.Color).Alias, "#6fa8dc");
    
    // Set the value of the property with alias 'theme'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.Theme).Alias, "rgba(111, 168, 220, 0.7)");
}
```

---


## File Upload | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8ae3a910d2061a5e4d9178281ece8be933e072bf%252Ffile-upload-definition.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a14183e2&sv=2)

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-92193a21f03675d9b5257f54337373fc7d6de483%252Ffileupload-content-empty.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=59f9b2a6&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-baf785c66085e1af3af26ee92f68c28b7c9c9889%252Ffileupload-content.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a7b1dc&sv=2)

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

Last updated

Was this helpful?

`Schema Alias: Umbraco.UploadField`


`UI Alias: Umb.PropertyEditorUi.UploadField`


`Returns: string`


Adds an upload field, which allows documents or images to be uploaded to Umbraco.

You can define which file types should be accepted through the upload field.

For uploading and adding files and images to your Umbraco project, we recommend using the Media Picker.

Find the full documentation for the property in the [Media Picker](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/media-picker-3) article.

Data Type Definition Example

Content Example

In code, the property is a string, which references the location of the file.

Example: `"/media/o01axaqu/guidelines-on-remote-working.pdf"`


MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of this property editor you need the and the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

If Models Builder is enabled you can get the alias of the desired property without using a magic string:

Last updated

Was this helpful?

Was this helpful?

```
@if (Model.HasValue("myFile"))
{
    var myFile = Model.Value<string>("myFile");

    <a href="@myFile">@System.IO.Path.GetFileName(myFile)</a>
}
```

```
@if (Model.HasValue("myFile"))
{
   <a href="@Model.MyFile">@System.IO.Path.GetFileName(Model.MyFile)</a>
}
```

```
@using System.Net
@using Umbraco.Cms.Core
@using Umbraco.Cms.Core.Services
@using Umbraco.Cms.Core.PropertyEditors
@using Umbraco.Cms.Core.IO
@using Umbraco.Cms.Core.Serialization
@using Umbraco.Cms.Core.Strings
@inject MediaFileManager MediaFileManager
@inject IShortStringHelper ShortStringHelper
@inject IContentTypeBaseServiceProvider ContentTypeBaseServiceProvider
@inject IContentService ContentService
@inject IMediaService MediaService
@inject IJsonSerializer Serializer
@inject MediaUrlGeneratorCollection MediaUrlGeneratorCollection
@{
    // Create a variable for the GUID of the parent where you want to add a child item
    var guid = Guid.Parse("32e60db4-1283-4caa-9645-f2153f9888ef");

    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page

    // Create a variable for the file you want to upload, in this case the Our Umbraco logo
    var imageUrl = "https://our.umbraco.com/assets/images/logo.svg";

    // Create a request to get the file
    var request = WebRequest.Create(imageUrl);
    var webResponse = request.GetResponse();
    var responseStream = webResponse.GetResponseStream();

    // Get the file name 
    var lastIndex = imageUrl.LastIndexOf("/", StringComparison.Ordinal) + 1;
    var filename = imageUrl.Substring(lastIndex, imageUrl.Length - lastIndex);

    // Create a media file
    var media = MediaService.CreateMediaWithIdentity("myImage", -1, "File");
    media.SetValue(MediaFileManager, MediaUrlGeneratorCollection, ShortStringHelper, ContentTypeBaseServiceProvider, Constants.Conventions.Media.File, filename, responseStream);
    // Save the created media 
    MediaService.Save(media);

    // Get the published version of the media (IPublishedContent)
    var publishedMedia = Umbraco.Media(media.Id);

    // Set the value of the property with alias 'myFile' 
    content.SetValue("myFile", publishedMedia.Url());

    // Save the child item
    ContentService.Save(content);
}
```

```
@using Umbraco.Cms.Core.PublishedCache
@inject IPublishedContentTypeCache PublishedContentTypeCache
@{
    // Set the value of the property with alias 'myFile'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.MyFile).Alias, publishedMedia.Url();
}
```

---


## Image Cropper | CMS

Settings

Define Crops

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-786888e25e94795c7a5d8fcf18e4cb8b21c21311%252FimageCropper.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fd98b189&sv=2)

Content Example

Uploading images

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-94e5f4e305625a2b93b48c8a6ded91298a432b39%252FimageCropper-upload-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=5891c54e&sv=2)

Set focal point

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8124cc536813c427171c1a3410d47e0bc76b7dfd%252FimageCropper-focalpoint.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=636daffd&sv=2)

Crop and resize

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-de2e956bea59bab145a60a39b17fc5057f238bb3%252FimageCropper-crop.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=6759544d&sv=2)

Powered by ImageSharp.Web

Sample code

Example to output a "banner" crop from a cropper property with the property alias "customCropper"

Example to dynamically create a crop using the focal point - in this case 300 x 400px image

CSS background example to output a "banner" crop

Add values programmatically

Get all the crop urls for a specific image

Sample on how to change the format of the image

Last updated

Was this helpful?

---


## Label | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-11094fa224c166cc490c39c9ecffc11fea66ef7d%252FLabel-Setup.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3494818c&sv=2)

Value type

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8542a32ceb9931e0ec872ed83beea444181083d7%252FLabel-Content-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a722a34e&sv=2)

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

Last updated

Was this helpful?

`Schema Alias: Umbraco.Label`


`UI Alias: Umb.PropertyEditorUi.Label`


`Returns: String`


Label is a non-editable control and can only be used to display a pre-set value.

Data Type Definition Example

Value type

If you want to set a value other than a String, you can define the data using one of the other available Data Types. These include Decimal, Date/time, Time, Integer, and Big integer.

There is also a Value Type: Long string if you need to set a long string value for your Label.

Content Example

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of a property editor you need the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

Although the use of a GUID is preferable, you can also use the numeric ID to get the page:

If Models Builder is enabled you can get the alias of the desired property without using a magic string:

Last updated

Was this helpful?

Was this helpful?

```
@{
    if (Model.HasValue("pageLabel")){
        <p>@(Model.Value("pageLabel"))</p>
    }
}
```

```
@{
    if (!string.IsNullOrEmpty(Model.PageLabel))
    {
        <p>@Model.PageLabel</p>
    }
}
```

```
@using Umbraco.Cms.Core.Services
@inject IContentService ContentService
@{
    // Create a variable for the GUID of the page you want to update
    var guid = Guid.Parse("32e60db4-1283-4caa-9645-f2153f9888ef");
    
    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page
    
    // Set the value of the property with alias 'pageLabel'. 
    content.SetValue("pageLabel", "A pre-set string value");
    
    // Save the change
    ContentService.Save(content);
}
```

```
@{
    // Get the page using it's id
    var content = ContentService.GetById(1234); 
}
```

```
@using Umbraco.Cms.Core.PublishedCache
@inject IPublishedContentTypeCache PublishedContentTypeCache
@{
    // Set the value of the property with alias 'pageLabel'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.MyLabel).Alias, "A pre-set string value");
}
```

---


## Markdown Editor | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-0b4b46160d66ee3bc374fec763ec383611afc8ca%252FMarkdown-Editor-definition-example.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c1d86316&sv=2)

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e71cbb2825f8a98fa1a56d80ff9e4abcf90af03d%252FMarkdown-Editor-content-example.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=dd97ea6d&sv=2)

Explanation of buttons from left to right

| Function | Shortcut | Further explanation |
|---|---|---|
| toggle bold text | Ctrl + B | |
| toggle italic text | Ctrl + I | |
| insert link | Ctrl + L | This opens the Select Link interface. |
| toggle quote | Ctrl + Q | |
| toggle code block | Ctrl + K | |
| insert image | Ctrl + G | This opens the Select Media interface. |
| toggle ordered list | Ctrl + O | |
| toggle unordered list | Ctrl + U | |
| toggle heading | Ctrl + H | This toggles between h1, h2 and off. |
| toggle a hr | ||
| undo | Ctrl + Z | |
| redo | Ctrl + Y |

Other functionality

| Function | Shortcut |
|---|---|
| select all | Ctrl + A |
| copy | Ctrl + C |
| paste | Ctrl + V |

Markdown to HTML Conversion

MVC View Example

With Models Builder

Without Models Builder

Add values programmatically

Last updated

Was this helpful?

---


## Media Picker | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-bc6ac25056b542533c0659f65b2dab4023764d66%252FMediaPicker-DataType.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a8c553e8&sv=2)

Accepted types

Pick multiple items

Amount

Start node

Ignore user start nodes

Enable Focal Point

Image Crops

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4cf7c146c4aa22f659b383057ce788ade1e28ab6%252FMedia-Picker3-Content.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c5d76dc8&sv=2)

MVC View Example

Multiple enabled without Models Builder

Multiple enabled without Models Builder to retrieve IEnumerable data

Multiple enabled with Models Builder

Multiple disabled without Models Builder

Multiple disabled with Models Builder

Using crops

Explicitly retrieving global crops

Add values programmatically

Last updated

Was this helpful?

---
