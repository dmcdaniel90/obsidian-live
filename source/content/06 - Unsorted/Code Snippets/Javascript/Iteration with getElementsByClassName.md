`.forEach()` doesn’t work with `getElementsByClassName()`. However this is easily remedied by using the `Array.from()` method. So an easy way to store elements by class name into an iterable array could be written like this:

```javascript
const myArray= Array.from(document.getElementsByClassName('some-element'))
```

>[!error] Avoid using `document.getElementsByClassName` and directly manipulating the DOM outside of React's controlled component lifecycle [[DOM Manipulation in React|generally breaks React principles]].


