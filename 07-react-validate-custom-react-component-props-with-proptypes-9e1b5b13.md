# 07. Validate Custom React Component Props with PropTypes

#### [📹 Video](https://egghead.io/lessons/react-v2-07-validate-custom-react-component-props-with-proptypes?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/07-prop-types?from-embed)

## Notes

- When you create reusable React components, you want to make sure that people use them correctly. The best way to do this is to use TypeScript in your codebase to give you compile-time checking of your code.
- If you’re not using TypeScript, you can still use PropTypes to get runtime validation.

- **Using PropTypes**:

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">

    function SayHello({ firstName, lastName }) {
       return (
         <div>
           Hello {firstName} {lastName}!
         </div>
       );
     }

     const PropTypes = {
       string(props, propName, componentName) {
         if (typeof props[propName] !== 'string') {
           return new Error(
             `Hey, the component ${componentName} needs the prop ${propName} to be a string`
           );
         }
       }
     };

     SayHello.propTypes = {
         firstName: PropTypes.string.isRequired
         lastName: PropTypes.string
     }

     const element = <SayHello firstName={false}>

     ReactDOM.render(element, document.getElementById('root'));
  </script>
</body>
```

- Using **`prop-types`** from unpkg:

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.production.min.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script src="https://unpkg.com/prop-types@15.6.1/prop-types.js"></script>
  <script type="text/babel">
    const rootElement = document.getElementById('root');

    function SayHello({ firstName, lastName }) {
      return (
        <div>
          Hello {firstName} {lastName}!
        </div>
      );
    }

    // prop-types creates a global variable called propTypes
    // passing .isRequired
    SayHello.propTypes = {
      firstName: PropTypes.string.isRequired,
      lastName: PropTypes.string.isRequired
    };

    const element = <SayHello firstName={false} />;

    ReactDOM.render(element, rootElement);
  </script>
</body>
```

- PropTypes are not rendered on production. You can also remove PropTypes using the [babel-plugin-transform-react-remove-prop-types](https://www.npmjs.com/package/babel-plugin-transform-react-remove-prop-types).

## Additional resource

- [npm - prop-types](https://www.npmjs.com/package/prop-types])
- [React Docs - Typechecking With PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html)
