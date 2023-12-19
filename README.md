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


