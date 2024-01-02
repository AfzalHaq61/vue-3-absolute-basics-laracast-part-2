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