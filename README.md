# Vue-Essentials-Cheat-Sheet 

### EXPRESSIONS

```vue
<div id="app">
<p>I have a {{ product }}</p>
<p>{{ product + 's' }}</p>
<p>{{ isWorking ? 'YES' : 'NO' }}</p> <p>{{ product.getSalePrice() }}</p>
</div>
```

### DIRECTIVES
Element inserted/removed based on truthiness:

```vue
<p -if="inStock">{{ product }}</p>
```
  
 ```vue
<p v-else-if="onSale">...</p>
 <p v-else>...</p>
```

Toggles the display: none CSS property:
```vue
<p v-show="showProductDetails">...</p>
```

Two-way data binding:
 ```vue
 <input v-model="firstName" >
```

 ```vue
 v-model.lazy="..." Syncs input after change event
   ```

 ```vue
 v-model.number="..." Always returns a number
```
 
 ```vue
v-model.trim="..." Strips whitespace
```

### LIST RENDERING
key always recommended
 ```vue
<li v-for="item in items" :key="item.id"> {{ item }}
```

To access the position in the array:
 ```vue
<li v-for="(item, index) in items">..
```

To iterate through objects:
``` vue
<li v-for="(value, key) in object">...
```

Using v-for with a component:

```vue
<cart-product v-for="item in products" :product="item" :key="item.id">
```

### BINDING

```vue
<a v-bind:href="url">...</a>
```
True or false will add or remove attribute:
```vue
<button :disabled="isButtonDisabled”>...
```
If isActive is truthy, the class ‘active’ will appear:
```vue
<div :class="{ active: isActive }">...
```
Style color set to value of activeColor:
```vue
<div :style="{ color: activeColor }">
```

### ACTIONS / EVENTS
```vue
<button v-on:click="addToCart">...
```
shorthand

```vue
<button @click="addToCart">...
```
Arguments can be passed:
```vue
<button @click="addToCart(product)">..
```
To prevent default behavior (e.g. page reload):
```vue
<form @submit.prevent="addProduct">..
```
Only trigger once:
```vue
<img @mouseover.once="showImage">...
```
Stop all event propagation

```vue
.stop   
```

Only trigger if event.target is element itself
```vue
.self   
```

Keyboard entry example:
```vue
<input @keyup.enter="submit">
```
Call onCopy when control-c is pressed:
```vue
<input @keyup.ctrl.c="onCopy">
```
Key modifiers:
```vue
.tab
.up
.delete
.down 
.esc
.left
.space 
.right
.ctrl
.alt 
.shift 
.meta
```
Mouse modifiers:
```vue
.left
.right
.middle
```

### COMPONENT ANATOMY
```vue

Vue.component('my-component', {
    components: {
        // Components that can be used in the template
        ProductComponent, ReviewComponent
    },
    props: {
        // The parameters the component accepts
        message: String,
        product: Object,
        email: {
            type: String,
            required: true,
            default: '',
            validator: function (value) {
                // Should return true if value is valid
            }
        },
        data: function () {
            // must be a function
            return {
                firstName: "Manoj",
                lastName: "Kumar",
                age: 21
            }
        },
        computed: {
            // Return cached values until dependencies change
            fullName: function () {
                return this.firstName + ' ' + this.lastName
            }
        },
        watch: {
            // Called when firstName changes value
            firstName: function (value, oldValue) { ...
            }
        },
        methods: {},
        template '<span>{{ message }}</span>',
        // Can also use backticks for multi-line
    }
});

```

### CUSTOM EVENTS

Use props (above) to pass data into child components, custom events to pass data to parent elements.

Set listener on component, within its parent:

```vue
<button-counter v-on:incrementBy="incWithVal">
```

Inside parent component:
```vue
methods: {
incWithVal: function (toAdd) { ... }
}
```
Inside button-counter template:

Custom event name : incrementBy and 5 : Data sent up to parent 
```vue
this.$emit('incrementBy', 5)
```

### LIFECYCLE HOOKS
```vue
beforeCreate
created
beforeMount
mounted
beforeUpdate
updated
beforeDestroy
destroyed
```

### USING A SINGLE SLOT
Component template:
```html
<div>
      <h2>I'm a title</h2>
        <slot>
          Only displayed if no slot content
        </slot>
    </div>
```

Use of component with data for slot:
```vue
<my-component>
<p>This will go in the slot</p>
</my-component>

```

### MULTIPLE SLOTS
Component template:
```vue
<div class="container">
     <header>
       <slot name="header"></slot>
     </header>
     <main>
       <slot>Default content</slot>
     </main>
     <footer>
       <slot name="footer"></slot>
     </footer>
  </div>
```
Use of component with data for slot:
```vue
<app-layout>
<h1 slot="header">Page title</h1> <p>the main content.</p>
<p slot="footer">Contact info</p> </app-layout>
```

### LIBRARIES YOU SHOULD KNOW

` Vue CLI`

Command line interface for rapid Vue development.

`Vue Router`

Navigation for a Single-Page Application.

`Vue DevTools`

Browser extension for debugging Vue applications.

`Nuxt.js`

Library for server side rendering, code-splitting, hot-re- loading, static generation and more.