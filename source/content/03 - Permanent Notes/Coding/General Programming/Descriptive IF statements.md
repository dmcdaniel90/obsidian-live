---
tags:
  - programming/iteration
---

**Date created**: 2025-05-08
**Tags**: [[programming]], [[programming#iteration]]

## Use descriptive `if` statements

Use descriptive values as arguments in `if` statements to show intention.

```csharp
// works, but not the best method
if (age >= 18 && isCitizen && hasValid) 
{
	LogAccessGranted(user);
	UpdateAccessHistory(user);
}

// better

if (hasValidCredentials(age, isCitizen, hasValidId))
{
	//…same
}

```

## Connected Ideas

[Similar or Opposing Idea](https://google.com)

## References / Sources

[Outgoing link]('https://google.com)
[Outgoing link]('https://google.com)
[Outgoing link]('https://google.com)

