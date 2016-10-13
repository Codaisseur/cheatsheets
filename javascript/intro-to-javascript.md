# Intro to JavaScript

## 1. Variables

JavaScript uses variables to store values, just like Ruby. JavaScript is an old
language however, and it has some quirks.

### Declaration

If you want to assign some value to a variable, you need to declare the variable
first. JavaScript needs you to tell that that word that is the name of your
variable is going to be a variable:

```js
var pet = "Hamster";
```

You can also declare a variable first, before assigning it a value:

```js
var pet;

pet = "Hamster";
```

Declare multiple variables at once:

```js
var pet, owner, shop;
```

### Undefined vs Undeclared

Variables that don't have a value return `undefined`:

```js
var pet;
pet;
//-> undefined
```

Variables that are not declared, raise an error:

```js
shop;
//-> Uncaught ReferenceError: shop is not defined(…)
```

### Mutable

Just like in Ruby, JS variables are `mutable` (you can give them an initial
value, and give them another value later).

```js
var pet = new Pet("Hamster");
pet.lives(3);
pet.dies();
pet = new Pet("Parrot");
```

### Naming Convention

In JavaScript code, we use `camelCase` for variable names:

```js
var linesOfCodeWritten = 10000;
var funWritingCode = 100 * linesOfCodeWritten;
```

While in Ruby we would use `snake_case`:

```ruby
lines_of_code_written = 10000;
```

## 2. Operators & Logic

In JavaScript, `if` statements need parentheses around the comparisons:

```js
if (energy === 0) {
  rest(energy);
} else {
  work(energy);
}
```

### Equality

Did you notice the triple equal sign in the code above?

```js
energy === 0
```

If you want to test for *equality*, use `===`, but if you don't care if energy
is `0` or `"0"`, you can use the double `==`, see:

```js
> 0 == "0"
true
> 0 === "0"
false
> 0 == "00"
true
> 0 !== "00"
true
> 0 != "00"
false
```

## 3. Loops

In Ruby there are many ways to create loops. In most languages, however, this
is not the case, and we can only use the standard loops: `for` and `while`.

### While Loop

```js
var energy = 100;

while (energy > 0) {
  workIt();
  energy--;
}
```

### For Loop

For loops look a bit weird with the declaration in the first statement:

```js
for (var energy = 0; energy < 100; energy++) {
  sleepItOff();
  energy++;
}
```

### Plus Plus?

Yeah, pretty neat huh?

```js
> var count = 0;
undefined
> count++;
0
> count++;
1
> count
2
```

What about minus minus?

```js
> var energy = 100;
undefined
> energy--;
100
> energy--;
99
> energy
98
```

### Return values

Compare these return values:

```js
> var energy = 100;
undefined
> energy--;
100
> energy;
99
```

```js
> var energy = 100;
undefined
> --energy;
99
> energy;
99
```

```js
> var energy = 0;
undefined
> energy++;
0
> energy;
1
```

```js
> var energy = 0;
undefined
> ++energy;
1
> energy;
1
```

## 4. Functions

Functions are blocks of code with a name. In Ruby we called them methods, in
JS we call them function:

```js
var bark = function() {
  console.log("Woof!");
}

bark();
```

### Arguments

Functions can take arguments:

```js
var multiply = function(a, b) {
  return a * b;
}

multiply(4, 3);
//-> 12
```

### Calling

A function needs to be called:

```js
var bark = function() {
  console.log("Woof!");
}

bark;
//-> [Function]

bark();
//-> "Woof!"
```

## 5. Objects

Plain old JavaScript uses Objects, instead of Classes, and they look like Ruby
hashes a lot:

```js
var person = {
  firstName: "Elon",
  lastName: "Musk",
  speak: function() {
    console.log("Seems like an opportune moment to bring up the Fermi Paradox…");
  }
}
```

### Dot Notation

To access stuff inside an Object, we can use the dot notation:

```js
> person.firstName;
"Elon"

> person.speak();
> "Seems like an opportune moment to bring up the Fermi Paradox…"
```

### Mutable

Objects are mutable. Which means you can change them after you created them. You
can change a value of a property:

```js
> person.firstName = "Mr.";
```

You can add properties later as well:

```js
> person.inventions = ["electric cars", "cheap space travel"];
```

This means you can initialize as an empty Object as well:

```js
var dog = {};

dog.bark = function () { alert("Woof!"); };
```

### Nesting

Objects can be nested:

```js
var person = {};
person.name = {
    first: "Bob",
    last: "Dylan"
};
person.name.first;
//-> "Bob"
```
