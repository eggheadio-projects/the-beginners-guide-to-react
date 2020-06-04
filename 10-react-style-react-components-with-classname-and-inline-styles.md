# 10. Style React Components with className and inline Styles

#### [📹 Video](https://egghead.io/lessons/react-v2-10-style-react-components-with-classname-and-inline-styles?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/10-styling?from-embed)

## Notes

- The application layout is only one part of the user interface equation. Another part is **styling**.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <style>
    .box {
      border: 1px solid #333;
      display: flex;
      flex-direction: column;
      justify-content: center;
      text-align: center;
    }
    .box--large {
      width: 270px;
      height: 270px;
    }
    .box--medium {
      width: 180px;
      height: 180px;
    }
    .box--small {
      width: 90px;
      height: 90px;
    }
  </style>
  <script type="text/babel">
    function Box({ style, size, className = '', ...rest }) {
      const sizeClassName = size ? `box--${size}` : '';
      return (
        <div
          className={`box ${className} ${sizeClassName}`}
          style={{ fontStyle: 'italic', ...style }}
          {...rest}
        />
      );
    }

    const element = (
      <div>
        <Box size="small" style={{ backgroundColor: 'lightblue' }}>
          small lightblue box
        </Box>
        <Box size="medium" style={{ backgroundColor: 'pink' }}>
          medium pink box
        </Box>
        <Box size="large" style={{ backgroundColor: 'orange' }}>
          large orange box
        </Box>
        <Box>sizeless box</Box>
      </div>
    );

    ReactDOM.render(element, document.getElementById('root'));
  </script>
</body>
```

- One of the most basic ways to style React components is with inline CSS. JSX elements can take a style attribute which takes in an object:

```js
const element = (
  <div>
    <div
      className="box box--small"
      style={{ fontStyle: 'italic', backgroundColor: 'lightblue' }}
    >
      small lightblue box
    </div>
  </div>
);
```

- The style property is wrapped in **two sets of curly braces**, one to interpolate JavaScript and the second to define the object.

```js
function Box({ style, size, className = '', ...rest }) {
  return (
    <div
      className={`box ${className}`}
      style={{ fontStyle: 'italic', ...style }}
      {...rest}
    />
  );
}
```

The next thing we'll do is make a reusable Box component. It would be better if the author could just define a size like `small`, `medium` or `large`. In this example we destructure size instead of `className`. That's why we could replace `className` with a size property that takes in a string:

```js
function Box({ style, size, className = '', ...rest }) {
  const sizeClassName = size ? `box--${size}` : '';
  return (
    <div
      className={`box ${className} ${sizeClassName}`}
      style={{ fontStyle: 'italic', ...style }}
      {...rest}
    />
  );
}

const element = (
  <div>
    <Box size="small" style={{ backgroundColor: 'lightblue' }}>
      small lightblue box
    </Box>
    <Box size="medium" style={{ backgroundColor: 'pink' }}>
      medium pink box
    </Box>
    <Box size="large" style={{ backgroundColor: 'orange' }}>
      large orange box
    </Box>
    <Box>sizeless box</Box>
  </div>
);
```

## Additional resource

- [Tailwind CSS Docs](https://tailwindcss.com)
- [styled-components](https://github.com/styled-components/styled-components)
- [React Docs - Styling and CSS](https://reactjs.org/docs/faq-styling.html)
- [Why do I have to use "className" instead of "class" in ReactJs components done in JSX?](https://www.quora.com/Why-do-I-have-to-use-className-instead-of-class-in-ReactJs-components-done-in-JSX-JSX-is-preprocessed-so-shouldnt-that-conversion-happen-when-JSX-is-converted-to-JavaScript)
