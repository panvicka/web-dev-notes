# CSS in Gatsby

### Global Styles
- dont just link CSS file, we want Gatsby to know about EVERYTHING (data, images, styles...)
- for styles Gatsby renders the critical CSS before the page content to prevent flashing up unstyled page and make loading faster (it doesnt do it in dev mode)
#### Ways to use CSS
- with just import `import 'src/styles/red-background.css;` and the page background color will be red
- styled components is the way to go :) 

### Global Styles
- global styles - applied globally (huh, dont say) to every element on page
- to delete all browser default setting use `normalize.css` <https://github.com/necolas/normalize.css>
- write all global styling into *GlobalStyles.js* with `styled-components`
- import all the svg and stuff, dont just reference it in css (if referenced, it goes to */static* folder and Gatsby doesnt know about stuff in there)
- selecting images that are not fully loaded 
    - can do that because Gatsby load images with all kind of smart features - loading small images when device is small, also when first loading the images it
    ships it as a base64 text (really really tiny picture of it that we can scale up and blur it or something)  
``` css
  .gatsby-image-wrapper img[src*=base64\\,] {
    image-rendering: -moz-crisp-edges;
    image-rendering: pixelated;
  }
```
### Nav links on current page
- Gatsby adds 'aria-current="page"' to the navigation link which leads to a site that is currently active - helfull for styling 
``` css
 a {  
    &[aria-current='page'] {
      color: var(--red);
    }
  }
```