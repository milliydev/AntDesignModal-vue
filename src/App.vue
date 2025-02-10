<template>
  <div class="flex gap-4 p-4">
    <Modal
      v-model="FirstModalOpen"
      title="Payment Modal"
      :closable="false"
      saveBtnText="Confirm"
      cancelBtnText="Cancel"
    >
      <template #content>
        <div>
          <h1>Hello UIC Group</h1>
        </div>
      </template>
    </Modal>

    <ModalTwo
      v-model="SecondModalOpen"
      title="Payment Modal"
      size="large"
      :closable="false"
      saveBtnText="Confirm"
      cancelBtnText="Cancel"
    >
    <template #content>
        <div>
          <h1>Hello UIC Group</h1>
        </div>
      </template>
  </ModalTwo>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import Modal from "./components/Modal.vue";
import ModalTwo from "./components/ModalTwo.vue";

const FirstModalOpen = ref(false);
const SecondModalOpen = ref(false);
</script>
