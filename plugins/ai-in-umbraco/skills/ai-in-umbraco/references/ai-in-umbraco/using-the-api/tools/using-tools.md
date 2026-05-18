# Using Tools | AI in Umbraco

Give AI models the ability to call functions using the Microsoft.Extensions.AI (M.E.AI) tool system.

Defining a Tool

```
using System.ComponentModel;
using Microsoft.Extensions.AI;

public static class WeatherTools
{
    [Description("Gets the current weather for a given city")]
    public static string GetWeather(
        [Description("The city name")] string city)
    {
        // In production, call a real weather API
        return $"The weather in {city} is 22°C and sunny.";
    }
}
```

Calling Chat with Tools

Automatic Tool Invocation

Multiple Tools

Tools with Complex Parameters

Related

Last updated

Was this helpful?