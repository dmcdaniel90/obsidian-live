---
tags:
  - c-sharp/types
---

**Date created**: 2025-04-21
**Tags**: [[c-sharp]], [[c-sharp#numbers]]

## Summary

The `TryParse` method attempts to convert a string to a number, while also handling any exceptions.

## Usage


To use the `TryParse` method in C#, you can follow these steps:

1. **Choose the Numeric Type**: Determine which numeric type you want to parse the string into (e.g., `int`, `long`, `decimal`, etc.).
2. **Call the TryParse Method**: Use the static `TryParse` method of the chosen numeric type. This method takes two parameters: the string you want to parse and an output variable that will hold the parsed numeric value if the parsing is successful.
3. **Check the Result**: The `TryParse` method returns a boolean value indicating whether the parsing was successful. If it returns `true`, the output variable will contain the parsed value; if it returns `false`, the output variable will be set to zero.

Here is an example of using `int.TryParse`:

```C#
int i = 0;
string s = "108";  
bool result = int.TryParse(s, out i); // i now = 108
```

In this example, if the string `s` contains a valid integer representation, `result` will be `true`, and `i` will hold the parsed integer value. If `s` is not a valid integer, `result` will be `false`, and `i` will be set to zero.

>[!hint] The `TryParse` method is used with other data types as well. See the [[#References / Sources]] section

## References / Sources

[Documentation: Int32.TryParse](https://learn.microsoft.com/en-us/dotnet/api/system.int32.tryparse?view=net-9.0)
[MS-Learn: How to convert a string to a numer](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/types/how-to-convert-a-string-to-a-number)
[TryParse in C#: Full Guide](https://www.bytehide.com/blog/tryparse-csharp)
