# JavaScript Arrays  
Arrays in JavaScript are versatile data structures that can hold multiple values. Each value is referred to as an element, and elements are accessed by their index.  
## Creating an Array  
Arrays in JavaScript can be created using array literals or the `Array()` constructor.  
### Using Array Literals  
```js
javascript const fruits = ['apple', 'banana', 'cherry'];
```

### Using Array Constructor

```js
const fruits = new Array('apple', 'banana', 'cherry');
```

## Accessing Elements

Array elements can be accessed using their index. JavaScript uses zero-based indexing.

```js
const fruits = ['apple', 'banana', 'cherry'];  
console.log(fruits[0]); // Output: 'apple' 
console.log(fruits[1]); // Output: 'banana'
```

## Modifying Elements

You can modify array elements by assigning a new value to a specific index.

```js
const fruits = ['apple', 'banana', 'cherry'];  
fruits[1] = 'orange'; 
console.log(fruits); // Output: ['apple', 'orange', 'cherry']
```

## Array Properties and Methods

JavaScript provides several properties and methods to work with arrays:

### Properties

- **`length`**: Returns the number of elements in the array.

```js
const fruits = ['apple', 'banana', 'cherry']; 
console.log(fruits.length); // Output: 3
```

### Methods

- **`push()`**: Adds one or more elements to the end of the array and returns the new length.

```js
const fruits = ['apple', 'banana']; 
fruits.push('cherry'); 
console.log(fruits); // Output: ['apple', 'banana', 'cherry']
```

- **`pop()`**: Removes the last element from the array and returns that element.

```js
const fruits = ['apple', 'banana', 'cherry']; 
const lastFruit = fruits.pop(); 
console.log(lastFruit); // Output: 'cherry' 
console.log(fruits); // Output: ['apple', 'banana']
```

- **`shift()`**: Removes the first element from the array and returns that element.

```js
const fruits = ['apple', 'banana', 'cherry']; 
const firstFruit = fruits.shift(); 
console.log(firstFruit); // Output: 'apple' 
console.log(fruits); // Output: ['banana', 'cherry']
```

- **`unshift()`**: Adds one or more elements to the beginning of the array and returns the new length.

```js
const fruits = ['banana', 'cherry']; 
fruits.unshift('apple'); 
console.log(fruits); // Output: ['apple', 'banana', 'cherry']
```

## Custom Array Function

You can also define custom functions to work with arrays. For example, here's a function `array_diff` that computes the difference between two arrays:

```js
function array_diff(a, b) {   
	return a.filter(e => !b.includes(e)); 
}  

const arr1 = [1, 2, 3, 4]; 
const arr2 = [2, 4];  
const diff = array_diff(arr1, arr2); 
console.log(diff); // Output: [1, 3]
```

And here's a function `array_intersection` that computes the similarity or intersection between two arrays:


```js
function array_intersection(a, b) {   
	return a.filter(e => b.includes(e)); 
}  

const arr1 = [1, 2, 3, 4]; 
const arr2 = [2, 4, 5];  
const intersection = array_intersection(arr1, arr2); 
console.log(intersection); // Output: [2, 4]
```
## Conclusion

JavaScript arrays are fundamental data structures that allow you to store and manipulate collections of elements. Understanding how to create, access, modify, and utilize array properties and methods is essential for effective programming in JavaScript.

This markdown provides an overview of creating arrays, accessing and modifying elements, and using properties and methods available in JavaScript arrays. Feel free to modify and expand upon it as needed.