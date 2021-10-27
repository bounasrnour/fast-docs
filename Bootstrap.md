## Container

contrainer-fluid

## responsive images

img-responsive

# text stuff

text-center
text-primary
text-danger

## buttons

btn btn-default
btn-block	#will stretch to fill the entire horizontal space
btn btn-primary
btn btn-info
btn btn-danger

## Columns

def md (medium) * number of columns wide 
col-md-*
example
col-xs-4 (extra small size 4 wide)
well #gived the sense of depth 

## Font Awesome

```html
<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.8.1/css/all.css" integrity="sha384-50oBUHEmvpQ+1lW4y57PTFmhCaXp0ML5d60M1M7uH2+nqUivzIebhndOJK28anvf" crossorigin="anonymous">

```

used in the i tag 

<i class="fas fa-thumbs-up">

fas fa-info-circle
fas fa-trash
fa fa-paper-plane



# JQuery

all jquery functions starts with $

## functions

$("button").addClass("classname"); #selector

$(".well").addClass("classname") #by class

$("#target").addClass("classname") #by id

.removeClass("classname")
.css("color","red"); #css properties
.prop("disabled",true); #for html properties
.html("<em>hello</em>");
$("#target").html("texthere")

$("h2").html("text");

.remove();
.appendTo() #example $("#target2").appendTo("#right-well");

.clone().appendTo()

.parent()

.children()

$(".target:nth-child(2)").addClass("animated bounce");

$(".target:even").addClass("animated shake");

$(".target:odd").addClass("animated shake");

# SASS

One feature of Sass that's different than CSS is it uses variables. They are declared and set to store data, similar to JavaScript.

Sass, variables start with a `$` followed by the variable name.

```scss
$main-fonts: Arial, sans-serif;
$headings-color: green;
```

remember in sass you can nest css 

```scss
nav {
  background-color: red;

  ul {
    list-style: none;

    li {
      display: inline-block;
    }
  }
}
```

## usable css functions

use @mixin border-radius($parameter){

function css body;

}

now call it with @include border-radius(15px);

example

```css
@mixin border-radius($radius){
  -webkit-border-radius:$radius;
  -moz-border-radius:$radius;
  -ms-border-radius:$radius;
}
 div{
    @include border-radius(15px);
  }
```

## Control Flow

```css

@mixin border-stroke($val){
  @if $val == light{
    border: 1px solid black;
  }
  @else if $val == medium{
    border: 3px solid black;
  }
  @else if $val == heavy{
    border: 6px solid black;
  }
  @else{
    border: none;
  }
}
```

## For

```css

@for $j from 1 to 6{
  .text-#{$j} {font-size:$j * 15px;}
}
@for $i from 1 through 12 {
  .col-#{$i} { width: 100%/12 * $i; }
}
```

**to** does not include the end 
**through** includes the end 
// #{$var} to convert to text

## each

```css
$colors: (color1: blue, color2: red, color3: green);

@each $key, $color in $colors {
  .#{$color}-text {color: $color;}
}

@each $color in blue, red, green {
  .#{$color}-text {color: $color;}
}
```



## while

```css
$x: 1;
@while $x < 13 {
  .col-#{$x} { width: 100%/12 * $x;}
  $x: $x + 1;
}

$i:1;
@while $i < 6{
  .text-#{$i} {
    font-size: 15px * $i;
  }
  $i: $i + 1;
}
```

## partials

Partials are a separate files that holds segments of CSS code.
names for Partials starts with _ and saved with .scss extension
to import use @import 
Example
if all mixins are saved in a partial named "_mixins.scss" we import using @import 'mixins'

## exntend

```css
.panel{
  background-color: red;
  height: 70px;
  border: 2px solid green;
}

.big-panel{
  @extend .panel;
  width: 150px;
  font-size: 2em;
}
```

instead of copying properties use @extend

# React

to use javascript in react use {`this is js`} because react use jsx an extension os javascript 

## JSX elements

JSX must return one single element, the parent element should wrap all the other levels of nested elements 

## comment

{/* comment */}

## ReactDOM

```javascript
ReactDOM.render(JSX, document.getElementById('challenge-node'));
//refresher
ReactDOM.render<(componentToRender />, targetNode)
```

render to the DOM, first arg is the element you want to render, the second where we want to render the element , or the root node

## JSX vs HTML

difference is that we use className instead of class, onChange , onchange, onClick, onclick
we use camelCase 
in JSX all tags must have a closing tags, can be self closing or not 

## React Component

### Stateless component

use javascript function, this way component creates a stateless functional component.
receive data and render it but does not manage or track changes to that data

PS: must start with a capital letter 

```javascript
const DemoComponent = function() {
  return (
    <div className='customClass' />
  );
};
```

### Stateful Component

using the class 

```javascript
class Kitten extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <h1>Hi</h1>
    );
  }
}
```

### Notes

a typical React component is an ES6 `class` which extends `React.Component`. It has a render method that returns HTML (from JSX) or `null`

## Props

properties, or props , you can pass props to child components 

```jsx
const Welcome = (props) => <h1>Hello, {props.user}!</h1>
```

It is standard to call this value `props` and when dealing with stateless functional components, you basically consider it as an argument to a function which returns JSX. You can access the value of the argument in the function body. 

set props using 

```javascript
<MyComponent propsname=value />
```

## Default Props

```javascript
MyComponent.defaultProps = { location: 'San Francisco' }
ShoppingCart.defaultProps = {items:0};
```



## PropsType

```javasc
MyComponent.propTypes = { handleClick: PropTypes.func.isRequired }

```

PS we need to import PropTypes

```javascript
import PropTypes from 'prop-types';
```

## this.props

while using class based components use this.props to access the props

## States

state consists of any data the app needs to know about that can change over time. Update UI relatively to state change 
Declare the state in the class constructor 
it must be set to a javascript object

```javascript
this.state = {
  
}
```

## setState

 React provides a method for updating component `state` called `setState`. You call the `setState` method within your component class like so: `this.setState()`, passing in an object with key-value pairs. The keys are your state properties and the values are the updated state data. For instance, if we were storing a `username` in state and wanted to update it, it would look like this

```javascript
this.setState({
  username: 'Lewis'
});
```

PS : React expects you to never modify `state` directly, instead always use `this.setState()` when state changes occur

## bind this

One common way is to explicitly bind `this` in the constructor so `this` becomes bound to the class methods when the component is initialized. this.handleClick = this.handleClick.bind(this)` for its `handleClick` method in the constructor. Then, when you call a function like `this.setState()` within your class method, `this` refers to the class and will not be `undefined`.

## input

 `event.target.value`

```javascript
 handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
```



## forms

You also must call `event.preventDefault()` in the submit handler, to prevent the default form submit behavior which will refresh the web page.



