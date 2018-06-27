# JavaScript Arithmetic

## Problem Statement
Up until now, we've been introducing a lot of different variables and website
structural elements that you can use to add functionality to your website with
JavaScript. This lesson introduces a number of the common operators and objects
you'll use to perform arithmetic operations in JavaScript.

Open up your browser's JavaScript console and test out all of the examples in
this lesson. Remember that we can't redeclare variables previously declared with
`const` or `let`, so you may have to refresh the page (which wipes away all
declared variables) or simply choose different variable names than those in the
examples.

## Objectives
1. Recognize the limitations of math in JavaScript
2. Employ operators to perform arithmetic and assign values to variables
3. Explain `NaN`
4. Use built-in objects like `Math` and `Number` to accomplish complex tasks

## Recognize the Limitations of Math in JavaScript
Math is awesome!

![Nerds](https://user-images.githubusercontent.com/17556281/28834889-9f87695e-76b1-11e7-84ff-5ce5cdf5a94b.gif)

As we learned in the lesson on data types, JavaScript has only a single,
all-encompassing `number` type. While other languages might have distinct types
for integers, decimals, and the like, JavaScript represents everything as a
double-precision floating-point number, or _float_. This imposes some
interesting technical limitations on the precision of the arithmetic we can
perform with JavaScript. For example:
```js
0.1 * 0.1;
//=> 0.010000000000000002

0.1 + 0.1 + 0.1;
//=> 0.30000000000000004

1 - 0.9;
//=> 0.09999999999999998
```

You shouldn't waste too much time diving into why this happens, but it basically
boils down to the language once again trying to be too nice to its human
masters. Under the hood, JavaScript stores numbers in binary (base-2) format, as
a series of `1`s and `0`s, but it displays numbers in the more human-readable
decimal (base-10) format. The problem that the above code snippet highlights is
that it's really easy to represent something like `1/10` in decimal (`0.1`) but
impossible to do it in binary (`0.0001100110011...`). It's the exact same
problem that the decimal system has in trying to represent `1/3` as
`0.33333333333...`.

The only time you'd really have to worry about this is if you needed to
calculate something to a high degree of precision, like interest payments for a
bank. For most of our day-to-day arithmetic needs, JavaScript is more than
capable.

## Employ Operators to Perform Arithmetic and Assign Values to Variables
JavaScript employs a pretty standard arsenal of arithmetic operators.

#### `+`
We've already used the addition operator to concatenate strings, but it's also
used to add numbers together:
```js
40 + 2;
//=> 42
```

#### `-`
The subtraction operator returns the difference between two numbers:
```js
9001 - 9000;
//=> 1
```

#### `*`
The multiplication operator returns the product of two numbers:
```js
6 * 7;
//=> 42
```

#### `/`
The division operator returns the result of the left number divided by the right
number:
```js
9001 / 42;
//=> 214.3095238095238
```

#### `%`
The remainder operator returns the remainder when the left number is divided by
the right number:
```js
9001 % 42;
//=> 13
```

#### `**`
The exponentiation operator returns the left number raised to the power of the
right number:
```js
2 ** 8;
//=> 256
```

#### Order of operations
JavaScript evaluates compound arithmetic operations by following the familiar
order of operations that's taught in standard math classes. You can remember the
order by remembering the phrase "<u>P</u>lease <u>E</u>xcuse <u>M</u>y
<u>D</u>ear <u>A</u>unt <u>S</u>ally". Anything in parentheses has highest
priority; exponentiation is second; then multiplication, division; and, finally,
addition and subtraction.

`( )` :arrow_right: `**` :arrow_right: `*` `/` `%` :arrow_right: `+` `-`

```js
2 - 2 % 2 + 2 / 2 ** 2 * 2;
//=> 3

2 - 2 % (2 + 2) / 2 ** 2 * 2;
//=> 1
```

#### Incrementing and decrementing
JavaScript also has a pair of operators that we can use to increment and
decrement a numerical value stored in a variable.

#### `++`
The `++` operator increments the stored number by `1`. If the `++` operator
comes after the variable (e.g., `counter++`), the variable's value is _returned
first and then incremented_:
```js
let counter = 0;
//=> undefined

counter++;
//=> 0

counter;
//=> 1
```

If the `++` operator comes before the variable (e.g., `++counter`), the
variable's value is _incremented first and then returned_:
```js
let counter = 0;
//=> undefined

++counter;
//=> 1

counter;
//=> 1
```

In both cases, `counter` contains the value `1` after incrementing. The
difference is in whether we want the operation to return the original or
incremented value.

#### `--`
The `--` operator decrements the stored number by `1` and has the same pair of
prefix and postfix options as the `++` operator:
```js
let counter = 0;
//=> undefined

// Return the current value of 'counter' and then decrement by 1
counter--;
//=> 0

// Check the new value of 'counter'
counter;
//=> -1

// Decrement 'counter' and then return the new value
--counter;
//=> -2

// Check the new value of 'counter'
counter;
//=> -2
```

#### Assignment operators
JavaScript has a number of operators for assigning a value to a variable. We've
already used the most basic, `=`, but we can also couple it with an arithmetic
operator to perform an operation _and_ assign the value of the operation:
```js
let counter = 0;
//=> undefined

counter += 10;
//=> 10

counter -= 2;
//=> 8

counter *= 4;
//=> 32

counter /= 2;
//=> 16

counter %= 6;
//=> 4

counter **= 3;
//=> 64
```

## Explain `NaN`
JavaScript tries to return a value for every operation, but sometimes we'll ask
it to calculate the incalculable. For example, imagine that one of the lines of
code in our program increments the value of a `counter` by `1`. However,
something broke in a different part of the program, and `counter` is currently
`undefined`. When the JavaScript engine reaches the incrementing line, what
happens?
```js
counter++;
//=> NaN
```

The JavaScript engine can't add `1` to `undefined`, so it tells us the result is **Not a Number** — `NaN`. It's basically JavaScript doing this:
![math](https://user-images.githubusercontent.com/17556281/28842772-effa3478-76cc-11e7-9d07-0c9a19b9b81b.gif)

***Top Tip***: Much like `undefined`, you should never assign `NaN` as the value of a variable
 and instead let it be a signal that some weird maths are happening in your
 code.

## Use Built-in Objects Like `Math` and `Number` to Accomplish Complex Tasks
To satisfy most of our math needs, JavaScript provides several built-in objects
that we can reference anywhere in JavaScript code, including `Number` and
`Math`.

#### `Number`
The `Number` object comes with a collection of handy methods that we can use for
checking and converting numbers in JavaScript.

#### `Number.isInteger()`
Checks whether the provided argument is an integer:
```js
Number.isInteger(42);
//=> true

Number.isInteger(0.42);
//=> false
```

#### `Number.isFinite()`
Checks whether the provided argument is finite:
```js
Number.isFinite(9001);
//=> true

Number.isFinite(Infinity);
//=> false
```

#### `Number.isNaN()`
Checks whether the provided argument is `NaN`:
```js
Number.isNaN(10);
//=> false

Number.isNaN(undefined);
//=> false

Number.isNaN(NaN);
//=> true
```

### `Math`
The `Math` object contains some properties representing common mathematical
values, such as `Math.PI` and `Math.E`, as well as a number of methods for
performing useful calculations.

#### `Math.ceil()` / `Math.floor()` / `Math.round()`
JavaScript provides three methods for rounding numbers. `Math.ceil()` rounds the
number _up_, `Math.floor()` rounds the number _down_, and `Math.round()` rounds
the number either up or down, whichever is nearest:
```js
Math.ceil(0.5);
//=> 1

Math.floor(0.5);
//=> 0

Math.round(0.5);
//=> 1

Math.round(0.49);
//=> 0
```

#### `Math.max()` / `Math.min()`
These two methods accept a number of arguments and return the lowest and highest
constituent, respectively:
```js
Math.max(1, 2, 3, 4, 5);
//=> 5

Math.min(1, 2, 3, 4, 5);
//=> 1
```

#### `Math.random()`
This method generates a random number between `0` (inclusive) and `1`
(exclusive):
```js
Math.random();
//=> 0.4495507082209371
```

In combination with some simple arithmetic and one of the rounding methods, we
can generate random integers within a specific range. For example, to generate a
random integer between `1` and `10`:
```js
Math.floor(Math.random() * 10) + 1;
//=> 8

Math.floor(Math.random() * 10) + 1;
//=> 1

Math.floor(Math.random() * 10) + 1;
//=> 6
```

`Math.random()` returns a number between `0` and `0.999...`, which we multiply
by `10` to give us a number between `0` and `9.999...`. We then pass that number
to `Math.floor()`, which returns an integer between `0` and `9`. That's one less
than the desired range (`1` to `10`), so we add one at the end of the equation.
Try it out in the JS console!

## Conclusion
Arithmetic in JavaScript can be helpful in a variety of ways once you get
comfortable with using it. This lesson gives you an overview of some of the
methods that are built in to JavaScript, but remember to use Google to look
around for other methods that might be built in as well. Play around with the
different methods in console, and you'll be a pro in no time!

## Resources
- MDN
  + [Basic math in JavaScript](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Math)
  + [Arithmetic operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators)
  + [Operator precedence](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)
  + [Assignment operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment_Operators)
  + [`NaN`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NaN)
  + [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)
  + [`Math`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math)
- [2ality — How numbers are encoded in JavaScript](http://2ality.com/2012/04/number-encoding.html)