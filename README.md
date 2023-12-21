16-Video (Vite)

// take care of server
// hot reloding (mean when we change something in file then it automatically reload the changes and page)
// it have a build tool which make the website proformant.

// Run this command to install vue
npm init vue@latest

// there is new file routes which manage our links, history managements, scroll positions and routes etc

17-Video (Little Confusing Things)

// @ is alias which is define in jsconfig.js and vite config.js
// sometime or some ide doesnt recognised vite config .js
// @ alias refer to ./src/* to root directory.
// ./ is used for back or root
// ./../ is used for 2 backs.
import HelloWorld from '@/components/HelloWorld.vue'

// jsconfig.js
{
  "compilerOptions": {
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "exclude": ["node_modules", "dist"]
}

// vite.config.js
import { fileURLToPath, URL } from 'node:url'

import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [
    vue(),
  ],
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    }
  }
})

// there is a <RouterView /> component which already select those component view which we provide in index of the router. like in index we declared route and its name and then component. this RouterView will directly take that component.

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
        <RouterLink to="/contact">Contact</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

routes: [
    {
      path: '/',
      name: 'home',
      component: HomeView
    },
]

// we can use both conventions.

import TheWelcome from '../components/TheWelcome.vue'

// it can be used when when we use template or usong it globally so the browser can understand but here we compile our code then we can use it.
<the-welcome />
// common convention
<TheWelcome />

// this component initialize with The becuse it is used only one time in the code.

18-Video (Two Mental Leaps to Script Setup)

// There are two type of apis used in vue 3. which is based on structures and orginize the code.
// note that option apis have no inorrect some thing it is totally correct but it have its own strength and its not going away it will be in vue and and compoisition api have its own strength.
// first is option apis. 
// second is composition apis.
// 1. setup method.
// 2. setup attribute.

// when vue launched we only have options api.

Options API​
With Options API, we define a component's logic using an object of options such as data, methods, and mounted. Properties defined by options are exposed on this inside functions, which points to the component instance:

<script>
export default {
  data() {
    return {
      count: 0
    }
  },

  methods: {
    increment() {
      this.count++
    }
  },

  mounted() {
    console.log(`The initial count is ${this.count}.`)
  }
}
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>

<!-- Composition API​
With Composition API, we define a component's logic using imported API functions. In SFCs, Composition API is typically used with <script setup>. The setup attribute is a hint that makes Vue perform compile-time transforms that allow us to use Composition API with less boilerplate. For example, imports and top-level variables / functions declared in <script setup> are directly usable in the template.

Composition API is a set of APIs that allows us to author Vue components using imported functions instead of declaring options. It is an umbrella term that covers the following APIs:

Reactivity API, e.g. ref() and reactive(), that allows us to directly create reactive state, computed state, and watchers.

Lifecycle Hooks, e.g. onMounted() and onUnmounted(), that allow us to programmatically hook into the component lifecycle.

Dependency Injection, i.e. provide() and inject(), that allow us to leverage Vue's dependency injection system while using Reactivity APIs.

Composition API is a built-in feature of Vue 3 and Vue 2.7. For older Vue 2 versions, use the officially maintained @vue/composition-api plugin. In Vue 3, it is also primarily used together with the <script setup> syntax in Single-File Components. Here's a basic example of a component using Composition API:

Here is the same component, with the exact same template, but using Composition API and <script setup> instead: -->

<script setup>
import { ref, onMounted } from 'vue'

// reactive state
const count = ref(0)

// functions that mutate state and trigger updates
function increment() {
  count.value++
}

// lifecycle hooks
onMounted(() => {
  console.log(`The initial count is ${count.value}.`)
})
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>

<!-- Option APi method  -->

<script>
export default {

  // here we declare the data which automatically reactive.
  data() {
    return {
      count: 0
    }
  },
}
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>

<!-- Composition apis method with setup method -->

<script>
import React from 'react';
import { ref, onMounted } from 'vue'

export default {
  component: { React },

  setup() {

    // reactive state
    const count = ref(0)

    // here we declare the data which is not automatically reactive first of all we have to declare it and this is declared in upper code.
    // but we don't use it directly we have to use it with .value like we use it in mounted. but in template we can use it directly with only name. but in script we have to use it with name.value.
    return {
      count,
    };

    // lifecycle hooks first of all we have to inport in fro reactive api.
    onMounted(() => {
      console.log(`The initial count is ${count.value}.`)
    })
  },
}
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>

<!-- Composition apis method with setup attribute (when we use setup attribute we turn on the compiler macro make the code little bit friendly)
1. when we import something we can use it directly we dont neet to declare it in cooponent.
2. we dont need export default object.
3. user ref for reactive.
4. and import ref and mounted from composition api.
5. wehen we declare variable then it is is not not neceassry to return it or define it data in data like option api or using setup method in compositio api and it is not reactive so we will use ref to make it reactive.
6. can't use that variable directly by its name in script. we have to use it by its name.value but we can use it in template.
7. functions can be direct use by its name just write function behind it.
// make the reactivityTransform true then you dont neet ref to be imported and dont neet to use name.vlaue in script you can directly use it
plugins: [
    vue({
      reactivityTransform: true,
    }),
  ],
 -->

<script setup>
// reactivityTransform: true, if thre then dont neet to import it.
import { ref, onMounted } from 'vue'

// reactive state. if we are using script attribute then we dont have to declaared data like in options api or we dont have to return it like when we use setup method. just declare it here with ref api.

// reactivityTransform: false,
const count = ref(0)
// reactivityTransform: true,
const count = $ref(0)

function increment() {
  // reactivityTransform: false,
  count.value++

  // reactivityTransform: true,
  count++
}

// can also make method like this.
let increment = () => {
  count++
}

onMounted(() => {
  // reactivityTransform: false,
  console.log(`The initial count is ${count.value}.`)

  // reactivityTransform: true,
  console.log(`The initial count is ${count}.`)
})
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
</template>









