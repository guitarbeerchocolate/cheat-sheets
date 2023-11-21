# Vue.js Cheat Sheet

## Introduction to Vue.js

- **What is Vue.js?** Vue.js is a progressive JavaScript framework for building user interfaces. It's designed to be incrementally adoptable.

## Getting Started

- **Installation:** Include Vue.js in your HTML file using a CDN or install it via npm.

```
<!-- Include Vue.js from CDN -->
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
```

## Install Vue.js via npm

```
npm install vue
```

Creating a Vue Instance: Initialize a Vue instance to bind data and methods.

```
<div id="app">
  {{ message }}
</div>
```

```
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello, Vue.js!'
  }
});
```

## Vue Directives

v-bind: Bind HTML attributes to data.

```
<img v-bind:src="imageUrl">
```

v-model: Create two-way data binding for form inputs.

```
<input v-model="message">
```

v-for: Loop through an array and render elements.

```
<ul>
  <li v-for="item in items">{{ item }}</li>
</ul>
```

v-on: Bind event listeners to elements.

```
<button v-on:click="doSomething">Click me</button>
```

## Vue Components

Creating Components: Define reusable components.

```
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
});
```

Using Components: Use components in templates.

```
<todo-item v-for="item in todos" v-bind:todo="item"></todo-item>
```

## Vue Lifecycle Hooks

beforeCreate: Executed before an instance is initialized.

created: Executed after an instance is created.

beforeMount: Executed before the template is compiled and inserted.

mounted: Executed after the instance is mounted.

beforeUpdate: Executed when data changes before re-rendering.

updated: Executed after a re-render when data changes.

beforeDestroy: Executed before an instance is destroyed.

destroyed: Executed after an instance is destroyed.

## Vue Router

Installation: Install Vue Router using npm.

```
npm install vue-router
```

Router Configuration: Define routes and use the <router-view> component.

```
const routes = [
  { path: '/', component: Home },
  { path: '/about', component: About }
];

const router = new VueRouter({
  routes
});
```

Router Links: Use <router-link> for navigation.

```
<router-link to="/">Home</router-link>
<router-link to="/about">About</router-link>
```

## Vue CLI

Installation: Install Vue CLI globally.

```
npm install -g @vue/cli
```

Create a Project: Create a new Vue.js project.

```
vue create my-project
```

Development Server: Start a development server.

```
cd my-project
npm run serve
```

## Vue Resources

Vue.js Official Documentation: Comprehensive documentation and guides.

Vue Router Documentation: Vue Router documentation.

Vue CLI Documentation: Vue CLI documentation.
