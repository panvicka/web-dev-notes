# Module #2 Gatsby Basics

### Linking

- Use `<Link to='whatever'>Link Text</Link>` instead of `<a href='whatever>Link Text</a>`. Link tag renders out anchor link but it has all the JS stuff to use HTML5 push state. It only swappes the components but also adds the action into a browser history.

- `<button>` always needs a type even if the type is "button" like this `<button type="button">Click me</button>`

- if you need to change page programmatically (after submitting a form or something use `navigate`. With `{replace: true}` it is added to a browser history

```javascript
import { navigate } from "gatsby";
// navigate to a page after 2 seconds
setInterval(() => {
  navigate("/home", { replace: true });
}, 2000);
```

- layout: for stuff that is on all/a lof of pages like navigation, header, footer etc.

  - create `Layout.js component`
  - everything inside component tag is called children and you can find it in props
  - in `Layout.js` print all you need for every page + all the children like that

  ```javascript
  import React from "react";
  import Footer from "./Footer";
  import Nav from "./Nav";

  export default function Layout({ children }) {
    return (
      <div>
        <Nav />
        {children}
        <Footer />
      </div>
    );
  }
  ```

  - in yout individual pages wrap all content with `<Layout>content</Layout>`
  - but what if I dont wanna do that on every page? we can hook into wrap-page element hook with `gatsby-browser.js`
  - here you can call `wrapPageElement()`... available hooks here: <https://www.gatsbyjs.com/docs/reference/config-files/gatsby-browser/>

  ```javascript
  export function wrapPageElement({ element, props }) {
    return <Layout {...props}>{element}</Layout>;
  }
  ```

  - restart the build if you change anything in `gatsby-*****.js` files
  - `gatsby-browser.js` runs only in browsers (DUH!) but Gatsby has also server side rendering and we need also `gatsby-ssr.js` with the same code as `gatsby-browser.js`
