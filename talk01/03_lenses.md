# Lenses

Lenses are a pattern in functional programming to "see" the "world". Lenses can show you the world as it is, you can
focus on whatever you want to see, and you can manipulate everything.

Lenses have 3 methods: `view`, `over` and `set`.

```js
const user = {
  name: "gal",
  nickname: "schniz"
};

const { lensProp, view, over, set } = require("ramda");
const $name = lensProp("name");

const userName = view($name, user);
console.log(userName);
```

You can say that it isn't impressive. It's just like using `user.name`. But lenses give more than just that. They're
composable.

```js
const user = {
  name: "gal",
  nickname: "schniz",
  hobby: {
    name: "talking"
  }
};

const { lensProp, view, over, set, compose } = require("ramda");
const $name = lensProp("name");
const $hobby = lensProp("hobby");

const hobbyName = view(compose($hobby, $name), user);
console.log(hobbyName);
```

Still not impressive? yes, still like `user.hobby.name`. Let's see the most powerful thing about lenses.

```js
const { lensProp, view, over, set, compose } = require("ramda");
const $name = lensProp("name");
const $hobby = lensProp("hobby");

const user = {
  name: "gal",
  nickname: "schniz",
  hobby: {
    name: "talking",
    lovedSince: "forever"
  }
};

const userHagever = set($name, "hagever", user);
const userDifferentHobby = set(compose($hobby, $name), "javascripting", user);
console.log({ user, userHagever, userDifferentHobby });

// in plain javascript, using shallow copying, it would be like

const userDifferentHobbyJS = Object.assign({}, user, {
  hobby: Object.assign({}, user.hobby, {
    name: "javascripting"
  })
});

console.log({ userDifferentHobbyJS });
```

Which one is better?

The last function I need to show you is `over`. Well, `over` is like `set`, but more flexible. You can implement `set` with `over`.
`over` takes a function (instead of a new plain value) to apply on the old value - it is something between `view` and `set`.

```js
const { lensProp, view, over, set, compose } = require("ramda");
const $nickname = lensProp("name");

const user = {
  name: "gal",
  nickname: "schniz",
};

const addHandleIfMissing = nickname => nickname.charAt(0) == '@' ? nickname : `@${nickname}`
const userWithHandle = over($nickname, addHandleIfMissing, user)
console.log({ user, userWithHandle });

// implementing set is easy -

const setWithOver = (lens, value, obj) => over(lens, () => value, obj)
const userWithNewNick = setWithOver($nickname, 'new nick', user)
console.log({ user, userWithNewNick })
```
