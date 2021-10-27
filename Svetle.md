#Svetle

In Svelte, an application is composed from one or more *components*. A component is a reusable self-contained block of code that encapsulates HTML, CSS and JavaScript that belong together, written into a `.svelte` file.

## Simple Component

```javascript
<script>
let name = 'world';
</script>
<h1>Hello {name}</h1>
```

Inside the curly braces, we can put any JavaScript we want. Try changing `name` to `name.toUpperCase()` for a shoutier greeting.

## HTML rendering

```javascript
<p>{@html string}</p>

```

## Reactivity

```javascript
$: console.log(`the count is ${count}`);

//can do rhis
$: {
	console.log(`the count is ${count}`);
	alert(`I SAID THE COUNT IS ${count}`);
}
//and this
$: if (count >= 10) {
	alert(`count is dangerously high!`);
	count = 9;
}
```

Reactivity helps us by running our code every time a value changes.

## Tricks

```javascript

function addNumber() {
	numbers.push(numbers.length + 1);
	numbers = numbers;
}
//equivalent to
function addNumber() {
	numbers = [...numbers, numbers.length + 1];
}
```

## Props

```javascript
<script>
	export let answer;
</script>
```

## Logic

```javascript
{#if user.loggedIn}
	<button on:click={toggle}>
		Log out
	</button>
{/if}

{#if !user.loggedIn}
	<button on:click={toggle}>
		Log in
	</button>
{/if}
 
 //another example
 {#if x > 10}
	<p>{x} is greater than 10</p>
{:else if 5 > x}
	<p>{x} is less than 5</p>
{:else}
	<p>{x} is between 5 and 10</p>
{/if}
```

A `#` character always indicates a *block opening* tag. A `/` character always indicates a *block closing* tag. A `:` character, as in `{:else}`, indicates a *block continuation* tag