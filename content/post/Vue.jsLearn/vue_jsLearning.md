# Creating a New Vue Project
```bash
npm create vue@latest
```
Then you'll have many options to choose the current project's configuration, such as whether to support TypeScript, whether to support vue-router, etc. After making your selections, the project will be automatically created.
Then follow the prompts for package management and run the project:
```bash
cd <your-project-name>
npm install
npm run dev
```

## HTML
Learning common attributes: Master some commonly used HTML attributes that you'll frequently use in daily development. Common attributes include:
- class: Specifies the style class of an element.
- id: Sets a unique identifier for an element.
- href: Defines the target URL of a hyperlink.
- src: Used to specify the source file for images, scripts, or iframes.
- alt: Provides alternative text for images.

## Vue
In web development, I mainly learned the following attributes:
```html
<button @click="function_name"></button>
<h1 v-bind:class="variable_name">{{text(also can be change)}}<h1> //You can call a function by clicking a button, this function can change the value of variable_name, thus changing the class value and the style. The specific text content can also be changed. @ is the shorthand for v-on

```
So a key aspect of HTML is dynamics!
```html
<input v-bind:value="text" @input="onInput">
<!-- Where onInput is a function -->
function onInput() {
    text.value = e.target.value
} 
<!-- This way you can get the data from e -->
<!-- Similarly, we can write like this -->
<input v-model="text"> 
<!-- 等效于 -->
<input :value="text" @input="event => text = event.target.value">
```
You can also use v-if/v-else for toggling
```html
<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Oh no 😢</h1>
```

v-for to render the list
```html
<ul>
  <li v-for="item in items" :key="item.id">{{ item.text }}</li>
</ul>
```
`computed()` is a function that can be used to calculate the value of a variable, and it will be called when the variable is used.
```html
const FilteredTodos = computed(() => {
    if (hideCompleted.value){
        return todos.value.filter(todo => !todo.done)
    }else{
        return todos.value
    }
})
```
