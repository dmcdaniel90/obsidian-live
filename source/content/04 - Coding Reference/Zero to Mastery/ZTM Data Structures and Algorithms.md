---
tags:
  - algorithms
  - data-structures
  - zerotomastery
---


## Table of Contents

>[!info] Click to jump to section

## Big O

>[!question] What is good code?
>Good code is code that is readable and scalable. Big O focuses on how code scales as it grows. It measures how well (efficient) code performs a set of instructions.

### Big O and Scalability

>[!code] Measuring code performance with performance.now()
>```js
>const nemo = ['nemo']
>const large = new Array(1000).fill('nemo')
>
>function findNemo(array) {
>	let t0 = performance.now();
>	for (let i = 0; i < array.length; i++) {
>		if (array[i] === 'nemo') {
>			console.log('Found NEMO!')
>		}
>	}
>	let t1 = performance.now();
>	console.log('Call to find Nemo took ' + (t1-t0) + 'ms')
>}

> Big O checks the algorithmic efficiency of a function, for example, by testing how much it slows down as the size of the input increases. 
> 
> For example, a simple for loop, as pictured above may have four elements to loop over. It takes one loop per element. Plotted on a graph, this results in a linear relationship.
>
> This is written in Big O as 0(n) --> Linear Time

>[!info] O(n) is the most common notation you will find. It has a fair performance compared to other notations.
