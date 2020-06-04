# 25. Make HTTP Requests with React

#### [📹 Video](https://egghead.io/lessons/react-v2-25-make-http-requests-with-react?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/25-http?from-embed)

## Notes

- Most useful React applications involve interacting with a server to load and persist data. To do this on the web, we use **HTTP requests** with the browser’s built-in fetch API.
- HTTP requests like this are inherently asynchronous in nature and **they’re also side-effects** so we’ll need to manage not only starting the request, but also what we should show the user while the request is “in flight.”

- In this lesson we’ll use a public **GraphQL server**that serves up pokemon data to load information for a given pokemon name. We’ll learn how to fetch that data inside a React.useEffect callback and display the results when the request completes.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    function PokemonInfo({ pokemonName }) {
      const [pokemon, setPokemon] = React.useState(null);

      React.useEffect(() => {
        if (!pokemonName) {
          return;
        }
        // Calling fetchPokemon and setting state for the data
        fetchPokemon(pokemonName).then(pokemonData => {
          setPokemon(pokemonData);
        });
      }, [pokemonName]);

      if (!pokemonName) {
        return 'Submit a pokemon';
      }

      if (!pokemon) {
        return '...';
      }
      // The effect hook called useEffect is used to fetch the data with axios from the API
      // and to set the data in the local state of the component with the state hook's update function.
      // The promise resolving happens with async/await.

      return <pre>{JSON.stringify(pokemon, null, 2)}</pre>;
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
    // GraphQL server that serves up pokemon data to load information for a given pokemon name
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

      // The Fetch API is a web standard built into most modern browsers to let us make HTTP requests to the server.
      // Using the Fetch API starts with calling the fetch() function, which allows us to make HTTP requests with the standard HTTP verbs: GET, POST, PUT, PATCH and DELETE.
      // The fetch function returns a promise which resolves when the request completes.
      // Making fetch call is a side-effect, so we are going to use the useEffect Hook
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

- [egghead courses - GraphQL](https://egghead.io/browse/tools/graphql)
- [React Docs - AJAX and APIs](https://reactjs.org/docs/faq-ajax.html)
- [Kent's Livestream - Testing axios](https://www.youtube.com/watch?v=YJKtzS1jGsI)
- [MDN - An overview of HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
