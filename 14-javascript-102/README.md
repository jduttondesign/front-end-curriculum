# JavaScript 102

## Variable names

> **Reminder:** You can name variables whatever you like and it has **no impact** on what is actually stored in that variable. Naming a variable that will hold an array of widgets `x` makes it seem much more like a variable, but naming it `widgetArray` is more helpful. But it doesn't mean that it can only hold arrays. It is just a label.

## Basic array methods

### join

This combines all elements in an array into a single string, delimited by the character that you specify.

```js
var fruit = ["cherries", "apples", "bananas"];
var fruitString = fruit.join(","); // "cherries,apples,bananas"
fruitString = fruit.join(" "); // "cherries apples bananas"
fruitString = fruit.join("><");
```

### String.split()

This is the reverse of the `join()` method. It take a string and converts it into an array. You pass in the character that is the delimiter of each item in the string.

```js
var fruits = "watermelon|lemon|orange";
var fruitArray = fruits.split("|");
```

### reverse

Pretty simple, it reverse the items in an array

```js
var fruit = ["cherries", "apples", "bananas"];
fruit.reverse(); // ["bananas", "apples", "cherries"]
```

### sort

Pretty simple, it sorts the items in an array

```js
var fruit = ["cherries", "apples", "bananas"];
fruit.sort(); // ["apples", "bananas", "cherries"]
```

The tricky thing about sort is that it doesn't work very well with numbers. To sort numbers, you have to pass a custom function to the sort method. The default sort logic simply looks at the first character of each item and compares the ASCII value of that character.

```js
var numbers = [8, 1, 42, 13, 22, 7, 4, 53];
numbers.sort(); // [1, 13, 22, 4, 42, 53, 7, 8]
numbers.sort(function(first, second) { return first - second; }) // [1, 4, 7, 8, 13, 22, 42, 53]
```

### slice

The slice() method returns a shallow copy of a portion of an array into a new array object.

```js
var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
var citrus = fruits.slice(1, 3); // ["Orange", "Lemon"]
```

### splice

The splice() method, unlike slice(), does not create a new array, but rather modifies the existing array. You can use it to remove items, or add new ones at any location.

```js
// Remove the item at position 2
var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
fruits.splice(2, 1);

// Replace Orange with Tangerine
var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
fruits.splice(1, 1, "Tangerine");

// Add new item at index 3
var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
fruits.splice(3, 0, "Date");
```

### indexOf

This method find the index of the specified value in an array. If it's not found, it returns -1.

```js
var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
fruits.indexOf('Lemon'); // 2
```

## Chaining methods

If you want to perform multiple operations on an array, you can execute several statements. For example, if you want sort the fruits in descending alphabetical order, and then insert a new item, you could write this code.

```js
var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
fruits.sort();                  // Sort array items
fruits.reverse();               // Reverse the items
fruits.splice(4, 0, "Apricot"); // Add item
```

You can also chain all three operations together into one JavaScript statement.

```js
var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
fruits.sort().reverse().splice(4, 0, "Apricot");
```

> **Instructor suggestion**:
>
> Have students do the [array methods exercise](exercises/BASICARRAYMETHODS.md).

## Advanced array methods

The `forEach` method on an array executed a callback function for each element in the array.

```js
function outputFruit(element, index, array) {
  console.log('array[' + index + '] = ' + element);
}

var fruits = ["apple", "banana", "cherry"];
fruits.forEach(outputFruit);
```

The `map()` method creates a new array with the results of calling a provided function on every element in this array.

```js
function reverseIt(element, index, array) {
  return element.split("").reverse().join("");
}

var fruits = ["apple", "banana", "cherry"];
var backwardFruits = fruits.map(reverseIt);
console.log(backwardFruits); // ["elppa", "ananab", "yrrehc"]
```

The `filter()` method creates a new array with all elements that pass the test implemented by the provided function.

```js
function filterIt(element, index, array) {
  if (element.length === 5) {
    return element;
  }
}

var fruits = ["apple", "banana", "cherry"];
var filteredFruits = fruits.filter(filterIt);
console.log(filteredFruits); // ["apple"]
```

The `reduce()` method applies a function against an accumulator and each value of the array (from left-to-right) to reduce it to a single value.

```js
var sum = [0, 1, 2, 3, 4].reduce(function(previousValue, currentValue, index, array) {
  console.log("curent index: " + index);
  return previousValue + currentValue;
});
console.log(sum);
```

> **Instructor suggestion**:
>
> Have students do the [advanced array methods exercise](exercises/ARRAYMETHODS.md).


## Objects

The most basic object is a collection of key:value pairs surrounded by curly braces.

```js
var myCar = {
  make: "Nissan",
  model: "Xterra",
  year: 2006,
  color: blue
}
```

You can add new key:value pairs after the initial definition.

```js
myCar.doors = 4;
myCar.sunroof = false;
```

You can then access the value of any of those keys.

```js
console.log("My car has " + myCar.doors + " doors.");
```

## Functions

##### Simple function

Go over the basics of functions and live code some examples.

```js
function sayHello() {
  document.write("Hello, world");
}

// Only when you write the name of the function with parenthesis, does it get executed.
sayHello();
```

##### Function with arguments

```
function saySomething(message) {
  document.write(message);
}

saySomething("Hello");
saySomething("World");
```


> **Instructor suggestion**:
>
> After live coding and student questions, have students do the [coins exercise](COINS.md) which combines working with an object and a function.


### Functions with/without return values

```js
function reverseIt(originalString) {

  // Convert string to array, reverse the elements, and join back together
  var reversedString = originalString.split("").reverse().join("");
  
  // Return the new string
  return reversedString;
}

var result = reverseIt("flambajamba");
console.log(result);
```

### Functions are first-order objects

Can be passed as arguments to other functions.

```js
function performOperationOnString(originalString, functionToExecute) {
  var finalValue = functionToExecute(originalString);

  return finalValue;
}

function alphabetical(originalString) {
  var alphabeticalOrder = originalString.split("").sort().join("");
  
  return alphabeticalOrder;
}

var result = performOperationOnString("The lazy brown dog", alphabetical);
console.log(result);
```

> **Instructor suggestion**:
>
> After live coding and student questions, have students do the [coins exercise](COINS.md). If you feel they are ready after that, throw the pine tree problem at them.

