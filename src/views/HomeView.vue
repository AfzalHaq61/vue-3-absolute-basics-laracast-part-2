<template>
  <div>
    <button @click="showModal = true">model</button>

    <Teleport to="body">
      <Modal :show="showModal" @close="showModal = false">
          <template #default>
            <p class="text-gray-900">Need to add a new member to your team?</p>

            <form class="mt-6">
              <div class="flex gap-2">
                <input type="email" placeholder="Email Address..." class="flex-1">
                <button>Add</button>
              </div>
            </form>
          </template>
      </Modal>
    </Teleport>
    
  </div>
</template>

<script setup>
import Modal from "@/components/Modal.vue";
import { ref } from "vue";

let showModal = ref(false);
</script>