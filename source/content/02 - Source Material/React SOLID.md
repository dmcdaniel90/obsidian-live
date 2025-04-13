---
tags:
  - react/general
---

## Overview

_Principle 1_: S - Single Responsibility
_Principle 2_: O - Open/Closed Principle
_Principle 3_: L - Liskov Substitution
_Principle 4_: I - Interface Segregation
_Principle 5_: D - Dependency Inversion

## Single Responsibility

A function should only have a single, clear responsibility instead of attempting multiple different operations. In React, large components can be reduced to smaller, more efficient ones by abstracting repetitive or expensive functions within the component into custom hooks such as a useFetch or useDebounce effect. It is best to refactor into hooks early to prevent extra work in the future ([[DRY Principle]]).

[[Pasted image 20250412195233.png | Example of Single Responsibility in React]]
[[Atomic Design]]
## Open/Closed Principle




https://www.linkedin.com/posts/fabriciodorneles_solidprinciples-openclosed-reactjs-activity-7315483291602567170-_66s?utm_source=share&utm_medium=member_ios&rcm=ACoAAAT2gTQBEqS-NYv_DuFuYP5brBUtKhR7jTY