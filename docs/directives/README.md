# Directives

The directives are the Vue-specific syntax elements that can be used in component templates.

## v-bind: Bind properties

Allows you to _bind_ an expression to the value of a property of an HTML element or component. Since this is the most commonly used directive, we usually use the shortened syntax `:property="value"`.

```html
<a v-bind:href="url">Link</a>

<a :href="url">Link</a>
<!-- shortened syntax -->
```

**Exercise: try to link the `src` and `width` attributes of the image**

```vue live
<template>
<h1>
    I {{likesVue ? "love" : "hate"}}
    <img src="" />
</h1>
</template>

<script>
export default {
  data(){
    return {
      likesVue: true,
      logo: 'https://vuejs.org/images/logo.png',
      logoWidth: 50
    }
  }
}
</script>
```

## Bind classes and styles

Several syntaxes are available to assign classes or CSS styles:

```html
<p :class="classAsString"></p>
<!-- "foo bar" -->
<p :class="classAsObject"></p>
<!-- { foo: true, bar: isBar } -->
<p :class="['foo', myOtherBarClass]"></p>
<p :class="{ foo: true, bar: isBar }"></p>

<p :style="styleAsString"></p>
<!-- "font-size: 48px" -->
<p :style="styleAsObject"></p>
<!-- { fontSize: "48px" } -->
<p :style="[baseStyles, overridingStyles]"></p>
<p :style="{ fontSize: size }"></p>
```

**Exercise: assign a class and a color to each ghost**

```vue live
<template>
<ol>
  <li>
    <span class="ghost">👻︎</span>
    I'm joyful and red
  </li>
  <li>
    <span class="ghost">👻︎</span>
    I'm jelly and green
  </li>
  <li>
    <span class="ghost">👻︎</span>
    I'm wobbly and blue
  </li>
</ol>
</template>

<script>
import "./ghosts.css";

export default {
  data(){
    return {
      ghost1: {
        anim: "joyful",
        style: "color: red"
      },
      ghost2: {
        anim: { jelly: true },
        style: { color: "green" }
      },
      ghost3: {
        isWobbly: true,
        isBlue: true
      }
    }
  }
}
</script>
```

## v-model: Forms and inputs

Allows you to bind the value of a form field to a component data item. It is a two-way binding: the variable is updated when the contents of the field change (typically by the user) and vice versa.

```html{3}
<label>
  What is your name ?
  <input v-model="name">
</label>

<p>Hello {{ name }} !</p>
```

<v-model-example />

**Exercise: use v-model on input, select, radio and checkbox**

