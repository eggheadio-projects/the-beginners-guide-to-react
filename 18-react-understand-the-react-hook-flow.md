# 18 Understand the React Hook Flow

#### [📹 Video](https://egghead.io/lessons/react-v2-18-understand-the-react-hook-flow?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/18-hook-flow?from-embed)

## Notes

- Understanding the order in which React hooks are called can be really helpful in using React hooks effectively.

- We’ll explore the lifecycle of a function component with hooks with colorful console log statements so we know when one phase starts and when it ends.

![](https://res.cloudinary.com/dg3gyk0gu/image/upload/v1591296082/transcript-images/react-understand-the-react-hook-flow-hook-flow.jpg)

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    // https://github.com/donavon/hook-flow

    function Child() {
      console.log('%c    Child: render start', 'color: MediumSpringGreen');
      // A useState Hook and console logging several useEffect Hooks
      const [count, setCount] = React.useState(() => {
        console.log('%c    Child: useState callback', 'color: tomato');
        return 0;
      });

      // The useEffect hooks are called in order starting from the child useEffect
      React.useEffect(() => {
        console.log('%c    Child: useEffect no deps', 'color: LightCoral');
        return () => {
          console.log(
            '%c    Child: useEffect no deps cleanup',
            'color: LightCoral'
          );
        };
      });

      React.useEffect(() => {
        console.log(
          '%c    Child: useEffect empty deps',
          'color: MediumTurquoise'
        );
        return () => {
          console.log(
            '%c    Child: useEffect empty deps cleanup',
            'color: MediumTurquoise'
          );
        };
      }, []);

      React.useEffect(() => {
        console.log('%c    Child: useEffect with dep', 'color: HotPink');
        return () => {
          console.log(
            '%c    Child: useEffect with dep cleanup',
            'color: HotPink'
          );
        };
      }, [count]);

      // Creating our React element
      const element = (
        // Providing an update function, triggering a re-render
        <button onClick={() => setCount(previousCount => previousCount + 1)}>
          {count}
        </button>
      );

      // Console log that our React element is finished
      console.log('%c    Child: render end', 'color: MediumSpringGreen');

      return element;
    }

    function App() {
      console.log('%cApp: render start', 'color: MediumSpringGreen');
      // A boolean useState
      const [showChild, setShowChild] = React.useState(() => {
        console.log('%cApp: useState callback', 'color: tomato');
        return false;
      });

      // The useEffect Hooks are called in order
      React.useEffect(() => {
        console.log('%cApp: useEffect no deps', 'color: LightCoral');
        return () => {
          console.log('%cApp: useEffect no deps cleanup', 'color: LightCoral');
        };
      });
      // Since this has no dependencies, it will not be called on updates
      React.useEffect(() => {
        console.log('%cApp: useEffect empty deps', 'color: MediumTurquoise');
        return () => {
          console.log(
            '%cApp: useEffect empty deps cleanup',
            'color: MediumTurquoise'
          );
        };
      }, []);
      // Running useEffect
      React.useEffect(() => {
        console.log('%cApp: useEffect with dep', 'color: HotPink');
        return () => {
          console.log('%cApp: useEffect with dep cleanup', 'color: HotPink');
        };
      }, [showChild]);

      // Rendering UI child `Child: render start`
      const element = (
        <>
          <label>
            <input
              type="checkbox"
              checked={showChild}
              onChange={e => setShowChild(e.target.checked)}
            />{' '}
            show child
          </label>
          <div
            style={{
              padding: 10,
              margin: 10,
              height: 30,
              width: 30,
              border: 'solid'
            }}
          >
            {/* Creating a component but only after initial render when showChild checkbox is checked */}
            {/* If it's not being called, it's only creating React objects  */}
            {showChild ? <Child /> : null}
            {/* when showChild is toggled off, it removes the Child component and calls for a cleanup  */}
          </div>
        </>
      );

      console.log('%cApp: render end', 'color: MediumSpringGreen');

      return element;
    }

    ReactDOM.render(<App />, document.getElementById('root'));
  </script>
</body>
```

- Understanding all of this is not critical to your success with using React, and most of the time you won’t need to think about this at all, but understanding it can help you at times.

## Additional resource

- [A flowchart that explains the new lifecycle of a Hooks component](https://github.com/donavon/hook-flow)
- [React Hooks: What's going to happen to my tests?](https://kentcdodds.com/blog/react-hooks-whats-going-to-happen-to-my-tests)
- [Kent's Livestream - React Hooks: Refactor compound components to hooks](https://www.youtube.com/watch?v=415EfGPuhSo)
