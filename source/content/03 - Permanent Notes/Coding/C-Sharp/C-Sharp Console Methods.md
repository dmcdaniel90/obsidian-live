---
tags:
  - c-sharp/system
---

**Date created**: 2025-04-21
**Tags**: 

## Basic usage

The Console module's most common methods are `WriteLine`, which displays text to the user, and `ReadLine`, which reads input from the user. `ReadKey` reads a single keystroke from the user.

## Adding color

The `Console.Foreground` and `Console.Background` methods can be used to change the Console text and background colours. You must set the value to a `ConsoleColor` property. `Console.ResetColor()` resets the Console colour properties.

```C#
Console.ForegroundColor = ConsoleColor.Cyan;
```

## Simple Example

This `Pause()` method prompts the user to enter any key to continue in dark grey text.

```C#
    static void Pause()
    {
        Console.ForegroundColor = ConsoleColor.DarkGray;
        Console.WriteLine("\nPress any key to return to menu...");
        Console.ResetColor();
        Console.ReadKey();
    }
```

## Connected Ideas


## References / Sources

[MS Documentation - Console Class](https://learn.microsoft.com/en-us/dotnet/api/system.console?view=net-9.0)
[Geeks for Geeks - C# Console Class](https://www.geeksforgeeks.org/console-class-in-c-sharp/)
[Spectre.Console .NET package](https://spectreconsole.net/)

