<template>
  <div class="flex gap-4 p-4">
    <Modal HeaderTitle="Attach payment" v-model="isFirstModalOpen">
      Content for first modal
    </Modal>
  <ModalTwo HeaderTitle="Attach payment" v-model="isSecondModalOpen" />
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import Modal from "./components/Modal.vue";
import ModalTwo from "./components/ModalTwo.vue";
const isFirstModalOpen = ref(false);
const isSecondModalOpen = ref(false);
</script>
