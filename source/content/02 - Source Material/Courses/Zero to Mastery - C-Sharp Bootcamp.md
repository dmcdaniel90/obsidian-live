---
tags:
  - zerotomastery
  - c-sharp
---

**Date created**: 2025-04-13
**Tags**: 

## Outline

1. [[#Setup]]
2. [[#Basics]]
3. [[#Variable Types]]
4. [[#Arrays and Collection Types]]
5. ADVANCED C#
6. LINQ FUNDAMENTALS
7. AUTOMATED TESTING 
8. INTRODUCTION TO WEB DEVELOPMENT IN .NET
9. ASP.NET CORE FUNDAMENTALS
10. ASP.NET CORE RAZOR PAGES
11. ASP.NET CORE MVC
12. ASP.NET CORE BLAZOR 
13. [C# Documentation]()

## Setup

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

Create a test project
```bash
dotnet new mstest ## Create a new test template
dotnet test ## Run all tests
```

Reference another project (The project to be tested)
```bash
dotnet add $test.csproj reference $path_to_project
```

## Basics

Writing to the console. The `ReadKey()` method can be used in console to prompt the user to press any key to continue.
```csharp
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
```csharp
bool calculating = true; // Boolean
float baseValue; // Floating Number
string? input1; // Optional String
```

`string`s and `char`s are used for "presentation, not calculation". If you need to perform a mathematical operation on numeric values, you should use an `int` or `decimal`. If you have data for presentation or text manipulation, you should use a `string` or `char` data type.

Prompting the user, then capturing user input into a variable
```csharp
Console.WriteLine("Enter a number"); // Must be in double quotes
input1 = Console.ReadLine(); // Statements end with a semi-colon!
```

Safe parsing of text to numbers
```csharp
float.tryParse(input1, out input1parsed);
```

Switch statements
```csharp
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
```csharp
decimal defaultBalance = 2500.00m;
```

#### Class Structure
```csharp
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

```csharp
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

## Variable Types

### Const

Prevents a variable from changing its value. can use any primitive. Can be used as a local constant or in classes. It is fully evaluated at compile time.

Must be placed before the variable type. Convention is to use an uppercase first letter in naming.

### Garbage Collection

Unlike C and other low-level languages, .NET is a managed-memory platform that has its own garbage collector to manage the allocation and release of memory in .NET applications.

It is part of the .NET runtime and can be used with F# and Visual Basic as well.

The two types of memory are the Stack and the Heap. The Stack is an array (ordered, accesses one by one LIFO aka only from the top). Method arguments and local variables of primitives are common items on the stack. The heap is what is used in garbage collection. They can be accessed in any order and are data objects accessed through references.

Memory that isn't dependent on another piece of memory is potential to be collected. The .NET runtime decides this.

### Enumeration

A set of named, constant values. Allows us to check types during compilation. They are easier to read, more extensible, and more type-safe when multiple defined values are present.

```csharp
var temperature = new Temperature(TemperatureUnit.Celsius, 10);

enum TemperatureUnit
{
Celsius,
Fahrenheit
Kelvin
}

class Temperature
{
	public Temperature(TemperatureUnit unit, decimal value)
	{
		Unit = unit;
		Value = value;
	}
	// Getters and Setters
	public TemperatureUnit Unit { get; set; }
	public decimal Value { get; set; }

	public decimal ValueInCelsius
	{
		get
		{
			if (Unit == TemperatureUnit.Celsius)
			{
				return Value; 
			}
			if (Unit == TemperatureUnit.Fahrenheit)
			{
				return (Value - 32 * 5 / 9);
			}
			if (Unit == TemperatureUnit.Kelvin)
			{
				return Value - 2473.15m;
			}

			return 0;
		}
	}
} // This is lengthy to do. We'll see a better option later.

```

### Switch Expressions

```csharp

// previous code...

	public decimal ValueInCelsius
	{
		get
		{
			switch (Unit)
			{
				case TemperatureUnit.Celsius:
					return Value;
				case: TemperatureUnit.Fahrenheit:
					return (Value - 32) * 5 / 9;
				case: TemperatureUnit.Kelvin:
					return Value - 273.15m;
				default:
					return 0;
			}
		}
	}
} // This is a switch statement

// Switch expression. Is declarative, instead of imperative. A return value is needed for every case

public decimal ValueInCelsius
{
	get
	{
		return Unit switch
		{
			TemperatureUnit.Celcius when Value > 100 => Math.Round(Value, 0), // Guard clause when a more specific option is needed
			TemperatureUnit.Celsius => Value, // Lambda or arrow operator
			TemperatureUnit.Fahrenheit => (Value - 32) * 5 / 9,
			TemperatureUnit.Kelvin => Value - 273.15m,
			_ => 0 // 2. Setting a default value
		}; // 1. No handling for other cases, throws an exception at runtime
	
	}
}

```

### Structs

A structure type (or struct) is a value type that encapsulates data and functionality. Similar syntax to a Class. The difference, however, is that Structs contain data, whereas a Class contains a reference to that data.

They are a performance optimisation; Classes live on the Heap and need to be garbage collected, Structs live on the Stack and use simpler memory management. They are used mostly in low-level systems, such as hardware programming.

Structs cannot inherit from other structs and cannot be used as a base class. They can, however, implement interfaces.

```csharp
var rectangle = new Rectangle();

public readonly struct Rectangle // readonly keyword makes it immutable
{
	public Rectangle(double width, double height)
	{
		Width = width;
		Height = height;
	}

	public double Width { get; set; }
	public double Height { get; set; }
}
```

### Passing Value-Type Parameters

Arguments are either passed by value (default) or by reference.

*Pass-by-value*: a copy of the variable will be passed to the method

*Pass-by-reference*: Access to the variable will be passed to the method

When we pass a value type by value, changes made within the method are not visible to the caller. This is true for struct, int, char, bool, or any other value type.

```csharp
var rectangle = new Rectangle(200, 300);
Console.WriteLine($"Height is {rectangle.Height}");

MethodParameters.ChangeHeight(ref rectangle); // adding ref here
Console.WriteLine($"Height is {rectangle.Height}"); // without ref, value is still 300

public struct Rectangle
{ 
	// Rectangle implementation
}

public class MethodParameters
{
	public static void ChangeHeight(ref Rectangle rectangle) // add ref here
	{
		rectangle.Height = 500;
		Console.WriteLine($"Height in Method is {rectangle.Height}");
	}
}

```

When you add the `ref` keyword in front of the method parameter, the compiler will force you to add it again to the method argument. This allows you to pass the value by reference now. Any changes made within the method now affect the value outside of it.

### Passing Reference-Type Parameters

Recall that Arguments are either passed by value (default) or by reference. Reference types include Classes, Interfaces, Delegates, Lists, Arrays, and Dictionaries.

In C#, the default is **pass-by-value**, which means that when we pass an instance of a **class** to a method, the method receives a **copy** of the **reference**. When we pass a reference type by value, changes made within the method are visible to the caller because we use the **same reference** inside and outside the method.


```csharp
var person = new Person("Devin McDaniel");
Console.WriteLine($"Name: {person.Name}");

MethodParameters.ChangeName(person); //person is a class
Console.WriteLine($"Name: {person.Name}"); //will be "unknown", by default. with the ref keyword, the value will be "John Wayne"

public class Person
{
	// Implement Person class
}

public class MethodParameters
{
	public static void ChangeName(ref Person person) //ref allows reassigning the variable to another object
	{
		person.Name = "Unknown";
		person = new Person("John Wayne"); // allowed when passing by ref
	}
}
```

> The default behaviours of passing value and reference types are likely preferred.

### Exception Handling

An exception is an event that happens during the execution of a .NET application in an exceptional case. It means that the program cannot continue. Exception Handling allows .NET developers to transfer control from one place (where the error occurs) to another (where the error is handled).

```csharp
// The syntax
try
{
	// potentially exception-throwing code
}
catch (Exception exception)
{
	// handling the exception
}
finally
{
	// running always after the try block
}
```

#### Example usage

```csharp
string content = "";
try
{
	content = File.ReadAllText("doc.txt");
	Console.WriteLine("The file has been read");
}
catch (FileNotFoundException exception)
{
	Console.WriteLine($"ERROR: The file '{exception.FileName}' could not be found);
}
finally
{
	Console.WriteLine($"The content length is: {content.Length}");
}
```

#### Exception Classes

Exception classes are all derived from the `System.Exception` class. You can use this type to catch exceptions, but it will not give much detail about that specific exception.

> Consider if an `if/else` statement would be better handler than using Exception Handling. For example, if looking for a file that does not exist, consider if the program flow allows for creating the file in an `else` block.


## Arrays and Collection Types

Arrays and collections are two different ways to handle grouping, ordering, storing, and accessing objects.

*Arrays* are most useful when you know how many objects you need to store
`int[] array1 = new int[7]`

*Collections* are more flexible in that they can grow and shrink in size dynamically. They can be generic or non-generic.

**Namespaces** 

| **System** | **System.Collections** | **System.Collections.Generics** |
| ---------- | ---------------------- | ------------------------------- |
| `Array`    | `ArrayList`            | `List<T>`                       |
|            | `Stack`                | `Dictionary<TKey, TValue>`      |
|            | `Queue`                | `Stack<T>`                      |
|            |                        | `Queue<T>`                      |
**Interfaces** (For this unit)

| `IEnumerbale`    | `ICollection`    | `IList`    |
| ---------------- | ---------------- | ---------- |
| `IEnumerable<T>` | `ICollection<T>` | `IList<T>` |
### Arrays

Arrays are *Array* types in the `System` namespace. The type of its elements must be declared. Bracket notation is used to access individual elements of the array. 

#### Value-type arrays

```csharp
//method one
int[] array1 = new int[4];

array1[0] = 1;
array1[1] = 2;

Console.WriteLine(array1[0]);
Console.WriteLine(array1[1]);

//method two
int[] array2 = new int[] {1, 2, 3, 4};

//method three (new keyword required)
var array3 = new int[] {1, 2, 3, 4};

//method four (modern)
int[] array4 = {1, 2, 3, 4};
```

>[!important] For uninitialised values, the default value for a a value type is `0` and for a reference type is `null`

#### Reference-type arrays

```csharp
//Arrays of reference types
Person[] persons = new Person[2];
persons[0] = new Person("John");
persons[1] = new Person("Mary");

//or
Person[] morePeople = {new Person("John"), new Person("Jane")};

//or
Person[] simplePeople = [new("John"),new("Jane")];
```

#### Array iteration

`forEach` allows you to iterate through the array without declaring an index

```csharp
foreach (Person person in persons)
{
	Console.WriteLine(person.Name);
}
```

>[!warning] Arrays are best used when the number of elements is known. When an array is modified, a new array is created. (Immutability)


### ArrayList

`ArrayList` is a non-generic collection of objects. Its size dynamically grows and shrinks when needed. We cannot specify the type of the objects.

>[!warning] You cannot access properties of an ArrayList item without casting it first. This creates unneccesary code  and should be avoided outside of use in legacy projects.

### Generic List `List<T>`

The generic List `List<T>` is a strongly typed collection, with items that can be accessed using an index. It works like an ArrayList, but with added type safety.

```csharp
var numbers = new List<int>();
var day = 22;
numbers.Add(day);

foreach (var number in numbers)
{
	Console.WriteLine($"Number: {number}");
}

var persons = new List<Person>();
var person1 = new Person("Andrew");
persons.Add(person1);

foreach (var person in persons)
{
	Console.Writeline($"Person One: {person1.Name}");
}
```

The generic List implements the generic `IEnumerable<T>`,  generic `ICollection<T>`, and generic `IList<T>` interfaces.

**Implemented Interfaces**

|         | `IEnumberable<T>` | `ICollection<T>`                          | `IList<T>`                        |     |
| ------- | ----------------- | ----------------------------------------- | --------------------------------- | --- |
| Methods | `GetEnumerator()` | `int Count { get; }`                      | `T this[int index] { get; set; }` |     |
|         |                   | `bool IsReadOnly { get }`                 | `int IndexOf(T item);`            |     |
|         |                   | `void Add(T item);`                       | `void Insert(int index, T item);` |     |
|         |                   | `void Clear();`                           | `void RemoveAt(int index);`       |     |
|         |                   | `bool Contains(T item);`                  |                                   |     |
|         |                   | `void CopyTo(T[] array, int arrayIndex);` |                                   |     |
|         |                   | `bool Remove(T item);`                    |                                   |     |

### Generic Stack `Stack<T>`


## References / Sources

[Outgoing link]('https://google.com)
[Outgoing link]('https://google.com)
[Outgoing link]('https://google.com)

