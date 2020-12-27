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
``` css
font-size: clamp(0.9rem, 1vw + 1rem, 2.2rem)
```
