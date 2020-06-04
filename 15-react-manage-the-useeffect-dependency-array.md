# 15. Manage the useEffect dependency array

#### [📹 Video](https://egghead.io/lessons/react-v2-15-manage-the-useeffect-dependency-array?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/15-effect-deps?from-embed)

## Notes

- Something that’s really important to know about **React’s useEffect** hook is that it eagerly attempts to synchronize the “state of the world” with the state of your application. That means that your effect callback will run every time your component is rendered.

- Our effect callback is getting called more than it needs to be. **Solution**, add a dependency array so it is updated only when the state it relies on changes.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    function Greeting() {
      const [name, setName] = React.useState(
        () => window.localStorage.getItem('name') || ''
      );

      // our effect callback is getting called more than it needs to be
      {
        /* 
      React.useEffect(() => {
        window.localStorage.setItem('name', name);
      });
      */
      }

      // add a dependency array so it is updated only when the state it relies on changes
      // This normally won’t lead to bugs but it can definitely be sub-optimal
      // and in some cases can result in an infinite loop
      React.useEffect(() => {
        window.localStorage.setItem('name', name);
      }, [name]);

      // You’ll want to make sure you have and follow the rules from the ESLint plugin: eslint-plugin-react-hooks
      // tools like Create React App have this installed and configured by default

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

    function App() {
      const [count, setCount] = React.useState(0);
      return (
        <>
          <button onClick={() => setCount(c => c + 1)}>{count}</button>
          <Greeting />
        </>
      );
    }

    ReactDOM.render(<App />, document.getElementById('root'));
  </script>
</body>
```

## Additional resource

- [Kent's Blog - 5 Tips to Help You Avoid React Hooks Pitfalls](https://kentcdodds.com/blog/react-hooks-pitfalls)
- [egghead.io - Handle Deep Object Comparison in React's useEffect hook with the useRef Hook](https://egghead.io/lessons/react-handle-deep-object-comparison-in-react-s-useeffect-hook-with-the-useref-hook)
- [eslint-plugin-react-hooks](https://www.npmjs.com/package/eslint-plugin-react-hooks)
- [React Docs - ESLint Plugin](https://reactjs.org/docs/hooks-rules.html#explanation)
