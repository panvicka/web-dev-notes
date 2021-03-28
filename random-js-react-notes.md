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

## useMemo()
- resources [Learn useMemo In 10 Minutes](https://www.youtube.com/watch?v=THL1OPn72vo&ab_channel=WebDevSimplified) and [How To Use Memoization To Drastically Increase React Performance](https://blog.webdevsimplified.com/2020-05/memoization-in-react/)
- if you update state in React whole component is re-rendered
- in case there is a very slow function inside of the container it will be called as well - which is not necessary! 
- causes performance problems
- use `useMemo` for catching 
``` js
const result = useMemo(() => {
  return slowFunction(a)
}, [a])
```
- if the `a` doesn't change we do not need to run the function on component re-render 
- do not memoizate everything, it gives memory overhead 
- another use would be to compare objects 
- when re-rendering component every object (for example object generating styles) is re-created, gets a new ID and even if the name did not changed it can not be accessed by the name anymore

This is not optimal, the `"Color schema changed"` will be logged after every component re-render even if the color schema was not changed 
```js
const myStyle = {
  backgroundColor: blue? 'blue' : 'white'
}

useEffect(() => {
  console.log("Color schema changed")
}, [myStyle])

```

With `useMemo()` the `"Color schema changed"` is only printed out when the myStyle changes (which means only when `blue` variable changes). It ic cached and it wont be called unless there is an actual change happening. 
```js
const myStyle = useMemo( () => {
  return backgroundColor: blue? 'blue' : 'white'
  }
}, [blue]);

useEffect(() => {
  console.log("Color schema changed")
}, [myStyle])

```
## ENV variables in React App
- you do not need to install anything extra if you want to use environmental variables in your React App
- make a new file `.env` in ROOT directory
- your variables must start with `REACT_APP_`
- do not use any quotes, semicolons or commas, example: 
```
REACT_APP_AUTH0_DOMAIN=dev.secret.com
REACT_APP_AUTH0_CLIENT_ID=Qu1XXXXXXXXXXXXXXXXXXXoA2K
```
- access variable like this `const clientId = process.env.REACT_APP_AUTH0_CLIENT_ID;`
- **you have to restart the app after every change in .env** 

## Auth0 returns 400 when checking if user is logged in or not
- I followed <https://auth0.com/blog/complete-guide-to-react-user-authentication/#Set-Up-the-Auth0-React-SDK> 
- There is a part when we can get `isLoading` status 
``` js
  const { isLoading } = useAuth0();

  if (isLoading) {
    return <Loading />;
  }
```
- `isLoading` was still `TRUE` and after a minute or so i got `Failed to load resource: the server responded with a status of 400 () ` error 
- You need to add the `Allowed Web Origins` on your Auh0 setting page like this `http://localhost:3000` not like this `http://localhost:3000/`
 

 ## Image is not loading on canvas
 This easy code is not working because the `draw` function will be always faster then the image loading. Add event listener on `load` and draw the image after all needed resources are loaded. 
 ```javascript
 // this wont work
const image1 = new Image();
image1.src = 'image1.jpg';
ctx.drawImage(image1, 0, 0);

// this will
const image1 = new Image();
image1.src = 'image1.jpg';
image1.addEventListener('load', function() {
  ctx.drawImage(image1, 0, 0);
})
 ```

