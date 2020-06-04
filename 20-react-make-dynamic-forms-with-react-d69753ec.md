# 20. Make Dynamic Forms with React

#### [📹 Video](https://egghead.io/lessons/react-v2-20-make-dynamic-forms-with-react?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/20-dynamic-forms?from-embed)

## Notes

- Often, it can be useful to know what the user’s input is as they’re typing it and use that information to change what is rendered. This can be **good for dynamic search** or filter inputs, or triggering changes when a user checks a checkbox, or a myriad of other use cases.
- W’re going to **dynamically show an error message** if the user types something invalid so they don’t have to wait until they submit the form to know they’re doing something wrong.
- To do this we’ll store the input’s value in state and then use that state to derive an error message which will be displayed if there is an error.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    function UsernameForm() {
      // adding state to handle username, keeping it up to date
      // updating the current state of the user's input
      const [username, setUsername] = React.useState('');
      // determine if it's lower case / displaying error message
      const isLowerCase = username === username.toLowerCase();
      const error = isLowerCase ? null : 'Username must be lower case';

      function handleSubmit(event) {
        event.preventDefault();
        alert(`You entered: ${username}`);
      }

      function handleChange(event) {
        setUsername(event.target.value);
      }

      return (
        <form onSubmit={handleSubmit}>
          <div>
            <label htmlFor="usernameInput">Username:</label>
            {/* Calling the function handleChange */}
            <input id="usernameInput" type="text" onChange={handleChange} />
          </div>
          {/* displaying error message */}
          <div style={{ color: 'red' }}>{error}</div>
          {/* disable button boolean */}
          <button disabled={Boolean(error)} type="submit">
            Submit
          </button>
        </form>
      );
    }

    ReactDOM.render(<UsernameForm />, document.getElementById('root'));
  </script>
</body>
```

## Additional resource

- [Blog post - Making dynamic form inputs with React](https://goshakkk.name/array-form-inputs/)
- [React Docs - Forms](https://reactjs.org/docs/forms.html)
- [Frontend Masters - Test a Form Component Solution](https://frontendmasters.com/courses/testing-react/test-a-form-component-solution/)
