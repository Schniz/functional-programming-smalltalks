Functions in JavaScript are declared this way:

```js
function fn(arg1, arg2, ...spread) {
  return value;
}
```

Functions can be stored in a variable/constant so they can also be declared this way:

```js
const fn = function(arg1, arg2, ...spread) {
  return value;
};
```

Or you can use arrow functions. This is nice and helps with JS context issues:

```js
const fn = (arg1, arg2, ...spread) => value;
```

Functions also have methods on them, because they're javascript objects!

```js
const fn = function(arg) {
  return [this, arg];
};
const fnBounded = fn.bind("a", "hey");
console.log(fnBounded());
```

We can even extend the functionalities by extending `Function.prototype` but we won't do it right now

Because all the above, functions can be arguments as well (callbacks)

```js
const apply = (fn, value) => fn(value);
const result = apply(x => x + 1, 2);
console.log({ result });

// You can pass functions without initiating them on the spot
const increment = x => x + 1;
const result2 = apply(increment, 2);
console.log({ result2 });
```

And you can even return a function from your function!

This is called "HoF" or "Higher order function":

> Higher order function: a function that receives or returns a function

```js
const map = fn => array => array.map(fn);
const incrementAll = map(x => x + 1);
const result = incrementAll([1, 2, 3]);
console.log(result);
```

The `map` method that recieves the function and then the data, is called _currying_ or _partial application_. It is also
called point-free, because after we make this function we can use `map` without using `.map`, and with the right
modifications it can work on _any_ type (`NodeList`!)

There are libraries to use currying without headaches, like `Ramda`. `Ramda`'s `curry` function gets one argument - a
function with some arity, and understands how many arguments left to provide to the given function on any invocation.

> ProTip: When using curried functions, we're most likely to take the data as the last argument.

```js
const { curry } = require("ramda");
const map = curry((fn, array) => array.map(fn));
const result1 = map(x => x + 1, [1, 2, 3]);
console.log({ result1 });

const incrementAll = map(x => x + 1);
const result2 = incrementAll([1, 2, 3]);
console.log({ result2 });
```

For React developers, partial applications and higher order functions should sound very odd. `Redux` is doing it too.
When using `redux`, you use the `connect` function, that has the signature `connect :: config -> Component ->
ConnectedComponent` - gets a config, then a React component, and provides you a new component that may or may not use
your original component.
