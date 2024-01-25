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


<!-- 18-Video (From Mixins to Composables) -->

<!-- Special alert which we install on this command. -->
<!-- npm install sweetalert --save-dev -->

<script setup>
// import it like this:
import swal from 'sweetalert';

function flash(message) {
  // fisrt is title, second is message. and third is icon.
  swal('Success!', message, 'success');
}

// Mixins Code.
// just paste you script code of alert here.
// it works like traits code in php having different funcitons in one file and you can use it from averywhere.
// if you have large code than mixins is not clear. where my function is define. sp instead of it the most recommended approch is coposables.

import swal from 'sweetalert';

export default {
    methods: {
        flash(message) {
            return swal('Success!', message, 'success');
        }
    },
}

// Page code example

<script>
  import flash from './../../mixins/flash';

  export default {
    mixins: [flash],
  };

</script>

<!-- Composables Code. -->
<!-- just paste you script code of alert here. -->
<!-- its an alternate of mixins. -->
<!-- when you are making composable make this file with name use and then its name like useName -->

import swal from 'sweetalert';

export function useFlash() {
    function flash(message) {
        return swal('Success!', message, 'success');
    }

    return { flash };
}

<!-- component code with setup method  -->
<script>
import { useFlash } from './../../composables/useFlash.js';

export default {
  setup() {
    // Destructure the flash function from the composable
    let { flash } = useFlash();

    // Expose the flash function to the template
    return { flash };
  }
};

</script>

<!-- component code with setup attribute  -->

<script setup>

  import { useFlash } from './../../composables/useFlash.js';
  
  let { flash } = useFlash();

</script>

// 19-video (Composable Example: Local Storage)
// used composables with coposition apis and reactivity.
// use localStorages and vue wachers.
// if you are using SSR then server doesnt know local storage then you need to create your own apis for it else it work for browser.

// To store value in localStorage.
<script setup>
  import { ref, watch } from "vue";

  // get value from localStorage.
  let food = ref(localStorage.getItem("food"));
  let age = ref(localStorage.getItem("age"));

  function write(key, value) {
    // set value in localStorage.
    localStorage.setItem(key, val);
  }
</script>

<template>
  <main>
    <p>
      What is your favorite food? <input type="text" v-model="food" @input="write('food', food)">
    </p>
    <p>
      What is your favorite food? <input type="text" v-model="age" @input="write('age', age)">
    </p>
  </main>
</template>

// We can do it by watch method instead of @input="write('food', food)" b/c if the value is change automatically or from somewhere else then it will not changed.
// watch is looking evertime for this value when the value is changes it will run its funtionolity

<script setup>
  import { ref, watch } from "vue";

  let food = ref(localStorage.getItem("food"));
  let age = ref(localStorage.getItem("age"));

  // define like this. the first value is the name of data. the second oen is the value of data.
  watch(food, (val) => {
    write('food', val);
  })

  function write(key, val) {
    localStorage.setItem(key, val);
  }
</script>

<template>
  <main>
    <p>
      What is your favorite food? <input type="text" v-model="food">
    </p>
  </main>
</template>

 // if you want to store array or object make it json decode by JSON.stringify and the decode it by JSON.parse.

<!-- comopsable code -->
import { ref, watch } from "vue";

export function useStorage(key, data = null) {
  let storedData = read();

  if (storedData) {
    data = ref(storedData);
  } else {
    data = ref(data);

    write();
  }

  <!-- if you use obj then you need deep = true so that waatch can check deep into obj it will check value in obj which is changed if there is no deep then it will nor check deep it will just look into the first value which is work for normal data. if there is no need then you need to changes the entire object with the obj name. -->
  watch(data, write, { deep: true });

  function read() {
    return JSON.parse(localStorage.getItem(key));
  }

  function write() {
    if (data.value === null || data.value === '') {
      localStorage.removeItem(key);
    } else {
      localStorage.setItem(key, JSON.stringify(data.value));
    }
  }

  return data;
}

<!-- component code -->
 <script setup>
  import { useStorage } from "./../../composables/useStorage";

  let food = useStorage('food', 'tacos');

  // store obj in local storage.
  let obj = useStorage('obj', { one : 'one' });

  setTimeout(() => {
    obj.value.one = 'changed';
  }, 3000);

</script>