**Composant : IceCreams.vue**
```vue live
<template>
<p>
   <svg version="1.1" class="ice-cream"
        v-for="n in +quantity" :key="n"
        :style="{ fill: flavour, height: size+'px' }"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        x="0px" y="0px"
        viewBox="0 0 113.2 244.1" enable-background="new 0 0 113.2 244.1" xml:space="preserve">
<g>
	<path class="ice-cream__cream" d="M21,101.7c-4.9,3.5-9.8,5.5-15.5,3.4c-4.7-1.8-6-5.1-2.3-8.3c3.6-3.2,3.7-6.6,4-10.9
		c1.4-16.7,12-26.6,26.6-33.7c-0.1,0.2,0.2-0.2,0.2-0.5c-0.9-13.5,2.4-18.3,15.5-22c6.6-1.9,13.3-3.2,19.8-5.4c3-1,6.7-3.2,7.6-5.7c1.1-2.9,0.3-7.5-1.5-9.9c-1.1-1.4-6,0.3-9.3,0.5c0.1-2.9,2.9-5.2,6.2-6.7c9.2-4.2,17.9-3,25.5,3.7c13.6,11.8,19.6,37.9,12.4,54.5c-1.1,2.5-2.5,5.3-4.6,7c-3.2,2.6-2.8,5-1.4,8.2c3.4,7.7,4.8,15.8,4,24.2c-0.8,8.2-4.3,14.7-12.2,19.1c1.7,5.3,3,10.9-3.6,14.2c-3.9,1.9-5.8,0.5-15.1-9.7c-13.5,9.2-26.8,6.1-35.7-8.2c-0.8-1.3-2.5-2.8-3.8-2.7C25.1,112.8,25.1,112.9,21,101.7z"/>
	<path class="ice-cream__cone" fill="#b38050" d="M29.7,151.5c3.2,6,6.1,11.5,9.4,17.7c-8,3.2-15.8,6.4-23.9,9.6c-2.7-5.1-5.4-9.8-7.6-14.7c-0.5-1,0.6-3.8,1.7-4.2C15.9,156.9,22.7,154.3,29.7,151.5z"/>
	<path class="ice-cream__cone" fill="#b38050" d="M15.9,180.3c8-3.2,15.8-6.3,23.8-9.5c0.1,0,1.8,3.2,2,3.5c0.6,1.1,1,2.2,1.6,3.2c0.8,1.4,1.6,2.9,2.3,4.3c0.4,0.7-0.1,1.2-0.5,1.8c-0.8,1.4-1.5,2.8-2.3,4.2c-0.5,1-0.8,1.5-1.8,2c-0.7,0.3-1.5,0.7-2.2,1.1c-0.9,0.5-1.8,1-2.7,1.6c-0.8,0.6-1.7,0.9-2.6,1.3c-2.9,1.2-5.8,2.3-8.6,3.5C22,191.6,19,186.1,15.9,180.3z"/>
	<path class="ice-cream__cone" fill="#b38050" d="M60.5,160.8c-6.7,2.7-13,5.2-19.5,7.8c-3.2-6-6.2-11.7-9.4-17.7c6.6-2.6,12.9-5.1,19.5-7.7C54.3,149.1,57.3,154.7,60.5,160.8z"/>
	<path class="ice-cream__cone" fill="#b38050" d="M33.7,128.5c0.6-0.2,1.2-0.4,1.8-0.6c1.6-0.7,3.1-1.3,4.7-1.9c0.3,0.9,0.6,1.4,1.2,1.9c1.8,1.7,4.3,2.8,5.8,4.7c0.2,0.3,0.3,0.6,0.5,0.9c0.7,1.8,1.4,3.5,2.1,5.3c0.2,0.6,0.5,1.2,0.2,1.8c-0.5,1-1.6,1.7-2.6,2c-5.3,2.2-10.6,4.4-16.4,6.7c-2.8-5.3-5.5-10.3-8.3-15.4c3-1.6,6-3.2,9.1-4.7C32.4,128.9,33,128.7,33.7,128.5z"/>
	<path class="ice-cream__cone" fill="#b38050" d="M13,227.8C9.5,221,6.2,214.9,2.6,208c7.3-3,14.2-5.8,21-8.6c5.3,6.7,5.3,6.7,0.6,13.1C20.7,217.4,17.1,222.2,13,227.8z"/>
	<path class="ice-cream__cone" fill="#b38050" d="M18,135.6c0.6-0.2,1.2-0.5,1.8-0.7c0.1,0,0.3-0.1,0.4,0c0.1,0,0.2,0.1,0.2,0.2c1.7,2.3,3.1,4.5,4.5,7.1c0.4,0.7,4,7.9,4.1,7.9c-7.2,2.9-14.1,5.6-21.7,8.7c0.3-0.1,0.2-3.5,0.2-3.9c0.1-1.3,0.2-2.6,0.2-3.9c0.2-2.6,0.3-5.2,0.6-7.8c0.1-0.9-0.1-2.7,0.5-3.4c0.6-0.8,2.3-1.2,3.2-1.6C14.1,137.2,16.1,136.4,18,135.6z"/>
	<path class="ice-cream__cone" fill="#b38050" d="M3.3,206c0.2-2.5,0.2-4.9,0.3-7.4c0.1-2.1,0.3-4.2,0.5-6.3c0.2-1.7,0.5-3.3,0.5-5c0-0.2,0-0.4,0.1-0.6c0.1-0.2,0.2-0.3,0.2-0.5c0-0.1,0-0.2,0-0.4c0-0.3,0.1-0.5,0.2-0.8c0.3-0.7,0.3-1.4,1.2-1.7c1.3-0.5,2.7-1.1,4-1.6c0.7-0.3,1.4-0.6,2.1-0.9c0.4-0.1,0.7-0.3,1.1-0.4c0.4-0.2,0.4-0.2,0.7,0.2c0.9,1.2,1.4,2.5,2.1,3.8c0.8,1.5,1.6,3,2.4,4.5c1.5,2.9,3.1,5.7,4.6,8.6c0,0.1,0.1,0.2,0.1,0.3C16.8,200.5,10.6,203,3.3,206z"/>
	<path class="ice-cream__cone" fill="#b38050" d="M62.3,160.7c-1.9-3.6-3.8-7.2-5.7-10.9c-1-1.8-1.9-3.6-2.9-5.4c-0.9-1.6-1.3-2.2,0.4-3.4c1.7-1.2,3.6-2.2,5.4-3.2c0.6-0.4,1.2-0.7,1.9-0.9c1.3-0.3,2.9,0,4.3-0.2c1.2-0.1,3-0.9,4.3-1c2.7-0.6,4.5-1.5,6.9-3.1c0.7,1.4,2.9,4,2.3,5.4c-0.7,1.7-2.4,3.1-3.5,4.6c-1.4,1.9-2.9,3.9-4.3,5.8C68.3,152.6,65.3,156.7,62.3,160.7z"/>
	<path class="ice-cream__cone" fill="#b38050" d="M33,126.4c-1.8,0.8-3.5,1.6-5.3,2.3c-1,0.5-2.1,0.9-3.1,1.4c-0.5,0.2-1.1,0.5-1.6,0.7c-0.3,0.1-1.1,0.7-1.5,0.6c-0.5-0.1-1-1.5-1.2-1.9c-0.4-0.8-0.8-1.5-1.2-2.3c-0.8-1.5-1.6-3.1-2.4-4.6c-1.6-3.1-3.2-6.3-4.7-9.5c-0.5-1.1,1.2-3.2,1.9-4.8c0.5,0.1,1,0.2,1.5,0.3c0.6,1.9,1.2,3.8,1.8,5.7c2.4,7.1,6.3,9.3,13.7,7.7c1.8-0.4,4-1.3,5.8-0.6c0.5,0.2,1,0.6,1.4,1.1c0.2,0.3,0.9,1.1,0.7,1.5c-0.1,0.4-1.3,0.7-1.6,0.8c-0.6,0.2-1.2,0.3-1.8,0.5c-0.4,0.2-0.9,0.4-1.3,0.6C33.6,126.1,33.3,126.3,33,126.4z"/>
	<path class="ice-cream__cone" fill="#b38050" d="M0,243.5c0.8-9.9,1.7-19.8,2.5-29.7c0.3-0.1,0.6-0.3,0.9-0.4c2.7,4.9,5.3,9.8,7.9,14.8c0.3,0.5,0.2,1.5-0.1,1.9c-3.4,4.7-6.9,9.3-10.3,14C0.6,243.9,0.3,243.7,0,243.5z"/>
	<path class="ice-cream__cone" fill="#b38050" d="M41.8,170c6.3-2.5,12.1-4.8,19.4-7.7c-5,6.8-9.1,12.4-13.6,18.6C45.4,176.9,43.7,173.6,41.8,170z"/>
	<path class="ice-cream__cone" fill="#b38050" d="M17.8,134.5c-1.8,0.7-3.5,1.4-5.3,2.2c-0.8,0.3-1.6,0.5-2.4,0.9c-0.4,0.2-0.8,0.5-1.2,0.8c-0.2-1,0.2-2,0.3-3c0.2-0.9,0.2-1.8,0.3-2.7c0.1-1.8,0.3-3.6,0.4-5.4c0.1-1.9,0.3-3.8,0.4-5.7c0.1-1,0.1-2,0.2-3.1c0-0.6,0.5-2.3,0.2-2.8c1.7,3.1,3.5,6.3,5.2,9.4c0.9,1.7,1.7,3.5,2.6,5.2c0.2,0.4,0.4,0.8,0.6,1.2c0.1,0.1,0.1,0.3,0.2,0.4c0.1,0.4,0.6,1.5,0.4,1.9C19.5,134,18.3,134.3,17.8,134.5z"/>
	<path class="ice-cream__cone" fill="#b38050" d="M13.7,179.4c-2.9,1.2-5.3,2.1-8.6,3.4c0.5-5.6,1-10.2,1.5-16.3C9.4,171.4,11.4,175.1,13.7,179.4z"/>
	<path class="ice-cream__cone" fill="#b38050" d="M29.3,205.5c-1.2-2.4-2.1-4.3-3.4-6.8c3.7-1.5,7-2.9,10.4-4.3c0.2,0.3,0.4,0.6,0.6,0.9C34.4,198.6,32,201.9,29.3,205.5z"/>
  <path class="ice-cream__napkin" v-if="napkin" fill="#cca" d="M0,243.5c0.8-9.9,1.7-19.8,5.5-89.7c0.3-0.1,0.6-0.3,56 10c0.3,0.5,0.2,1.5-0.1,1.9c-3.4,4.7-6.9,9.3-10.3,14C0.6,243.9,0.3,243.7,0,243.5z"/>
</g>
</svg>
</p>
</template>

<script>
export default {
    name: "IceCreams",
    props: ['quantity', 'size', 'flavour', 'napkin']
}
</script>
```
```vue live
<template>
<div id="icecream-store">
  <h1>Icecream store</h1>

  <label>Quantity: <input type="number"></label>

  <label>Size:
    <select>
      <option value="100">Small</option>
      <option value="150">Medium</option>
      <option value="200">Giant</option>
    </select>
  </label>

  <label>Flavour:</label>
  <label><input type="radio" name="flavour" value="#F3E5AB">Vanilla</label>
  <label><input type="radio" name="flavour" value="#5B2F00" />Chocolate</label>
  <label><input type="radio" name="flavour" value="#DE0934" />Strawberry</label>

  <label><input type="checkbox"> Napkin</label>

  <IceCreams :quantity="quantity" :flavour="flavour" :size="size" :napkin="napkin" />
</div>
</template>

<style>label { display: block }</style>

<script>
import IceCreams from "./IceCreams.vue";

export default {
  components: { IceCreams },
  data(){
    return {
      quantity: 1,
      flavour: "#5B2F00",
      size: 150,
      napkin: true
    }
  }
}
</script>
```

