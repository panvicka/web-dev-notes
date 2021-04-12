# Vue notes

### Props definition
as an array
```js
export default {
    name: 'Header',
    props: ['title'],
}
```

or as an object 
```js
export default {
    name: 'Header',
    props: {
        title: String
       }
    }
}
```

or as an object with default value 
```js
export default {
    name: 'Header',
    props: {
        title: {
            type: String,
            default: "Hello World"
        }
    }
}
```