<template>
  <main>
    <p>
      What is your favorite food? <input type="text" v-model="food">
    </p>
  </main>
</template>

// 20-video (Refactor to defineProps and defineEmits)
// In text area when we click button tab then it didn't work but it select browser functionolity so will will make the tab button to work when click in text area.

// child compomemt code.
<script setup>

// props is used like this in composable api and if we want to take model value so we can taek it like this same as option api.
// that how we passed model data from parent compoennt to child compoennt.
defineProps({
  modelValue: String
});

// this decleration is must.
let emit = defineEmits(['update:modelValue']);

// e will give you total elemen template and the .target will give you the data.
function onTabPress(e) {
  let textarea = e.target;
  let val = textarea.value,
    start = textarea.selectionStart,
    end = textarea.selectionEnd;
  // select value then start position and then end position and put tab between them.
  textarea.value = val.substring(0, start) + "\t" + val.substring(end);
  // then move the cursot to the end of that value so you can write from that tabbable position. and i think this start + 1 is not necessary.
  textarea.selectionStart = textarea.selectionEnd = start + 1;
}
</script>
<template>
  // prevent is used to disable the default functionality of the browser when click on tab and it works on our way.
  @keydown.tab. tab is modifier for tab button and there also more like for enter, backspace etc.
  // display modelvalue prop like this. v-text="modelValue"
  // @keyup="emit('update:modelValue', $event.target.value)"
  // when key up it will update the model value of the parent compoenent. but we have to declare the emits like we declare it in upper portion.
  <textarea
    @keydown.tab.prevent="onTabPress"
    @keyup="emit('update:modelValue', $event.target.value)"
    v-text="modelValue" />
</template>

// Parent compomemt code.
<script setup>
  import TabbableTextarea from "./../components/TabbableTextarea.vue";
  import { ref } from "vue";
  let comment = ref('initial textarea value');
</script>

<template>
  <main>
    <form>
      <TabbableTextarea v-model="comment" style="width: 100%; height: 300px;" />
    </form>
  </main>
</template>

// if we want to take template of something element of html then pass it to ref like in the below code
// make ref varible of it and then you can use its template for every thing you want.
<script> 
  let textarea = ref(null)

  let t = textarea.value;

</script>

<TabbableTextarea ref="textarea" />

// 21-video (Dependency Injection With Provide and Inject)
// you can see here we have to pass a prop from parnt to child and then child to child. this is a problem when we have large amounts of components and pass data to last child. so we can do it easily by Dependency Injection With Provide and Inject.

// parent componnt
<script setup>
  import Quiz from "../components/Quiz.vue";
  import { ref } from "vue";

</script>

<template>
  <main>
    <Quiz myquiz="first quiz"></Quiz>
  </main>
</template>

// child component
<script setup>
import QuizFoot from './QuizFoot.vue'

defineProps({
  myquiz: {
    type: String,
    required: true
  }
})
</script>
<template>
  <QuizFoot :myquiz="myquiz"></QuizFoot>
</template>

// scond child component
<script setup>

const props = defineProps({
  myquiz: {
    type: String,
    required: true
  }
})

</script>

<template>
  {{ myquiz }}
</template>

// by Dependency Injection With Provide and Inject. import provide from vue and thn pass data to it then in last child component import inject from vue and collct that key which you provide.
// if the data is reactive. and you change it from nested child then it will change in parent component because it is ractive.
// If you did not want to change value from footer then make function in provide and inject that function in child and you can call that function to change value from it. b/c in large projects if you change value from child then it is very hard to find that from where it changed.

// parent componnt
<script setup>
  import Quiz from "../components/Quiz.vue";
  import { provide, ref } from "vue";

  let key = ref("first quiz za mara");

  provide('key', {
    key,
    changeName: () => key.value = 'Change Name'
  });

</script>

<template>
  <main>
    {{ key }}
    <Quiz></Quiz>
  </main>
</template>

// last child component
<script setup>
import { inject } from 'vue';

const { key, changeName }  = inject('key');

setTimeout(() => {
  changeName();
}, 3000);
</script>

<template>
  {{ key }}
</template>

// 21-video (Store State in an External File)
// we will discuss this.
// global state.
// prop drilling.
// ractivity.

// if we have data and we want access of that data in every component. then we want some global state that we store our data there and we have access of that data to all components.

