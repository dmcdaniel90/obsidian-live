---
tags: []
---

**Date created**: 2025-04-13
**Tags**: 

## Why directly manipulating the DOM is against React principles

*   **Unidirectional Data Flow:** React emphasises a one-way data flow from the parent component to its children. Your components should be derived from the application's state and properties (props), not vice versa. Directly manipulating the DOM bypasses this flow. You're essentially allowing DOM elements to change directly, of which React is unaware.
  
*   **Declarative vs. Imperative:** React is declarative. You describe *what* the UI should look like based on the data, and React handles the *how* of updating the DOM to match that description. Manually using `document.getElementsByClassName` and modifying the DOM is imperative - you're directly instructing the browser to change the DOM. This makes the component harder to reason about.
  
*   **Virtual DOM and Reconciliation:** React uses a Virtual DOM to update the real DOM efficiently. It compares the Virtual DOM with the actual DOM, identifies the differences, and only updates the necessary parts. When you directly modify the DOM outside of React's awareness, the Virtual DOM becomes out of sync. This can lead to unexpected behaviour, performance issues, and React overwriting your manual changes.
  
*   **Component Reusability and Predictability:**  By relying on direct DOM manipulation, you couple your component tightly to the specific DOM structure. This makes the component less reusable and more prone to errors when the DOM structure changes. A React component should ideally be independent of the surrounding DOM structure.
  
*   **State Management Complexity:** If your component modifies the DOM directly and the DOM changes should influence the application state, you'll have to manually handle synchronization between the DOM and React's state. This adds complexity and is a common source of bugs.

## Alternatives that Adhere to React Principles:

Instead of directly accessing and modifying the DOM using `document.getElementsByClassName` and `Array.from`, here's how to achieve the same result in a way that's more React-friendly:

1.  **Controlled Components and State:**

    *   **Component-Driven Approach:** Let React control the rendering of the elements with the `some-element` class.
    *   **State Management:** If you need to track or modify the properties of these elements, store the necessary data in React's state.
    *   **Event Handlers:**  Use React's event handling system (e.g., `onClick`, `onChange`) to trigger state updates when user interactions occur on these elements.
    *   **Dynamic Rendering:**  Use conditional rendering and mapping to create or update the elements based on the state dynamically.

    **Example:**

    ```javascript
    import React, { useState, useEffect, useRef } from 'react';

    function MyComponent() {
        const [elements, setElements] = useState([]);
        const containerRef = useRef(null);

        useEffect(() => {
          // Simulate fetching data that describes the elements,
          // or generate them based on some logic.  This replaces the direct DOM query.
          const initialData = [
            { id: 1, text: "First Element", style: { color: "blue" } },
            { id: 2, text: "Second Element", style: { color: "red" } },
            { id: 3, text: "Third Element", style: { color: "green" } },
          ];
          setElements(initialData);

        }, []);


        const updateElementStyle = (id, newStyle) => {
          setElements(prevElements =>
            prevElements.map(element =>
              element.id === id ? { ...element, style: { ...element.style, ...newStyle } } : element
            )
          );
        };

        return (
            <div ref={containerRef}>
                {elements.map(element => (
                    <div
                        key={element.id}
                        className="some-element"
                        style={element.style}
                        onClick={() => updateElementStyle(element.id, { fontWeight: "bold" })} // Example: Update style on click
                    >
                        {element.text}
                    </div>
                ))}
            </div>
        );
    }

    export default MyComponent;
    ```

2.  **Ref to the Container (Less Recommended - Use with Caution):**

    *   If you absolutely need to access the DOM elements (e.g., for integrating with a third-party library that requires direct DOM manipulation), use `useRef` to get a reference to the container element.
    *   Use `useEffect` to run code *after* the component has rendered.  Within the `useEffect` hook, you can safely access the DOM elements within the container.
    >[!question] Could you use `useLayoutEffect`?
    
    *   Even when using refs, strive to keep the DOM manipulations minimal and focused on integration with external libraries.  Avoid using refs for core component logic.

    **Example:**

    ```javascript
    import React, { useEffect, useRef } from 'react';

    function MyComponent() {
        const containerRef = useRef(null);

        useEffect(() => {
            if (containerRef.current) {
                const elements = containerRef.current.getElementsByClassName('some-element');
                const elementArray = Array.from(elements);

                elementArray.forEach(element => {
                    // Example:  Modify the element's style (use sparingly!)
                    element.style.backgroundColor = 'lightgray';
                });
            }
        }, []); // Run only once after initial render

        return (
            <div ref={containerRef}>
                <div className="some-element">Element 1</div>
                <div className="some-element">Element 2</div>
                <div className="some-element">Element 3</div>
            </div>
        );
    }

    export default MyComponent;
    ```

**Explanation of the Ref-Based Example:**

1.  **`useRef(null)`:**  Creates a ref object that initially points to `null`.
2.  **`<div ref={containerRef}>`:** Attaches the ref to the container `div`.  After the component mounts, `containerRef.current` will hold a reference to this `div` element.
3.  **`useEffect`:**  The `useEffect` hook runs after the component is mounted. The empty dependency array `[]` ensures it only runs once.
4.  **`containerRef.current.getElementsByClassName('some-element')`:** Accesses the DOM node using the ref and then finds the elements with the class name.
5.  **`Array.from(elements)`:**  Converts the `HTMLCollection` returned by `getElementsByClassName` into a standard JavaScript array.
6.  **`element.style.backgroundColor = 'lightgray'`:**  The code iterates through the array and changes the `backgroundColor` of each element.

## Important Considerations:

*   **Performance:** Direct DOM manipulation can be less efficient than letting React handle updates, especially for complex UI changes.
*   **Unpredictability:**  Direct DOM manipulation can introduce side effects that are difficult to track and debug.
*   **Maintainability:**  Components that rely on direct DOM manipulation are harder to maintain and refactor.

[[Considerations when modifying the DOM directly in React?]]


## References / Sources



