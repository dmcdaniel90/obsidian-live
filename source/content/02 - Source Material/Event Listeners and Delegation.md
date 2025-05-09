---
tags: []
---

**Date created**: 2025-04-13
**Tags**: 

## Summary

The `EventTarget.addEventListener` method listens for events on an element. You can pass the `event` object (or however you want to name it `e`) as an argument to the callback function in the second argument of the parent function. The `event.target` property shows the clicked element.

It should only be attached to an individual element and not iterables, unless using a specialised library. A common, but very non-performant, solution is to add an event listener on each iteration.

*Event Delegation* specifies adding the event listener to the parent element. *Event bubbling* references the action of an element registering a click and reporting that event to the nearest parent event listener 

Certain events, like `focus`, don’t bubble. To use event delegation with events that don’t bubble, you can set an optional third argument on the `EventTarget.addEventListener()` method, called `useCapture`, to `true`.

If you need to run the same callback on different events, create a named function and pass it (without invoking `()`) as the second argument to all the required event listeners.

[[The Var Keyword]]
[[The Var Keyword]]
[[The Var Keyword]]


## References / Sources

[List of available events - MDN](https://developer.mozilla.org/en-US/docs/Web/Events)

