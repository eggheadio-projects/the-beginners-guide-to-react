# 04. Use JSX effectively with React

#### [📹 Video](https://egghead.io/lessons/react-v2-04-use-jsx-effectively-with-react?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/04-jsx-tricks?from-embed)

## Notes

- JSX is not an entirely different language, but it is a bit of an extension to the language, so knowing how you would express certain JavaScript things within the JSX syntax is important to using JSX effectively.

- To interpolation use `{ }`. Any JavaScript expression inside of the curly braces will be evaluated and passed to the `React.createElement` API. This allows you to be expressive when building out UI's. Example:

```html
<script type="text/babel">
  const rootElement = document.getElementById('root');
  // declaring variables
  const children = 'Hello World';
  const className = 'container';
  // interpolation
  const element = <div className={className}>{children}</div>;
  ReactDOM.render(element, rootElement);
</script>
```

Since this is JSX and not HTML, you can use self-closing tags:

```html
<script type="text/babel">
  const rootElement = document.getElementById('root');
  const children = 'Hello World';
  const className = 'container';
  const props = { children, className };
  // self-closing tags
  const element = <div {...props} />;
  ReactDOM.render(element, rootElement);
</script>
```

- The spread operator takes either an array or an object and expands it into its set of items. We can use the spread operator to pass down our props to the `React.createElement` API:

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    const rootElement = document.getElementById('root');
    const children = 'Hello World';
    const className = 'container';
    const props = { children, className };
    // using spread operator
    const element = <div {...props} />;
    ReactDOM.render(element, rootElement);
  </script>
</body>
```

- You can also add or extended props in a declarative and deterministic way.

## Additional resource

- [Understanding the Spread Operator in JavaScript](https://zendev.com/2018/05/09/understanding-spread-operator-in-javascript.html)
- [MDN Spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
