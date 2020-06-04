# 16. Create reusable custom hooks

#### [📹 Video](https://egghead.io/lessons/react-v2-16-create-reusable-custom-hooks?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/16-custom-hooks?from-embed)

## Notes

- Let’s imagine a scenario where we want to share our `localStorage` code with other components so other components could synchronize state with `localStorage`.

- Considering how code reuse works in JavaScript in general, we can simply make a function, put our relevant code in that function, and then call it from the original location. That process works exactly the same with React hooks code, so let’s do that:

- **Original code**:

```js
const [name, setName] = React.useState(
  () => window.localStorage.getItem('name') || ''
);

React.useEffect(() => {
  window.localStorage.setItem('name', name);
}, [name]);
```

- **Refactor code** to a reusable custom hooks:

```js
//
function useLocalStorageState(key, defaultValue = '') {
  const [state, setState] = React.useState(
    () => window.localStorage.getItem(key) || defaultValue
  );

  React.useEffect(() => {
    window.localStorage.setItem(key, state);
  }, [key, state]);

  return [state, setState];
}
```

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    // the community standard is to use `useWhateverName` following React Hooks name standards
    // providing key for localStorage and defaultValue
    function useLocalStorageState(key, defaultValue = '') {
      const [state, setState] = React.useState(
        () => window.localStorage.getItem(key) || defaultValue
      );

      React.useEffect(() => {
        window.localStorage.setItem(key, state);
        // Make sure to add key to our array
      }, [key, state]);
      // Getting access to state and setState
      // a custom Hook doesn’t need to have a specific signature.
      // We can decide what it takes as arguments
      return [state, setState];
    }

    function Greeting() {
      // calling our useLocalStorageState
      const [name, setName] = useLocalStorageState('name');

      const handleChange = event => setName(event.target.value);

      return (
        <div>
          <form>
            <label htmlFor="name">Name: </label>
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

- When we want to share logic between two JavaScript functions, we extract it to a third function. Both components and Hooks are functions, so this works for them too!
- Building your own Hooks lets you extract component logic into reusable functions.

## Additional resource

- [eslint-plugin-react-hooks](https://www.npmjs.com/package/eslint-plugin-react-hooks)
- [Kent's Blog - The State Reducer Pattern with React Hooks](https://kentcdodds.com/blog/usememo-and-usecallback)
- [React Docs - Building Your Own Hooks](https://reactjs.org/docs/hooks-custom.html)
