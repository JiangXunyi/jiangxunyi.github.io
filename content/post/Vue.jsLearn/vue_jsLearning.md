# Vue 新建项目
```bash
npm create vue@latest
```
然后就会有很多个选项选择当前项目的状态，比如是否支持typescript，是否支持vue-router等等。选择完之后就会自动创建项目。
然后按照提示进行pakage 的管理, 项目运行
```bash
cd <your-project-name>
npm install
npm run dev
```

## HTML
学习常用属性：掌握一些常用的 HTML 属性，这些属性你会在日常开发中经常用到。常用的属性包括：
- class：指定元素的样式类。
- id：为元素设置唯一标识符。
- href：定义超链接的目标 URL。
- src：用于指定图像、脚本或 iframe 的源文件。
- alt：为图像提供替代文本。

## Vue
在网页中我主要学习了以下一下属性
```html
<button @click="function_name"></button>
<h1 v-bind:class="variable_name">{{text(also can be change)}}<h1> //可以通过按按钮来call function，这个function可以来改变variable_name的值，从而改变class的值，也就是样式，具体文本内容都可以被改变, @就是v-on的简写

```
所以html的一个关键就是动态！
```html
<input v-bind:value="text" @input="onInput">
<!-- 其中onInput 是一个函数 -->
function onInput() {
    text.value = e.target.value
} 
<!-- 这样就可以获取e 中的数据， -->
<!-- 同样的，我们可以这么写 -->
<input v-model="text"> 
<!-- 等效于 -->
<input :value="text" @input="event => text = event.target.value">
```
还可以通过v-if/ v-else 来进行toggle
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