// you can create many stores as you want . may be you can create for some specific user or for shopping cart
// you can make the store reactive then you can use it change it from the component. as like we have done it below.

// some of the road blocks.
// In bigger apps some time our states changes but we dont know from where it changes.
// and i want to hook in when data changes. may be store data in local storage.
// these are some bloacks in next video we will discuss this that how to overcome.

// quizStore code.
// reactive is a specially use for objects.
import { reactive } from "vue";

export let state = reactive({
  name: 'My Second Quiz',
  questions: []
});

// template code.
<template>
  <div>
    <h5>{{ state.name }}</h5>
  </div>

  <button @click="state.name = 'changed'">{{ state.name }}</button>
</template>

<script setup>
import {state} from "@/stores/quizStore";
</script>

// 22-video (Direct Mutation Concerns)
// we will discuss this.
// State
// Actions
// Mutating State

// we discuss globall state lately and now the variabe we store data is called state.
// the function based on this state is called action.

// Parent component.
<script setup>
import {counter} from "@/stores/counterStore";
</script>

<template>
  <div>
    <h1>{{ counter.count }}</h1>

    <button @click="counter.increment()">Increment</button>
  </div>
</template>

// store code.
import { reactive } from "vue";

export let counter = reactive({
  // state
  count: 0,

  // action
  increment() {
    if (this.count >= 10) {
      return;
    }

    this.count++;
  }
});

// 23-video (Say Hello to Pinia)

// we are discussig this.
// State
// Actions
// Getters

// we are using a dedicated tool for state management called pinia.
// there is a differnet tool vuex but this is official replacement of it called pinia.

// we will convert the last episode to pinia and then make a proper project in next episode.

// install pinia by this command
// npm install pinia
// then import in in main.js file and register it.
// Make stores folder in src.
// make a file with name start with capital letter and the followed by store. likw CounterStore.

import './assets/main.css'

import { createApp } from 'vue'
// here we import it.
import { createPinia } from 'pinia'
import App from './App.vue'
import router from './router'

const app = createApp(App)

app.use(router)
// here we register it.
app.use(createPinia())

app.mount('#app')

// state code.
//import define store from pinia.

import { defineStore } from "pinia";

// the name will be like it start with use and the file name like useCounterStore.
// then defien store and give a name to its first parameter.
// this name is use for dev tools or extention which we use in browser for pinia.s
// it is identifier.
// then export.

export let useCounterStore = defineStore('counter', {
  // data
  // understand it like data.
  state() {
    return {
      count: 5
    };
  },

  // methods
  // // understand it like functions.
  actions: {
    increment() {
      if (this.count < 10) {
        this.count++;
      }
    }
  },

  // computed
  // understand it like computed properties.
  getters: {
    remaining() {
      return 10 - this.count;
    }
  }
});

//main code.
<script setup>
// import the function from the store.
import {useCounterStore} from "@/stores/CounterStore";

// store it in variable.
let counter = useCounterStore();
</script>

<template>
  <div>
    // it is in state function but we can use it.
    // and we can change it from every where it is reactive.
    <h1>{{ counter.count }}</h1>

    <button
      @click="counter.increment()"
      :disabled="! counter.remaining"
    >Increment ({{ counter.remaining }} Remaining)</button>
  </div>
</template>

// 24-video (Code Organization)
//Extract Vue Components
// in this video we just set the design of the project and extaract component by simple props and now in next we will use state managment.

// here if we dont have data then we can use json file as a database like we make this
{
    "name": "Smily",
    "slot": 8,
    "members": [
        {
            "name": "test",
            "email": "test@example.com",
            "status": "Active"
        },
        {
            "name": "test",
            "email": "test@example.com",
            "status": "Active"
        },
        {
            "name": "test",
            "email": "test@example.com",
            "status": "Active"
        },
        {
            "name": "test",
            "email": "test@example.com",
            "status": "Active"
        },
        {
            "name": "test",
            "email": "test@example.com",
            "status": "Active"
        },
        {
            "name": "test",
            "email": "test@example.com",
            "status": "Active"
        }
    ]
}   

// we can pass concanicate dynamic value with string like this.
// both the ways are coorect

<img :src="`https://i.pravatar.cc/50?u=${email}`" alt="" class="rounded-xl">
<img :src="'https://i.pravatar.cc/50?u='+email" alt="" class="rounded-xl">














