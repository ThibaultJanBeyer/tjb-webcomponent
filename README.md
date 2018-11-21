# tjb-webcomponent

Dead Simple helper Class for creating HTMLElements (native WebComponents).  
_This is a heavily improved version of [@Tonis2](https://github.com/tonis2) [Kelbas](https://github.com/tonis2/kelbas)_

![gzip size](http://img.badgesize.io/https://thibaultjanbeyer.github.io/tjb-WebComponent/tjb-wc.min.js?compression=gzip)

## Benefits

Take away amount of boilerplate to create:

- ShadowDom combining CSS & HTML nodes
- Add getters and setters to watched attributes:
  So for each attribute `myClass.foo = 'bar'` will work the same as `myClass.setAttribute('foo', 'bar')`

## Add to project

### Include via HTML

```html
<script
  src="https://thibaultjanbeyer.github.io/tjb-WebComponent/tjb-wc.min.js"
  type="module"
></script>
```

### Include via JavaScript

```JavaScript
import WebComponent from 'https://thibaultjanbeyer.github.io/tjb-WebComponent/tjb-wc.min.js'
```

### Include via NPM

Console:

```bash
npm i -S tjb-WebComponent
```

Then in your code:

```JavaScript
import WebComponent from 'tjb-WebComponent'
```

## Useage

When defining your WebComponent, instead of extending `HTMLElement` just extend `WebComponent` like so:

```JavaScript
class MyClass extends WebComponent {
  // do something here
}
```

That’s it. You’re ready to use the WebComponent helper like so:

- With any html template tool

```JavaScript
class MyClass extends WebComponent {

  CSS() {
    return html`
      <style>
        .orange {
          color: orange;
        }

        .blue {
          color: blue;
        }
      </style>
    `;
  }

  HTML() {
    return html`
      <div class="orange">I’m an orange text</div>
    `;
  }

  static get observedAttributes() {
    return ['color']
  }

  handleColorChange(newValue, oldValue) {
    this.domNode.className = newValue;
  }
}

customElements.define("my-class", MyClass);
```

Now you can use it just as any other Web Component:

```html
<my-class></my-class>
```

You would be able to change the color for instance like so:

```JavaScript
const node = document.querySelector('my-class'); // get the node if you don’t already have it
node.color = 'blue'; // will call handleColorChange and add the class 'blue'
// this is equivalent to node.setAttribute('color', 'blue')
// or also <my-class color="blue"></my-class>
```

# Enjoy

[![Typewriter Gif](https://thibaultjanbeyer.github.io/tjb-WebComponent/typewriter.gif)](http://thibaultjanbeyer.com/)
