---
tags:
  - zerotomastery
  - c-sharp
---

**Date created**: 2025-04-13
**Tags**: 

## Outline

1. [[#Review]]
2. INTERMEDIATE C# PROGRAMMING
3. C# ARRAYS & COLLECTIONS
4. ADVANCED C#
5. LINQ FUNDAMENTALS
6. AUTOMATED TESTING 
7. INTRODUCTION TO WEB DEVELOPMENT IN .NET
8. ASP.NET CORE FUNDAMENTALS
9. ASP.NET CORE RAZOR PAGES
10. ASP.NET CORE MVC
11. ASP.NET CORE BLAZOR 

## Review

### Setup

>[!tip] In VS Code, you can add C# features by installing the .NET Extension Pack by Microsoft. You may need to also install the .NET SDK.

Verify installation by running in the terminal:
```bash
dotnet --list-sdks ## Lists the installed SDKs; we need .NET
dotnet --list-runtimes ## Lists the current installed runtimes
```

Creating a new project
```bash
dotnet new console ## Create new project using console template
```


Run a project
```bash
dotnet run
```

>[!tip] Install the Roslynator VS Code plugin to help with C# analysis and refactoring

### Setting up the VS code Debugger with C\#

>[!important] On the first run, you must click "Generate C# Assets for Build and Debug"

### Testing in VS Code

Create a tests project
```bash
dotnet new mstest ## Create a new test template
dotnet test ## Run all tests
```

Reference a another project (The project to be tested)
```bash
dotnet add $test.csproj reference $path_to_project
```

## Basics

Writing to the console. The `ReadKey()` method can be used in console to prompt the user to press any key to continue.
```C#
Console.WriteLine(string); // Writes a string to the console
Console.ReadKey(); // Reads the next keypress and proceed to the next line
Console.WriteLine($"Hello there, {name}"); // Using variables
Console.WriteLine(@$"Choose a colour: 
					A. Red
					B. Yellow
					C. Green
					"); // Multi-line
```

A few basic types, also with the optional (?) flag
```C#
bool calculating = true; // Boolean
float baseValue; // Floating Number
string? input1; // Optional String
```

Prompting the user, then capturing user input into a variable
```C#
Console.WriteLine("Enter a number");
input1 = Console.ReadLine();
```

Safe parsing of text to numbers
```C#
float.tryParse(input1, out input1parsed);
```

Switch statements
```C#
switch(oper) {
	case "+":
		baseValue = baseValue + value2;
		break; // Remember to break
	...
	default:
		Console.WriteLine("Invalid");
		break;
}
```

### Reviewing the MyAccount App

The `decimal` type, which accepts numbers `m` suffix, is often used in financial and monetary calculations due to its high precision
```C#
decimal defaultBalance = 2500.00m;
```

#### Class Structure
```C#
class Account {
	
	// Local variables
	public string Owner;
	public decimal Balance;
	public decimal IntRate;

	// Constructor
	public Account(string owner, decimal openingBalance, decimal intRate)
	{
		Owner = owner;
		Balance = openingBalance;
		IntRate = intRate;
	}

	// Static method to create a new class. "Create a method on the Account class that takes an account of type Account as an argument and returns a new Account"
	public static Account OpenAccount(Account account) {
		...
		return new Account(owner, openingBalance, intRate);
	};

	// Function overloading; multiple versions of methods with different parameters
	public void withdrawChecking(CheckingAccount checking);
	public void withdrawChecking(CheckingAccount checking, string?, transferAmt)
}
```

#### Auto-Implemented Getters and Setters

```C#
// long version
class Person
{
	private string name;
	
	public string GetName()
	{
		return name;
	}
	public void SetName(string value)
	{
		if (!string.IsNullOrEmpty(value))
		{
			name = value; // Assign the value if it's not null or empty
		}
	}
}

// short version
class PersonTwo
{
	public string Name { get; set; }
	public string Age { get; private set; }
}

```

[[↪ Atomic note]]
[[↪ Atomic note]]
[[↪ Atomic note]]


## References / Sources

[Outgoing link]('https://google.com)
[Outgoing link]('https://google.com)
[Outgoing link]('https://google.com)

