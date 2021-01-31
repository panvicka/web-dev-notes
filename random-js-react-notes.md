# Things that does not fit anywhere else

## react-icons

if you want to have a cool icon of for example pizza you can import it `import { MdLocalPizza as icon } from 'react-icons/md'` and just use it.
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

## access component data in chrome console

- go to dev tools -> Components tab -> select the component you would like to inspect -> to go dev tools console -> write `$r`

## flat()

- takes array of arrays and puts it into one huge array
``` javascript
return pizzas.map((pizza) => pizza.toppings).flat();
```