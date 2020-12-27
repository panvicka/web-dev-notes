# Fancy programming words

## Declerative vs Imperative 
Declerative - Is like asking a friend to draw a picture of a house for you. You don't care how he does it. 
Imperative - Is your friend following a drawing tutorial which gives step by step directions. 

[Codeburst explanation I find usefull](https://codeburst.io/declarative-vs-imperative-programming-a8a7c93d9ad2#:~:text=Declarative%20programming%20is%20a%20programming,that%20change%20a%20program's%20state.&text=Declarative%20Programming%20is%20like%20asking%20your%20friend%20to%20draw%20a%20landscape)

**code example for imperative**
```javascript
const container = document.getElementById(‘container’);
const btn = document.createElement(‘button’);
btn.className = ‘btn red’;
btn.onclick = function(event) {
 if (this.classList.contains(‘red’)) {
   this.classList.remove(‘red’);
   this.classList.add(‘blue’);
 } else {
   this.classList.remove(‘blue’);
   this.classList.add(‘red’);
 }
};
container.appendChild(btn);
```

**code example for declarative**
- it doesn't touch the DOM element, it just says how it should be rendered
- in React you should not try to do direct DOM manipulation; if you feel like you have to you are (probably) doing something wrong  
```javascript
class Button extends React.Component{
  this.state = { color: 'red' }
  handleChange = () => {
    const color = this.state.color === 'red' ? 'blue' : 'red';
    this.setState({ color });
  }
  render() {
    return (<div>
      <button 
         className=`btn ${this.state.color}`
         onClick={this.handleChange}>
      </button>
    </div>);
  }
}
```

##  HTML5 PushState()
- use it to add stuff to user browser history and manipulate the content of the history stack
- push new with `history.pushState(state, title [, url])` and retrieve with `back(), froward(), go()`
- <https://developer.mozilla.org/en-US/docs/Web/API/History/pushState>
- example: Routing libraries used with for example React uses it when doing the `<Link>` navigation. The side is NOT reloaded, only the components are swapped (therefore it is really fast). But without the PushState user would not be able to navigate with the browser back/forward button which would be kinda annoying
(because user thinks he/she changed the page)

## React Fragment 
`<></>` renders out to nothing allowing us to return more then one element - prevents a div soup  


## Headless CMS
A headless content management system. It means only backend - there is no way to show the content, it is only accessible thru API. 

## Slug
"A slug is a unique string (typically a normalized version of title or other representative string), often used as part of a URL". *I like JS* becomes *i-like-js*