## v-if: Conditions

Allows you to insert or not an element according to a condition. If you want the element not to be removed from the DOM but just visually hidden in CSS, use `v-show` instead.

The `v-else-if` and`v-else` directives work in the same way as their JavaScript equivalent and depend on the `v-if` condition of the element directly preceding them.

```html{1,4,7,11}
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="isTypeB">
  B
</div>
<div v-else>
  Not A nor B
</div>

<template v-if="loaded">
  <h1>Use a template</h1>
  <p>to put a condition on a group of elements</p>
</template>
```

**Exercise: use v-if, v-else and v-else-if to alternate faces according to the temperature**

```vue live
<template>
<div>
  <input type="range" min="0" max="40" v-model="temperature" />
  {{ temperature }} °C
  <span>🥵</span>
  <span>🥶</span>
  <span>😀</span>
</div>
</template>

<script>
export default {
  data(){
    return { temperature: 20 }
  }
}
</script>
```

## v-for: Loops

Generates lists of elements by repeating a template by iteration on an iterable value: typically an `Array`, the list of properties of an object, or a fixed number of iterations.

The directive declares local variables representing each iterated element and their index, which can be used in the template within the element.

```html
<span v-for="n in 10">{{ n }} ; </span>

<!-- items: ["apple","kiwi","mango"] -->
<ul> <li v-for="item in items">{{ item }}</li> </ul>
```

