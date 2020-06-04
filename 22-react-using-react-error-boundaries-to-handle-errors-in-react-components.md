# 22. Using React Error Boundaries to handle errors in React Components

#### [📹 Video](https://egghead.io/lessons/react-v2-22-using-react-error-boundaries-to-handle-errors-in-react-components?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/22-error-boundaries?from-embed)

## Notes

- There’s a simple way to handle errors in your application using a special kind of component called an Error Boundary. Unfortunately, there is currently no way to create an Error Boundary component with a function and you have to use a class component instead, but we got another lucky break because there’s a terrific open source library we can use called [react-error-boundary](https://github.com/bvaughn/react-error-boundary).

- Error boundaries are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of the component tree that crashed.

- Error boundaries catch errors during rendering, in lifecycle methods, and in constructors of the whole tree below them.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script src="https://unpkg.com/react-error-boundary@1.2.5/dist/umd/react-error-boundary.js"></script>
  <script type="text/babel">
    // This is recommended:
    const ErrorBoundary = ReactErrorBoundary.ErrorBoundary;
    // error boundaries need to be a class component
    // returning this.props.children

    // class ErrorBoundary extends React.Component {
    //   state = {error: null}
    //   static getDerivedStateFromError(error) {
    //     return {error}
    //   }
    //   render() {
    //     const {error} = this.state
    //     if (error) {
    //       return <this.props.FallbackComponent error={error} />
    //     }

    //     return this.props.children
    //   }
    // }

    function ErrorFallback({ error }) {
      return (
        <div>
          {/* controlling error by ErrorBoundary */}
          <p>Something went wrong:</p>
          <pre>{error.message}</pre>
        </div>
      );
    }

    function Bomb() {
      // when this function is called, it throws an error
      throw new Error('💥 CABOOM 💥');
      // Note that error boundaries only catch errors in the components below them in the tree.
    }

    function App() {
      const [explode, setExplode] = React.useState(false);
      return (
        <div>
          <div>
            <button onClick={() => setExplode(true)}>💣</button>
          </div>
          <div>
            {/* controlling error by ErrorBoundary */}
            {/* + providing ErrorFallback */}
            <ErrorBoundary FallbackComponent={ErrorFallback}>
              {explode ? <Bomb /> : 'Push the button Max!'}
            </ErrorBoundary>
          </div>
        </div>
      );
    }
    ReactDOM.render(<App />, document.getElementById('root'));
  </script>
</body>
```

- The granularity of error boundaries is up to you. You may wrap top-level route components to display a “Something went wrong” message to the user, just like server-side frameworks often handle crashes.

## Additional resource

- [React Docs - Error Boundaries](https://reactjs.org/docs/error-boundaries.html)
- [egghead lesson - Handle React Suspense Errors with an Error Boundary](https://egghead.io/lessons/react-handle-react-suspense-errors-with-an-error-boundary)
- [repo - react-error-boundary](https://github.com/bvaughn/react-error-boundary)
- [npm - react-error-boundary](https://www.npmjs.com/package/react-error-boundary)
