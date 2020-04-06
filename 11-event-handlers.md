# 11. Use Event Handlers with React

#### [📹 Video](https://egghead.io/lessons/react-v2-11-use-event-handlers-with-react?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/11-event-handlers?from-embed)

## Notes

- There are a ton of supported events that you can find on the [docs](https://reactjs.org/docs/handling-events.html). Let’s get an introduction to event handlers with React.

- We still haven’t gotten to state yet, so we’ve implemented our own little way of managing state and re-rendering our component so we can play around with event handlers.

- One thing you’ll want to know is that events with React are very similar to working with events in regular DOM.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    const rootElement = document.getElementById('root');

    // The current state of our app
    const state = { eventCount: 0, username: '' };

    function App() {
      function handleClick() {
        setState({ eventCount: state.eventCount + 1 });
      }

      function handleChange(event) {
        // Getting current value from the input
        console.log(event);
        // Getting the SyntheticEvent
        console.log(event.nativeEvent);
        // Getting the nativeEvent if needed
        setState({ username: event.target.value });
      }

      return (
        <div>
          <p>There have been {state.eventCount} events.</p>
          <p>
            {/* We can have different types of events here that are supported by React: https://reactarmory.com/guides/react-events-cheatsheet */}
            <button onClick={handleClick}>Click Me</button>
          </p>
          <p>You typed: {state.username}</p>
          <p>
            <input onChange={handleChange} />
          </p>
        </div>
      );
    }

    // This is generally not how you handle state
    function setState(newState) {
      Object.assign(state, newState);
      renderApp();
    }

    function renderApp() {
      ReactDOM.render(<App />, document.getElementById('root'));
    }

    renderApp();
  </script>
</body>
```

- React does have an optimization implementation on top of the event system called [SyntheticEvents](https://reactjs.org/docs/events.html), but most of the time you won’t observe any difference with those events from regular DOM events (and you can always get access to the native event using the nativeEvent property).

## Additional resource

- [React Docs - Handling Events](https://reactjs.org/docs/handling-events.html)
- [Kent Livestream](https://www.youtube.com/watch?v=WqFlnolg7mo)
- [React Event Handlers: onClick, onChange ...](https://www.robinwieruch.de/react-event-handler)