<v-for-example-1 />

::: warning
In addition to the `v-for` directive, you should bind a `key` property to a value that uniquely identifies each element of the list (an identifier, a reference, etc.).

This is not mandatory but helps Vue to better understand the changes that occur on a list (additions, deletions, sorts, etc.) and optimize the transitions between two states of the list.
:::

```html{5}
<!-- todos: [ { label: 'See list transitions', done: false },
              { label: 'Learn Vue', done: false },
              { label: 'Use v-for', done: true }, ... ] -->
<ul>
<!-- the list is ordered by putting completed tasks at the end -->
  <li v-for="(todo, index) in todos_after_sort" :key="todo.label">
    <label>
      <input type="checkbox" v-model="todo.done">
      Task {{ index }}: {{todo.label}}
    </label>
    - <i>{{todo.done ? "DONE !": "in progress..."}}</i>
  </li>
</ul>
```

<v-for-example-2 />

::: tip
To repeat a group of elements, use `v-for` on a `<template>`tag
:::

**Exercise: use two v-for loops to display all the contents of the basket**

```vue live
<template>
<div id="basket">
  <h1>In my basket:</h1>
  <ul>
    <li>
      <span>🍌</span>
      <span>🍌</span>
    </li>
  </ul>
</div>
</template>

<style>
li { list-style: none; font-size: 2rem; }
</style>

<script>
export default {
  data() {
    return {
       basket: [
        { type: '🍌', quantity: 2 },
        { type: '🍎', quantity: 4 },
        { type: '🍒', quantity: 6 },
        { type: '🍉', quantity: 1 },
      ]
    }
  }
}
</script>
```

