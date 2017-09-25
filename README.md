---
title: Iterators and Control Flow
type: lesson
duration: "2:35"
creator:
    name: Vince Abruzzo
    modified by: Ari Brenner, J Silverstein
    city: NY
competencies: Programming
---

# Iterators and Control Flow

### Objectives
*After this lesson, students will be able to:*
- Implement `if/else` and `switch` statements and contrast use-cases
- Implement `while`-loops and understand how to break
- Identify the 4 components of a `for`-loop and their execution order
- Compare the use-cases of `for` and `while`-loops

### Preparation
*Before this lesson, students should already be able to:*
- Be comfortable with arrays and indexing
- Be comfortable with objects and getting values
- Understand the concepts of truthy/falsy

## Conditional Statements

### if...else statement

If statements are an extremely common way to manage application logic -- what happens when, etc.

![flowchart](./assets/if-else-flowchart.jpg)

```js
if (/* whatever's in here is true */) {
  // this code runs
}
```

... means run the `code` block if `expr` is truthy

```javascript
if (true) { 
  console.log('Hello')
}

if (1 > 0) {
  console.log('World')
}
//=> Hello
//=> World
```

When you need to test more than one case, you may use `else if`:

```javascript
var favoritePet = 'dog';

if (favoritePet === 'cat') {
  console.log('Achoo!!! Im allergic to cats.');
} else if (favoritePet === 'dog') {
  console.log('Yeah!! Dogs are the best.');
} else {
  console.log(`Please don't tell me you own a ferret`);
}

//=> Yeah!! Dogs are the best.
```

#### You Do
Let's see if you have enough money to buy a cat.

If `yourMoney` is equal to `price`, log the message "You have just enough to buy a cat!"
If `yourMoney` is more than `price`, log the message "You can buy a cat and will have <X> dollars left over"
If `yourMoney` is less than `price`, log the message "You cannot buy a cat.  You need <X> more dollars :("

```javascript
  var yourMoney = 50;
  var catPrice = 100;

  // YOUR CODE HERE
```
Play with the numbers above to make sure your code works!



### Ternary Operator

JavaScript has a ternary operator for conditional expressions. You can think about the ternary operator as a concise "if-else in one line":

`(condition) ? ifTrue : ifFalse`

```javascript
var age = 12;

var allowed = (age > 18) ? 'yes' : 'no';

allowed;
//=> "no"
```

## Switch Statement

The switch statement can be used for multiple branches based on `===` equality:

```javascript
var food = 'apple';

switch(food) {
  case 'pear':
    console.log('I like pears');
    break;
  case 'apple':
    console.log('I like apples');
    break;
  case 'orange':
  case 'clem':
    console.log('mmm... citrus');
    break;
  default:
    console.log('idk what that is');
}
//=> I like apples
```

In this case the `switch` statement compares `food` to each of the cases (`pear` and `apple`), and evaluates the expressions beneath them if there is a match. (Using `===` to evaluate equality)

The default clause is optional.

#### You Do

Use a `switch` statement to inform us if some number `n` is prime.
* If it's 1, log the message '1 is actually not prime!'
* If it's 2, log the message '2 is the smallest prime!'
* If it's 3, 5, or 7, log the message: '`n` is prime!'
* If it's 4, 6, 8, or 9, log the message: '`n` is not prime :('
* Otherwise, log the message "idk if `n` is prime. google it, ask yourself, ask your friend."

(of course you should interpolate `n` in your messages)

### Using objects for assignment

Let's assume we are given a Greek God's Greek name and we would like to determine the Roman name
```javascript
var greekName = 'zeus';

switch(greekName) {
  case 'hermes':
    var romanName = 'mercury';
    break;
  case 'aphrodite':
    var romanName = 'venus';
    break;
  case 'ares':
    var romanName = 'mars';
    break;
  case 'zeus':
    var romanName = 'jupiter';
    break;
  case 'cronos':
    var romanName = 'saturn';
    break;
  case 'poseidon':
    var romanName = 'neptune';
    break;
  case 'hades':
    var romanName = 'pluto';
    break;
}
```

This works but is a little verbose.  How can we accomplish the same thing with an object?

```javascript
var greekName = 'zeus';

var greekToRoman = {
  hermes: 'mercury',
  aphrodite: 'venus',
  ares: 'mars',
  zeus: 'jupiter',
  cronos: 'saturn',
  poseidon: 'neptune',
  hades: 'pluto'
};

var romanName = greekToRoman[greekName];
```

Sleek. Sexy. Concise.

## Iteration

### [`while`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/statements/while) loops

`while` is a loop statement that will run while a condition evaluates to truthy.
**WARNING** if your `while` loop never evaluates to falsy you may be stuck in an infinite loop!

```javascript
var animal;
var array = ['dog', 'cat', 'ferret', 'zebra'];

while (array.length > 0) {
  animal = array.pop();
  console.log(`I have a ${animal}`)
}
```

You can also `break` to exit the loop before the condition is met.

```javascript
var animal;
var array = ['dog', 'cat', 'ferret', 'zebra'];

while (array.length > 0) {
  animal = array.shift();
  console.log(`I have a ${animal}`);

  if(animal === 'ferret') {
    console.log('ew ferrets are gross');
    break;
  }
}
```

Similarly, we can use [`continue`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/continue) to "skip" the rest of the current iteration and move to the next.

### [`for`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/statements/for) loops

`for` loops contain 4 components:
* _initialization_ (e.g. `var i = 0;`)
* _test condition_ (e.g. `i < 10;`)
* _final expression_ or _incrementor_ (e.g. `i++`)
* _block_ (e.g. `console.log(i)`)

```javascript
// start at i = 0; continue while i < 10; add 1 to i after each iteration
for (var i = 0; i < 10; i++) {
  console.log(i);
  // do more stuff
}
```
What will we see when running the above snippet?
What is the final value of `i`?

You can think of the above as short-hand for
```javascript
var i = 0;
while(i < 10) {
  console.log(i);
  // do more stuff

  i++;
}
```

We can use `for` loops to iterate over an array

```javascript
var people = ['homer', 'marge', 'maggie', 'bart', 'lisa'];
var person;

for (var i = 0; i < people.length; i++) {
  person = people[i];
  console.log(`hello, ${person}!`);
}
```

We can implement something similar to a `for` loop with a `while` loop.

#### You Do

Let's expand our `switch` statement from above that checks for primes.  Instead of just seeing the output for one number, let's use a loop to get the output for every number from 1 to 12.



## Conclusion (5 mins)
- When would use conditionals? What are the different ways to tackle conditional logic?
- What can we use `for` and `while` loops to accomplish?
- How do we choose between using a `for` or a `while` loop?

**[Lab here](https://git.generalassemb.ly/wdi-nyc-delorean/LAB_U01_D04_Iterators-and-Control-Flow)**
