---
tags:
  - c-sharp
  - c-sharp/classes
---

**Date created**: 2025-04-23
**Tags**: [[c-sharp]], [[c-sharp#classes]]

## Old version

In Java and older versions of C#, you define a class in order of:
1. Members
2. Constructor (aka *secondary constructor*)
3. Methods

   ```csharp
   // C# Example (Older Style)
   public class Person
   {
       private string _name;
       private int _age;

       public Person(string name, int age)
       {
           _name = name;
           _age = age;
       }

       public string Name { get { return _name; } }
       public int Age { get { return _age; } }
   }
   ```

## New version

In the modern version, members are set in the *primary constructor* parameters. It is more concise, readable, and encourages immutability. The syntax is similar to functional programming in JavaScript.

```csharp
// C# Primary Constructor (Concise)
public class Person(string name, int age) // Primary Constructor Parameters
{
	public string Name { get; } = name;
    public int Age { get; } = age;

    // You can still have additional methods and properties here
}
```


```javascript
// Using destructuring and default parameters to achieve a similar effect in Javascript
   
function createPerson({ name = "Unknown", age = 0 } = {}) {
	return { name, age };
}

const person1 = createPerson({ name: "Bob", age: 25 });
const person2 = createPerson(); // Uses defaults
```

## Connected Ideas

[Similar or Opposing Idea](https://google.com)

## References / Sources

[MS Documentation - Primary Constructors](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-12.0/primary-constructors)
[Jeremy Bites - Thoughts on C# Primary Constructors](https://jeremybytes.blogspot.com/2024/04/thoughts-on-primary-constructors-in-c.html)
[C# 12: Primary Constructors](https://endjin.com/blog/2024/10/csharp-12-primary-constructors)

