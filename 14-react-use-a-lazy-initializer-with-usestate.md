# 14. Use a lazy initializer with useState

#### [📹 Video](https://egghead.io/lessons/react-v2-14-use-a-lazy-initializer-with-usestate?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/14-lazy-initialization?from-embed)

## Notes

- Something it's important to recognize is that every time you call the state updater function, that will trigger a re-render of the component that manages that state (the Greeting component in our example).
- This is exactly what we want to have happen, but it can be a problem in some situations and there are some optimizations we can apply for `useState` specifically in the event that it is a problem.

- In our case, we’re reading into `localStorage` to initialize our state value for the first render of our Greeting component.

- After that first render, we don’t need to read into localStorage anymore because we’re managing that state in memory now.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    function Greeting() {
      const [name, setName] = React.useState(
        // Arrow function
        //  React allows us to specify a function instead of an actual value, and then it will only call that function when it needs to – on the initial render.
        () => window.localStorage.getItem('name') || ''
      );

      // We don't want to render on every change
      // Since we're using localStorage, it's not a big deal

      React.useEffect(() => {
        window.localStorage.setItem('name', name);
      });

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

## Additional resource

- [Kent's Blog - How to implement useState with useReducer](https://kentcdodds.com/blog/how-to-implement-usestate-with-usereducer)
- [React Docs - Effects Without Cleanup](https://reactjs.org/docs/hooks-effect.html#effects-without-cleanup)
