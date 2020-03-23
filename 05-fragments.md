# 05. Render two elements side-by-side with React Fragments

#### [📹 Video](https://egghead.io/lessons/react-v2-05-render-two-elements-side-by-side-with-react-fragments?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/05-fragements?from-embed)

## Notes

- In React, you can’t render two React elements side-by-side (`<span>Hello</span><span>World</span>`). They have to be wrapped in another element (like a `<div>`).
- This may seem like an odd limitation, but when you think about the fact that JSX is compiled to `React.createElement` calls, it makes sense.
- [React Fragments](https://reactjs.org/docs/fragments.html) let you group a list of children without adding extra nodes to the DOM.

- Using the **React Fragments API**:

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    const helloElement = React.createElement('span', null, 'Hello');
    const worldElement = React.createElement('span', null, 'World');
    // Using the React Fragments API:
    const element = React.createElement(
        React.Fragment,
        null,
        helloElement
        worldElement
    )
    ReactDOM.render(element, document.getElementById('root'));
  </script>
</body>
```

- You can also use a **React Fragments Element**:

```js
const element = (
  <React.Fragment>
    <span>Hello</span>
    <span>World</span>
  </React.Fragment>
);
```

- Since React Fragments is so common, JSX has a **special syntax** for it:

```js
const element = (
  // open and closing angle brackets
  <>
    <span>Hello</span>
    <span>World</span>
  </>
);
```

## Additional resource

- [React doc- Fragments](https://reactjs.org/docs/fragments.html)
