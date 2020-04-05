# 17. Manipulate the DOM with React refs

#### [📹 Video](https://egghead.io/lessons/react-v2-17-manipulate-the-dom-with-react-refs?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/17-dom-refs?from-embed)

## Notes

- React is really good at creating and updating DOM elements, but sometimes you need to work with them yourself.
- A common use case for this is when you’re using a third party library that wasn’t built for or with React specifically.
- To do this, we need to have some value that’s associated with our component (like state) to store a reference to the DOM element, but doesn’t trigger re-renders when it’s updated (unlike state). React has something specifically for this and it’s called a ref.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script src="https://unpkg.com/vanilla-tilt@1.7.0/dist/vanilla-tilt.min.js"></script>
  <style>
    /*
    Taken from the vanilla-tilt.js demo site:
    https://micku7zu.github.io/vanilla-tilt.js/index.html
    */
    .tilt-root {
      height: 150px;
      background-color: red;
      width: 200px;
      background-image: -webkit-linear-gradient(
        315deg,
        #ff00ba 0%,
        #fae713 100%
      );
      background-image: linear-gradient(135deg, #ff00ba 0%, #fae713 100%);
      transform-style: preserve-3d;
      will-change: transform;
      transform: perspective(1000px) rotateX(0deg) rotateY(0deg) scale3d(
          1,
          1,
          1
        );
    }
    .tilt-child {
      position: absolute;
      width: 50%;
      height: 50%;
      top: 50%;
      left: 50%;
      transform: translateZ(30px) translateX(-50%) translateY(-50%);
      box-shadow: 0 0 50px 0 rgba(51, 51, 51, 0.3);
      background-color: white;
    }
    .totally-centered {
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
    }
  </style>
  <script type="text/babel">
    function Tilt({ children }) {
      const tiltRef = React.useRef();

      // refs provide a way to access DOM nodes or React elements created in the render method.
      React.useEffect(() => {
        // useRef returns a mutable ref object whose .current property is initialized to the passed argument (initialValue).
        const tiltNode = tiltRef.current;
        // The returned object will persist for the full lifetime of the component.
        const vanillaTiltOptions = {
          max: 25,
          speed: 400,
          glare: true,
          'max-glare': 0.5
        };
        // Initiating VanillaTilt and passing tiltNode and vanillaTiltOptions
        VanillaTilt.init(tiltNode, vanillaTiltOptions);
        return () => {
          // ensuring that any node refs in memory get garbage collected
          // prevent memory leaks
          tiltNode.vanillaTilt.destroy();
        };
        // adding a dependencies array, to avoid multiple renders
      }, []);

      return (
        // Referencing the useEffect hook return
        <div ref={tiltRef} className="tilt-root">
          <div className="tilt-child">{children}</div>
        </div>
      );
    }

    function App() {
      const [showTilt, setShowTilt] = React.useState(true);
      return (
        <div>
          <label>
            <input
              type="checkbox"
              checked={showTilt}
              // show and hide Tilt using the useState Hook
              onChange={e => setShowTilt(e.target.checked)}
            />{' '}
            show tilt
          </label>
          {showTilt ? (
            <Tilt>
              <div className="totally-centered">vanilla-tilt.js</div>
            </Tilt>
          ) : null}
        </div>
      );
    }

    ReactDOM.render(<App />, document.getElementById('root'));
  </script>
</body>
```

- You create a **ref object with the useRef hook** and that object’s current property is the current value of the ref.
- It can be anything, but if you pass that `ref object` to a component as a prop called `ref`, then React will set the current property to the DOM element it creates so you can reference it and manipulate it in your useEffect hook.

## Additional resource

- [Kent's egghead course - Simplify React Apps with React Hooks](https://egghead.io/courses/simplify-react-apps-with-react-hooks)
- [React Hooks - useRef](https://reactjs.org/docs/hooks-reference.html#useref)
- [Manipulating DOM Elements With React Hook useRef()](https://dev.to/spukas/manipulating-dom-elements-with-react-hook-useref-446c)
