# 19. Make Basic Forms with React

#### [📹 Video](https://egghead.io/lessons/react-v2-19-make-basic-forms-with-react?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/19-basic-forms?from-embed)

## Notes

- Forms are a basic building block of the web. Every web application uses form elements as a way to accept input from the user.

- There are a few things to keep in mind with how forms work on the web and in this lesson we’ll learn about those as well as various ways you can retrieve values from elements in the form as well as a few best practices you should consider when working with form elements on the web.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    function UsernameForm() {
      // When submitting a form, it automatically makes a post request with the data
      function handleSubmit(event) {
        // preventing from automatically sending a post request/full page refresh
        event.preventDefault();
        // Please don't use this:
        // document.querySelector('input').value, this breaks the encapsulation

        // we can access the form element directly, console.dir(event.target)
        // one option: const username = event.target[0].value
        // If ref is not needed, then use the id
        const username = event.target.elements.usernameInput.value;
        // Alerting this to users or sending this to backend server
        alert(`You entered: ${username}`);
      }

      return (
         {/* Creating a form  */}
        <form onSubmit={handleSubmit}>
          <div>
            {/* adding a label - htmlFor="usernameInput" */}
            <label htmlFor="usernameInput">Username:</label>
            <input id="usernameInput" type="text" />
          </div>
          {/* Forms are automatically submitted on type="submit*/}
          {/* Make sure to specify the type on the button */}
          <button type="submit">Submit</button>
        </form>
      );
    }

    ReactDOM.render(<UsernameForm />, document.getElementById('root'));
  </script>
</body>
```

- You can learn more about basic forms in the React documentation about Uncontrolled Components.

## Additional resource

- [React Docs - Forms](https://reactjs.org/docs/forms.html)
- [Kent's Blog - Please stop building inaccessible forms](https://kentcdodds.com/blog/please-stop-building-inaccessible-forms-and-how-to-fix-them)
- [Kent's Livestream - Testing a Multi-Page form](https://www.youtube.com/watch?v=9xaJ78qEJCM)