## v-on: Events

Define an action to take when an event occurs. It can be a DOM event (`click`, `mouseover`, `focus`, etc.) or a custom event emitted by a child component.

```html{1,5}
<button v-on:click="counter += 1"> Click here! </button> This button has been
clicked {{ counter }} times.

<!-- shortened syntax: @event -->
<button @click="resetCounter($event)"> Reset </button>
```

<v-on-example />

::: tip
You can use the `$event` variable as a reference to the captured event
:::

**Exercise: use events to add a monkey when clicking the button, and make them open their eyes on mouse hover**

```vue live
<template>
<div>
  <span v-for="monkey in monkeys">
    {{ monkey.hasEyesOpen ? '🙉' : '🙈' }}
  </span>
  <br/>
  <button>Add monkey</button>
</div>
</template>

<style>span { font-size: 2rem; }</style>

<script>
export default {
  data(){
    return {
      monkeys: [
        { hasEyesOpen: false }
      ]
    }
  },
  methods: {
    addMonkey(){
      this.monkeys.push({ hasEyesOpen: false })
    }
  }
}
</script>
```

### Modifiers

Modifiers are suffixes used to slightly change the behavior of some directives: for example stop the propagation of a captured event with `v-on`. For more information, please refer to [official documentation](https://vuejs.org/v2/guide/events.html#Event-Modifiers).

```html
<!-- the propagation of the click event will be stopped -->
<a @click.stop="onThis">...</a>

<!-- submitting the form will not reload the page -->
<form @submit.prevent="onSubmit">...</form>

<!-- modifiers can be chained -->
<a @click.stop.once="doSomethingOnce">...</a>

<!-- also available: .tab, .delete, .esc, .space... -->
<input @keypress.enter="submit" />
```

## Practical work: Film card

1. In the authentication form, add two variables `email` and`password` in the `data` attribute of the component and use the `v-model` directive on the email and password fields to bind them.
2. Add another `loggedIn` variable initially set to `false`, then use the `v-on` directive to set it to `true` when the form is submitted.
3. Change the default behavior of the `submit` event of the authentication form to avoid reloading the page.
4. In `LoginForm.vue`, add the following HTML under the authentication form :

```html
<ul class="films">
  <li class="film card">
    <img
      class="poster"
      src="https://m.media-amazon.com/images/M/MV5BMDdmZGU3NDQtY2E5My00ZTliLWIzOTUtMTY4ZGI1YjdiNjk3XkEyXkFqcGdeQXVyNTA4NzY1MzY@._V1_SX300.jpg"
    />
    <p class="title">
      Titanic
      <span class="rating">★★★★</span>
    </p>
    <dl>
      <dt>Release date</dt>
      <dd>07/01/1998</dd>
      <dt>Director</dt>
      <dd>James Cameron</dd>
      <dt>Actors</dt>
      <dd>Leonardo DiCaprio, Kate Winslet, Billy Zane, Kathy Bates</dd>
    </dl>
    <p class="plot">
      84 years later, a 100 year-old woman named Rose DeWitt Bukater tells the
      story to her granddaughter Lizzy Calvert, Brock Lovett, Lewis Bodine,
      Bobby Buell and Anatoly Mikailavich on the Keldysh about her life set in
      April 10th 1912, on a ship called Titanic when young Rose boards the
      departing ship with the upper-class passengers and her mother, Ruth DeWitt
      Bukater, and her fiancé, Caledon Hockley. Meanwhile, a drifter and artist
      named Jack Dawson and his best friend Fabrizio De Rossi win third-class
      tickets to the ship in a game. And she explains the whole story from
      departure until the death of Titanic on its first and last voyage April
      15th, 1912 at 2:20 in the morning.
    </p>
  </li>
</ul>
```

5. Use the `v-if` and `v-else` directives to display the authentication form and hide the films list when `loggedIn === false`, and vice versa.
6. Add the following variable in the `data` attribute of the component:

```js
films: [
  {
    title: "Titanic",
    released: "19 Dec 1997",
    director: "James Cameron",
    actors: "Leonardo DiCaprio, Kate Winslet, Billy Zane, Kathy Bates",
    poster:
      "https://m.media-amazon.com/images/M/MV5BMDdmZGU3NDQtY2E5My00ZTliLWIzOTUtMTY4ZGI1YjdiNjk3XkEyXkFqcGdeQXVyNTA4NzY1MzY@._V1_SX300.jpg",
    plot:
      "84 years later, a 100 year-old woman named Rose DeWitt Bukater tells the story to her granddaughter Lizzy Calvert, Brock Lovett, Lewis Bodine, Bobby Buell and Anatoly Mikailavich on the Keldysh about her life set in April 10th 1912, on a ship called Titanic when young Rose boards the departing ship with the upper-class passengers and her mother, Ruth DeWitt Bukater, and her fiancé, Caledon Hockley. Meanwhile, a drifter and artist named Jack Dawson and his best friend Fabrizio De Rossi win third-class tickets to the ship in a game. And she explains the whole story from departure until the death of Titanic on its first and last voyage April 15th, 1912 at 2:20 in the morning.",
    metascore: "75"
  },
  {
    title: "Blade Runner",
    released: "25 Jun 1982",
    director: "Ridley Scott",
    actors: "Harrison Ford, Rutger Hauer, Sean Young, Edward James Olmos",
    poster:
      "https://m.media-amazon.com/images/M/MV5BNzQzMzJhZTEtOWM4NS00MTdhLTg0YjgtMjM4MDRkZjUwZDBlXkEyXkFqcGdeQXVyNjU0OTQ0OTY@._V1_SX300.jpg",
    plot:
      "A blade runner must pursue and terminate four replicants who stole a ship in space, and have returned to Earth to find their creator.",
    metascore: "89"
  },
  {
    title: "The Shining",
    released: "13 Jun 1980",
    director: "Stanley Kubrick",
    actors: "Jack Nicholson, Shelley Duvall, Danny Lloyd, Scatman Crothers",
    poster:
      "https://m.media-amazon.com/images/M/MV5BZWFlYmY2MGEtZjVkYS00YzU4LTg0YjQtYzY1ZGE3NTA5NGQxXkEyXkFqcGdeQXVyMTQxNzMzNDI@._V1_SX300.jpg",
    plot:
      "A family heads to an isolated hotel for the winter where an evil spiritual presence influences the father into violence, while his psychic son sees horrific forebodings from both past and future.",
    metascore: "63"
  }
];
```

7. Using the `v-for` directive, repeat the `.film.card` element to display as many films as the `films` list.
8. Complete the card with data from each film using the directives and interpolation.
9. **Bonus:** the `metascore` property is a string that can take the value `"N/A"`, or a number between `"0"` and `"100"`. Use this property to display 1 to 5 stars next to each film title, when relevant.
