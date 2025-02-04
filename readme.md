# Custom Element
A base class for Custom Elements which provides simple data binding.

This is a simple POC to demonstrate how data binding can be easily implemented using Web Components. It is not a 
replacement for React or other frameworks, nor is it intended to be.

See my [article on medium.com](https://medium.com/@drmoerkerke/https-medium-com-drmoerkerke-data-binding-for-web-components-in-just-a-few-lines-of-code-33f0a46943b3?sk=09dd590e07b3300bae4b63dbb716cc39) for an in depth explanation. 

### How it works
Inside the Shadow Root of any Web Component that extends `CustomElement` data binding can be provided through the `data-bind`
attribute on any HTML element, including other Web Components. Data binding is done through the properties of the `state` object 
inside `CustomElement`.

For example:

```
<p data-bind="title"></p>
```

means the value of the `state.title` property of `CustomElement` is bound to this `<p>`. If the value of `state.title` 
changes the `textContent` of this `<p>` will change with it.
If the value of `state.title` needs to be bound to a property of another Web Component it should be prefixed with the name
of that property and a `:`.

For example:

```
<web-component data-bind="name:title"></web-component>
```

means the property `name` of `<web-component>` is bound to `state.title`.

If `<web-component>` also extends `CustomElement` then its property `state.name` is bound to `state.title`, which allows 
for multiple levels of data binding. This is because internally the `setState` method of `<web-component>` will be invoked.

`CustomElement` also provides some convenience methods:
- `show()`, show the element
- `hide()`, hide the element
- `select(selector: string)`, select and element from the component's Shadow DOM (calls `querySelector` internally)
- `selectAll(selector: string)`, select multiple elements from the component's Shadow DOM (calls `querySelectorAll` internally)

### Demo
To run the demo, run `npm install` once and then `npm start` and view the demo on
[http://localhost:8080/](http://localhost:8080/)

### Testing
Run `npm test` and view the results on [http://localhost:8080/](http://localhost:8080/)
or run `npm run test:headless` to run the tests on the command line.

This repo also contains the configuration file `wallaby.js` to run the
tests from your IDE using [Wallaby.js](https://wallabyjs.com/)

### Browser support
- Chrome 53+
- Firefox 63+
- Safari 10+
- iOS Safari 10+
- Chrome Android 71+
- Firefox Android 64+





