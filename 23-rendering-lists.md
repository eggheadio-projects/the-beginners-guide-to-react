# 23. Use the key prop when Rendering a List with React

#### [📹 Video](https://egghead.io/lessons/react-v2-23-use-the-key-prop-when-rendering-a-list-with-react?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/23-rendering-lists?from-embed)

## Notes

- It doesn’t take long working with React before you want to render a list of items and when you do, you’ll inevitably encounter this console warning: “**Warning**: Each child in a list should have a unique key prop.”
- This warning is pretty simple to silence by providing the bespoke `key` prop, but it is really useful to understand what that warning is about and the bugs that can happen if you do not address the warning properly.
- `Keys` help React identify which items have changed, are added, or are removed. `Keys` should be given to the elements inside the array to give the elements a stable identity:

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    const allItems = [
      { id: 'a', value: 'apple' },
      { id: 'o', value: 'orange' },
      { id: 'g', value: 'grape' },
      { id: 'p', value: 'pear' }
    ];

    function App() {
      const [items, setItems] = React.useState(allItems);

      function addItem() {
        setItems([...items, allItems.find(i => !items.includes(i))]);
      }

      function removeItem(item) {
        setItems(items.filter(i => i !== item));
      }

      return (
        <div>
          <button disabled={items.length >= allItems.length} onClick={addItem}>
            add item
          </button>
          <ul style={{ listStyle: 'none', paddingLeft: 0 }}>
            {items.map(item => (
              // each iteam needs to have a key prop
              // We’re using inputs in this example
              // but the same thing can happen for your own components that maintain state.
              <li>
                <button onClick={() => removeItem(item)}>remove</button>{' '}
                <label htmlFor={`${item.value}-input`}>{item.value}</label>{' '}
                <input id={`${item.value}-input`} defaultValue={item.value} />
              </li>
              // The best way to pick a key is to use a string that uniquely
              // identifies a list item among its siblings
            ))}
          </ul>
        </div>
      );
    }

    ReactDOM.render(<App />, document.getElementById('root'));
  </script>

  <script type="text/babel">
    function FocusDemo() {
      const [items, setItems] = React.useState([
        { id: 'a', value: 'apple' },
        { id: 'o', value: 'orange' },
        { id: 'g', value: 'grape' },
        { id: 'p', value: 'pear' }
      ]);

      React.useEffect(() => {
        const interval = setInterval(() => {
          setItems(shuffle(items));
        }, 1000);
        return () => clearInterval(interval);
      }, []);

      return (
        <div>
          <div>
            <h1>Without Key</h1>
            {items.map(item => (
              <input value={item.value} />
            ))}
          </div>
          <div>
            <h1>With Key as Index</h1>
            {items.map((item, index) => (
              <input key={index} value={item.value} />
            ))}
          </div>
          <div>
            <h1>With Key</h1>
            {items.map(item => (
              <input key={item.id} value={item.value} />
            ))}
          </div>
        </div>
      );
    }

    function shuffle(originalArray) {
      const array = [...originalArray];
      let currentIndex = array.length;
      let temporaryValue;
      let randomIndex;
      // While there remain elements to shuffle...
      while (0 !== currentIndex) {
        // Pick a remaining element...
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;
        // And swap it with the current element.
        temporaryValue = array[currentIndex];
        array[currentIndex] = array[randomIndex];
        array[randomIndex] = temporaryValue;
      }
      return array;
    }
    // uncomment this line to demo:
    // ReactDOM.render(<FocusDemo />, document.getElementById('root'))
  </script>
</body>
```

- You definitely do not want to ignore this warning.
- It's not recommend using indexes for `keys` if the order of items may change. This can negatively impact performance and may cause issues with component state.

## Additional resource

- [React Docs - Recursing On Children](https://reactjs.org/docs/reconciliation.html#recursing-on-children)
- [Kent's Blog - Understanding React's key prop](https://kentcdodds.com/blog/understanding-reacts-key-prop)
