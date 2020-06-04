# 13. Manage side-effects in a React Component with the useEffect hook

#### [📹 Video](https://egghead.io/lessons/react-v2-13-manage-side-effects-in-a-react-component-with-the-useeffect-hook?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/13-side-effects?from-embed)

## Notes

- Another piece to the web application puzzle is managing side-effects of our user’s interactions.

- In this lesson we’ll be interacting with the browser’s **localStorage API**, but this same thing would apply if we’re interacting with a backend server, or the geolocation API, or anything else that needs to happen when the state of our component changes.

- You’ll learn how to use **React’s useEffect hook** to manage the side-effect of saving state into localStorage, and also how to re-synchronize our application with the stored value in localStorage.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    function Greeting() {
      // using useState
      const [name, setName] = React.useState(
        // we are getting the name from localStorage or default to empty string
        window.localStorage.getItem('name') || ''
      );

      // The Effect Hook lets you perform side effects in function components
      // Load every time the Greeting() is rendered
      React.useEffect(() => {
        // The read-only localStorage property allows you to access a Storage object for the
        // document's origin; the stored data is saved across browser sessions.
        window.localStorage.setItem('name', name);
      });

      const handleChange = event => setName(event.target.value);

      return (
        <div>
          <form>
            <label htmlFor="name">Name: </label>
            {/* showing the current state of name prop */}
            <input value={name} onChange={handleChange} id="name" />
          </form>
          {name ? <strong>Hello {name}</strong> : 'Please type your name'}
        </div>
      );
    }

    ReactDOM.render(<Greeting />, document.getElementById('root'));
  </script>
</body>
```

## Additional resource

- [React Docs - useEffect hook](https://reactjs.org/docs/hooks-effect.html)
- [React Docs - API reference](https://reactjs.org/docs/hooks-reference.html#useeffect)
- [Kent's Blog - useEffect vs useLayoutEffect](https://kentcdodds.com/blog/useeffect-vs-uselayouteffect)
- [MDN - Window.localStorage docs](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)
