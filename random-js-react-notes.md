# Things that does not fit anywhere else

## react-icons

if you want to have a cool icon of for example pizze you can import it `import { MdLocalPizza as icon } from 'react-icons/md'` and just use it.
<https://react-icons.github.io/react-icons> It also has all the **Font Awesome** icons.

run this to install

```
npm install react-icons --save
```

## money formatter

```javascript
// create money formatter
const formatMoney = Intl.NumberFormat('en-CA', {
  style: 'currency',
  currency: 'CAD',
}).format;

// use it like this
formatMoney(value / 100);
```
