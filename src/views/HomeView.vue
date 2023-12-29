<script setup>
  import { useStorage } from "./../../composables/useStorage";

  let food = useStorage('food', 'tacos');

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