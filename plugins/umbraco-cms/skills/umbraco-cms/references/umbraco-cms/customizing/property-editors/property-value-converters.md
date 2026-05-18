# Property Value Converters | CMS

A guide to creating a custom Property Value Converter in Umbraco

Create a Property Value Converter

```
public class ContentPickerValueConverter : IPropertyValueConverter
```

Implement information methods

`IsConverter(IPublishedPropertyType propertyType)`

`IsValue(object value, PropertyValueLevel level)`

`GetPropertyValueType(IPublishedPropertyType propertyType)`

`GetPropertyCacheLevel(IPublishedPropertyType propertyType)`

`PropertyCacheLevel.Element`

`PropertyCacheLevel.Elements`

`PropertyCacheLevel.None`

`PropertyCacheLevel.Unknown`

Implement conversion methods

`ConvertSourceToIntermediate(IPublishedElement owner, IPublishedPropertyType propertyType, object source, bool preview)`

`ConvertIntermediateToObject(IPublishedElement owner, IPublishedPropertyType propertyType, PropertyCacheLevel referenceCacheLevel, object inter, bool preview)`

Override existing Property Value Converters

Full example

Last updated

Was this helpful?