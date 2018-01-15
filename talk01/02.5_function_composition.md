# Function composition

I am going to talk a lot about the `compose` function. It is basically function composition:

```
  +-------------> f o g ------------+
  |                                 |
  |                                 v
+-+-+         +------+         +---------+
| x | -> g -> | g(x) | -> f -> | f(g(x)) |
+---+         +------+         +---------+
```

```js
const upcase = x => x.toUpperCase();
const excl = x => `${x}!`;
const shout = x => excl(upcase(x));

console.log(shout("gal is awesome"));
```

The more functions we compose, the ugly it looks. Let's make it better.

```js
const upcase = x => x.toUpperCase();
const excl = x => `${x}!`;

const compose = (f, g) => x => f(g(x));

const shout = compose(upcase, excl); // x => upcase(excl(x))
console.log(shout("gal is more than awesome"));
```

What just happened?

```js
//                                 ("gal")
const shout = compose(upcase, excl);
//                           ("gal")
const shout = compose(upcase, excl);
//                   ("gal!")
const shout = compose(upcase, excl);
//               ("GAL!")
const shout = compose(upcase, excl);
```

GREAET ANIMATION! And if we'd like to implement `compose` for more than just 2 functions (`sanctuary` doesn't support
it, but `ramda` does)

```js
const upcase = x => x.toUpperCase();
const excl = x => `${x}!`;
const addIrcChatBubble = name => text => `<${name}> ${text}`;

const compose = (...fns) => x => fns.reduceRight((acc, currFn) => currFn(acc), x);

const firstExample = addIrcChatBubble("gal")(upcase(excl("hello everyone")));
const secondExample = compose(addIrcChatBubble("gal"), upcase, excl)("hello everyone"); // extract shout!

console.log({ firstExample, secondExample });
```
