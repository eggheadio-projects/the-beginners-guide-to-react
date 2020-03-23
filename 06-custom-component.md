# 06. Create a Simple Reusable React Component

#### [📹 Video](https://egghead.io/lessons/react-v2-06-create-a-simple-reusable-react-component?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/06-custom-component?from-embed)

## Notes

- One of the biggest paradigm shifts that React offered to the UI ecosystem was the component model.
- Components let you split the UI into independent, reusable pieces, and think about each piece in isolation.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    // creating a function component, that accepts a props object and returns a React Element
    // it passes JSX attributes and children to this component as a single object “props”
    function Message({ children }) {
      return <div className="message">{children}</div>;
    }

    const element = (
      <div className="container">
        <Message>Hello World</Message>
        <Message>Goodbye World</Message>
      </div>
    );

    ReactDOM.render(element, document.getElementById('root'));
  </script>
</body>
```

- **Rendering** a Component:

```js
//  capitalized to ensure that babel passes the function rather than the string message
const element = (
  <div className="container">
    <Message>Hello World</Message>
    <Message>Goodbye World</Message>
  </div>
);
```

## Additional resource

- [React doc - Components and Props](https://reactjs.org/docs/components-and-props.html)
