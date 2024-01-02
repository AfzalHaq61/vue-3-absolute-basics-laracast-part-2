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