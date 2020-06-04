# 24. Lifting and colocating React State

#### [📹 Video](https://egghead.io/lessons/react-v2-24-lifting-and-colocating-react-state?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/24-lifting-and-colocating?from-embed)

## Notes

- A **common question** from React beginners is how to share state between two sibling components.
- **The answer** is to Lift the state which basically amounts to finding the lowest common parent shared between the two components and placing the state management there, and then passing the state and a mechanism for updating that state down into the components that need it.

- As a community we’re pretty good at doing this and it becomes natural over time. One thing that we typically have trouble remembering to do is to **push state back down** (or colocate state).

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    function Name({ name, onNameChange }) {
      return (
        <div>
          <label>Name: </label>
          <input value={name} onChange={onNameChange} />
        </div>
      );
    }
    // In React, sharing state is accomplished by moving it up to the closest
    // common ancestor of the components that need it.
    // This is called “lifting state up”.

    function FavoriteAnimal() {
      const [animal, setAnimal] = React.useState('');
      return (
        <div>
          <label>Favorite Animal: </label>
          <input
            value={animal}
            onChange={event => setAnimal(event.target.value)}
          />
        </div>
      );
    }

    // Since any state “lives” in some component and that
    // component alone can change it, the surface area for bugs is greatly reduced.

    function Display({ name }) {
      return <div>{`Hey ${name}, you are great!`}</div>;
    }

    function App() {
      const [name, setName] = React.useState('');
      return (
        <form>
          <Name
            name={name}
            onNameChange={event => setName(event.target.value)}
          />
          <FavoriteAnimal />
          <Display name={name} />
        </form>
      );
    }

    ReactDOM.render(<App />, document.getElementById('root'));
  </script>
</body>
```

- Lifting state involves writing more “boilerplate” code than two-way binding approaches, but as a benefit, it takes less work to find and isolate bugs.

## Additional resource

[Kent's Blog - State Colocation will make your React app faster](https://kentcdodds.com/blog/state-colocation-will-make-your-react-app-faster)
[Kent's Blog - Application State Management with React](https://kentcdodds.com/blog/application-state-management-with-react)
[React Docs - Lifting State Up](https://reactjs.org/docs/lifting-state-up.html)
