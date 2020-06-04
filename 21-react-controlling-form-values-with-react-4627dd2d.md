# 21 Controlling Form Values with React

#### [📹 Video](https://egghead.io/lessons/react-v2-21-controlling-form-values-with-react?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/21-controlled-forms?from-embed)

## Notes

- There are many situations where you want to **programmatically control the value** of a form field.
- Maybe you want to set the value of one field based on the user’s interactions with another element. Or maybe you want to change the user’s input as they’re typing it.
- In this example, we’ll be preventing the user from typing upper case characters into our field by turning our input from an **“Uncontrolled field”** to a **“Controlled field.”**

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    function UsernameForm() {
      const [username, setUsername] = React.useState('');

      function handleSubmit(event) {
        event.preventDefault();
        alert(`You entered: ${username}`);
      }

      function handleChange(event) {
        // making sure that the value is turned into lower case
        // the input value is now handled with React
        setUsername(event.target.value.toLowerCase());
      }

      return (
        <form onSubmit={handleSubmit}>
          <div>
            <label htmlFor="usernameInput">Username:</label>
            {/* controlling the value with value={username} */}
            <input
              id="usernameInput"
              type="text"
              onChange={handleChange}
              value={username}
            />
          </div>
          <button type="submit">Submit</button>
        </form>
      );
    }

    ReactDOM.render(<UsernameForm />, document.getElementById('root'));
  </script>
</body>
```

## Additional resource

- [React Docs - Forms](https://reactjs.org/docs/forms.html)
- [Frontend Masters - Test a Form Component Solution](https://frontendmasters.com/courses/testing-react/test-a-form-component-solution/)
