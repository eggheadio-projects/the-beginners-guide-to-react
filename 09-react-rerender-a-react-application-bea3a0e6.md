# 09. Rerender a React Application

#### [📹 Video](https://egghead.io/lessons/react-v2-09-rerender-a-react-application?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/09-re-render?from-embed)

## Notes

- Updating the DOM is typically the slowest part of the whole process. React only updates what’s necessary.
- React DOM compares the element and its children to the previous one, and only applies the DOM updates necessary to bring the DOM to the desired state.
- When we re-render the entire app with `setInterval` you can see the clock changes without a browser window refresh.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    const rootElement = document.getElementById('root');

    function tick() {
      const time = new Date().toLocaleTimeString();
      const element = `
        <div>
          <input value="${time}" />
          <input value="${time}" />
        </div>
      `;
      rootElement.innerHTML = element;
    }

    tick();
    setInterval(tick, 1000);
  </script>
</body>
```

- The `focus` remains on the selected element because React keeps track of it. React also keeps track of the actual changes within our app so even though we call `ReactDOM.render` every second, it will not refresh every element inside, just the `time` value.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    const rootElement = document.getElementById('root');

    function tick() {
      const time = new Date().toLocaleTimeString();
      const element = (
        <>
          <input value={time} />
          <input value={time} />
        </>
      );
      ReactDOM.render(element, rootElement);
    }

    tick();
    setInterval(tick, 1000);
  </script>
</body>
```

- Even though we create an element describing the whole UI tree on every tick, only the text node whose contents have changed gets updated by React DOM.

## Additional resource

- [kent's Blog - One simple trick to optimize React re-renders](https://kentcdodds.com/blog/optimize-react-re-renders/)
- [React Docs - Rendering Elements](https://reactjs.org/docs/rendering-elements.html)
- [React Docs - ReactDOM](https://reactjs.org/docs/react-dom.html)
