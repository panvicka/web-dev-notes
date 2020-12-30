# CSS trickery

## Update \*CSS Property\* with variables to prevent overwriting

When trying to update _transform_ for an another selector, the original _transform_ properties are overwritten

```css
li {
  transform: rotate(-2deg) scale(4);
}
li:nth-child(1) {
  transform: rotate(-1deg);
  /* oh no, the scale(4) is no longer there! */
}
```

Save the stuff inside a variable and only update the variable.

```css
li {
  --rotate: -2deg;
  transform: rotate(var(--rotate) scale(4));
  order: 1;
}

li:nth-child(1) {
  --rotate: 1deg;
  /*rotate will be changed but it stays scaled!*/
}
```

## font-size: clamp()

font is scaling up/down with browser size, for example minimal size 0.9rem, maximal size 2.2rem, preferred 1vw+1rem

```css
font-size: clamp(0.9rem, 1vw + 1rem, 2.2rem);
```

## CSS subgrid

- children of element that is part of the grid cant be affected with `grid-auto-rows: auto auto 500px;` and this is causing items
  inside an element that is displayed in grid to be missaligned (see picture).
- can be solved with using `grid-template-rows: subgrid` on the desired element
- **is not supported in Chrome yet (30.12.2020)!!!**

![alt text](assets/css-grid-problem.PNG)

## fallback css in case that a browser does not support it

- fallback CSS with `@supports not(*CSS line that may not be supported) {enter here alternative CSS}`
- also possible to do with varibles like this

```CSS
  @supports not (grid-template-rows: subgrid) {
    --rows: auto auto 1fr;
  }
  /* this syntax means: check if --rows has something in it otherwise use subgrid */
  grid-template-rows: var(--rows, subgrid); 

```
