# 26. Handle HTTP Errors with React

#### [📹 Video](https://egghead.io/lessons/react-v2-26-handle-http-errors-with-react?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/26-http-errors?from-embed)

## Notes

- Unfortunately, sometimes a server request fails and we need to display a helpful error message to the user.
- We’ll handle a promise rejection so we can collect that error information, and we’ll also learn how we can best display manage the state of our request so we have a deterministic render method to ensure we always show the user the proper information based on the current state of our React component.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    function PokemonInfo({ pokemonName }) {
      // A common mistake people make is to create a state variable called `isLoading` and set that to true or false.
      // Instead, we’ll be using a status variable which can be set to idle, pending, resolved, or rejected.

      // Adding state to Pokemon status
      const [status, setStatus] = React.useState('idle');
      const [pokemon, setPokemon] = React.useState(null);
      // Adding state to handle errors
      const [error, setError] = React.useState(null);

      React.useEffect(() => {
        if (!pokemonName) {
          return;
        }
        // setting the status when the data is resolved
        setStatus('pending');
        fetchPokemon(pokemonName).then(
          pokemonData => {
            setStatus('resolved');
            setPokemon(pokemonData);
          },
          errorData => {
            setStatus('rejected');
            setError(errorData);
          }
        );
      }, [pokemonName]);
      // this is very predictable, now that we can handle the status
      // In order to force an error yourself, you can alter the pokemonQuery into something invalid.
      if (status === 'idle') {
        return 'Submit a pokemon';
      }

      if (status === 'rejected') {
        return 'Oh no...';
      }

      if (status === 'pending') {
        return '...';
      }

      if (status === 'resolved') {
        return <pre>{JSON.stringify(pokemon, null, 2)}</pre>;
      }
    }

    function App() {
      const [pokemonName, setPokemonName] = React.useState('');

      function handleSubmit(event) {
        event.preventDefault();
        setPokemonName(event.target.elements.pokemonName.value);
      }

      return (
        <div>
          <form onSubmit={handleSubmit}>
            <label htmlFor="pokemonName">Pokemon Name</label>
            <div>
              <input id="pokemonName" />
              <button type="submit">Submit</button>
            </div>
          </form>
          <hr />
          <PokemonInfo pokemonName={pokemonName} />
        </div>
      );
    }

    function fetchPokemon(name) {
      const pokemonQuery = `
        query ($name: String) {
          pokemon(name: $name) {
            id
            number
            name
            attacks {
              special {
                name
                type
                damage
              }
            }
          }
        }
      `;

      return window
        .fetch('https://graphql-pokemon.now.sh', {
          // learn more about this API here: https://graphql-pokemon.now.sh/
          method: 'POST',
          headers: {
            'content-type': 'application/json;charset=UTF-8'
          },
          body: JSON.stringify({
            query: pokemonQuery,
            variables: { name }
          })
        })
        .then(r => r.json())
        .then(response => response.data.pokemon);
    }

    ReactDOM.render(<App />, document.getElementById('root'));
  </script>
</body>
```

## Additional resource

- [ROBIN WIERUCH - How to fetch data with React Hooks?](https://www.robinwieruch.de/react-hooks-fetch-data)
- [Kent's Blog - How to use React Context effectively](https://kentcdodds.com/blog/how-to-use-react-context-effectively)
- [repo - react-error-boundary](https://github.com/bvaughn/react-error-boundary)
