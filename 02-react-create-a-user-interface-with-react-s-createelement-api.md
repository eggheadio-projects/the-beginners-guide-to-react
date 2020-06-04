# 02. Create a User Interface with React’s createElement API

#### [📹 Video](https://egghead.io/lessons/react-v2-02-create-a-user-interface-with-react-s-createelement-api?pl=a-beginners-guide-to-react-v2-6c4d)

#### [💻 CodeSandbox](https://codesandbox.io/s/github/kentcdodds/beginners-guide-to-react/tree/codesandbox/02-react-create-element?from-embed)

## Notes

- React uses the same APIs to control and update the DOM that we did in the previous lesson.
- Instead of creating DOM elements, we’ll create React elements and then hand those off to `react-dom` to handle turning those into DOM elements and putting them into the page.
- If you’ve ever learned or used React before, you’re probably more familiar with JSX than React’s `createElement` API, but it’s important to understand the `createElement` API first so you understand the magic.

- Get `react` and `react-dom` from unpkg.com, using a fixed version:

```
unpkg.com/react@16.12.0/umd/react.production.min.js
unpkg.com/react-dom@16.12.0/umd/react-dom.production.min.js
```

- And add a `script` tag to the page:

```html
<script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
```

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script type="text/javascript">
    const rootElement = document.getElementById('root');
    // specify properties on creation, as an object
    const element = React.createElement('div', {
      className: 'container',
      children: 'Hello World'
    });
    // use `react-dom` to render those elements to the page
    console.log(element);
    // props argument is what we passed as a second argument
    // we can also specify it as an array
    // Example: children: ['Hello World', ", Goodbye World"]
    ReactDOM.render(element, rootElement);
  </script>
</body>
```

- Now with `react` you can create `React.createElement` and use `react-dom` to render those elements to the page.
- `React.createElement` API is as simple as the element that you want to create `<div>`, and then an object that has all of the props that you want to have applied, `className`, `children`.
- Just as a convenience, you can provide the `children` with any number of arguments after the props argument as well.

## Additional resource

- [React Top-Level API](https://reactjs.org/docs/react-api.html)
- [React Without JSX](https://reactjs.org/docs/react-without-jsx.html)
