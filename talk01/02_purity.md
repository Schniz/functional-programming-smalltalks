When we talk about "function purity", it means one thing and one thing only: Every time that we call the function with
the same arguments, the same result comes out. That means - no side effects. No DB calls, no exceptions, no mutations of
any kind outside the function scope.

```js
const pure = x => x + 1;
const pure = x => Promise.resolve(x);
const impure = x => db.getValueFor(x);

const pure = xs => xs.map(x => x + 1);
const pure = xs => {
  const result = [];
  xs.forEach(x => result.push(x + 1));
  return results; // mutation but inside this scope
};
const impure = xs =>
  xs.forEach(x => {
    x.y += "hey"; // mutation!
  });
```

Think about `React.Component#render`. You can't make HTTP calls there, you can't do anything but to provide the
components based on `this.state` and `this.props`. This is the restriction React's API have to maintain your DOM tree.
Mutations are fine! _React itself does mutations and side effects_, but these should be VERY managed and well tested.

This is why I love 2 ways of making HTTP calls in React - HoCs and Render props:

```js
const ComponentWithData = withFetch("https://app.keywee.co/...", MyComponent);

// or
function render() {
  return (
    <Fetch url={url} onLoading={() => "Loading"} onError={(error, retry) => "Error!"}>
      {value => JSON.stringify(value)}
    </Fetch>
  );
}
```

But this is for another talk.
