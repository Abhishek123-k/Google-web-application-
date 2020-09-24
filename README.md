# Google-web-application-Getting started
Firstly, install the package:

npm install --save styled-jsx
Next, add styled-jsx/babel to plugins in your babel configuration:

{
  "plugins": [
    "styled-jsx/babel"
  ]
}
Now add <style jsx> to your code and fill it with CSS:

export default () => (
  <div>
    <p>only this paragraph will get the style :)</p>

    { /* you can include <Component />s here that include
         other <p>s that don't get unexpected styles! */ }

    <style jsx>{`
      p {
        color: white;
      }
    `}</style>
  </div>
)
Features
Full CSS support, no tradeoffs in power
Runtime size of just 3kb (gzipped, from 12kb)
Complete isolation: Selectors, animations, keyframes
Built-in CSS vendor prefixing
Very fast, minimal and efficient transpilation (see below)
High-performance runtime-CSS-injection when not server-rendering
Future-proof: Equivalent to server-renderable "Shadow CSS"
Source maps support
Dynamic styles and themes support
CSS Preprocessing via Plugins
How It Works
The example above transpiles to the following:

import _JSXStyle from 'styled-jsx/style'

export default () => (
  <div className="jsx-123">
    <p className="jsx-123">only this paragraph will get the style :)</p>
    <_JSXStyle id="123">{`p.jsx-123 {color: red;}`}</_JSXStyle>
  </div>
)
Why It Works Like This
Unique classnames give us style encapsulation and _JSXStyle is heavily optimized for:

Injecting styles upon render
Only injecting a certain component's style once (even if the component is included multiple times)
Removing unused styles
Keeping track of styles for server-side rendering
Targeting The Root
Notice that the outer <div> from the example above also gets a jsx-123 classname. We do this so that you can target the "root" element, in the same manner that :host works with Shadow DOM.

If you want to target only the host, we suggest you use a class:

export default () => (
  <div className="root">
    <style jsx>{`
      .root {
        color: white;
      }
    `}</style>
  </div>
)
