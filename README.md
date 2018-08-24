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
*Before this lesson, students should already:*
- Understand the concepts of truthy/falsy

### Before we start!

You'll see `let` and `const` in here quite a bit instead of `var`. `let` and `const` also let you declare variables. For now, all you need to know is:

- You use `let` to declare a variable that you know you will reassign later.
- You use `const` to declare a variable that will never be re-assigned.

(They also have something to do with something called _scope_, which we'll get into in more detail when we talk about functions.)

When declaring a variable, you should default to `const`. If you realize later that you need to change it, it's easy to change it to `let`.

> Why would we prefer `let` to `const`?

# Conditional Statements

## if...else statement

If statements are an extremely common way to manage application logic -- what happens when, etc.

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

![flowchart](./assets/if-else-flowchart.jpg)

```javascript
const favoritePet = 'cat';

if (favoritePet === 'dog') {
  console.log('Achoo!!! Im allergic to dogs.');
} else if (favoritePet === 'cat') {
  console.log('Yeah!! Cats are the best.');
} else {
  console.log(`Please don't tell me you own a ferret`);
}

//=> Yeah!! Cats are the best.
```

When you're comparing variables to values, make sure you're using  `===` -- not `=`. If you use `=`, you're reassigning the variable, instead of checking it for equality.

### 🚀 Independent Practice!!

Touch a new javascript file -- `lecture-practice.js` -- and work in that. Remember, you can use Node to run the file: `node lecture-practice.js`.

Let's see if you have enough money to buy a cat.

If `yourMoney` is equal to `price`, log the message "You have just enough to buy a cat!"
If `yourMoney` is more than `price`, log the message "You can buy a cat and will have <X> dollars left over"
If `yourMoney` is less than `price`, log the message "You cannot buy a cat.  You need <X> more dollars :("

```javascript
// Put these lines into your `lecture-practice.js` file.

  const yourMoney = 50;
  const catPrice = 100;

  // YOUR CODE HERE
```
Play with the numbers above to make sure your code works!


### Ternary Operator

`(condition) ? ifTrue : ifFalse`

JavaScript has a ternary operator for conditional expressions. Where an `if ... else` **statement** conditionaly runs code, a ternary is used to make an **expression** which returns a value conditionally. Consider the difference when distinguishing between a statement and an expression:

```javascript
const age = 12

let allowed

if (age > 18) {
  allowed = 'yes'
} else {
  allowed = 'no'
}

console.log(allowed)
```

```javascript
const age = 12

const allowed = (age > 18) ? 'yes' : 'no'

console.log(allowed)
//=> "no"
```

## Switch Statement

The switch statement can be used for multiple branches based on `===` equality:

```javascript
const food = 'apple';

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

The default clause is technically optional but in most cases it is good practice to include one.

### 🚀 Independent Practice!!

Use a `switch` statement to inform us if some number `n` is prime.
- If it's 1, log the message '1 is actually not prime!'
- If it's 2, log the message '2 is the smallest prime!'
- If it's 3, 5, or 7, log the message: '`n` is prime!'
- If it's 4, 6, 8, or 9, log the message: '`n` is not prime :('
- Otherwise, log the message "idk if `n` is prime. google it, ask yourself, ask your friend."

(of course you should interpolate `n` in your messages)

# Iteration

### [`while`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/statements/while) loops

`while` is a loop statement that will run while a condition evaluates to truthy.
**WARNING** if your `while` loop never evaluates to falsy you may be stuck in an infinite loop!

```javascript
let n = 0
while (n < 50) {
  console.log(`${n} is ${n % 2 ? 'odd' : 'even'}`)
  n++
}
```

You can also `break` to exit the loop before the condition is met.

```javascript
let n = 0
while (n < 50) {
  console.log(`${n} is ${n % 2 ? 'odd' : 'even'}`)
  if (n === 42) {
    break
  }
  n++
}
```

Similarly, we can use [`continue`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/continue) to "skip" the rest of the current iteration and move to the next.

> How would we skip all values divisible by 7?

### [`for`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/statements/for) loops

`for` loops contain 4 components:
- _initialization_ (e.g. `let i = 0;`)
- _test condition_ (e.g. `i < 10;`)
- _final expression_ or _incrementor_ (e.g. `i++`)
- _block_ (e.g. `console.log(i)`)

Notice these components all exist in our `while` example above. A `for` loop is just a specialized while loop since the pattern is so common.

```javascript
// start at i = 0; continue while i < 10; add 1 to i after each iteration
for (let i = 0; i < 10; i++) {
  console.log(i);
  // do more stuff
}
```
What will we see when running the above snippet?
What is the final value of `i`?

```javascript
let i = 0;
while(i < 10) {
  console.log(i);
  // do more stuff

  i++;
}
```

We can implement something similar to a `for` loop with a `while` loop.

### 🚀 Independent Practice!!

Let's expand our `switch` statement from above that checks for primes.  Instead of just seeing the output for one number, let's use a loop to get the output for every number from 1 to 12.

## 🚀 LAB TIME!!

Working with a partner we will fork and clone [this repo](https://git.generalassemb.ly/wdi-nyc-arcadia/LAB_U01_D02_choose-your-own-adventure)!

## Conclusion (5 mins)
- When would use conditionals? What are the different ways to tackle conditional logic?
- What can we use `for` and `while` loops to accomplish?
- How do we choose between using a `for` or a `while` loop?
