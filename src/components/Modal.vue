<template>
    <div>
      <Button type="primary" @click="openModal">Modal</Button>
      <Modal
        :open="isOpen"
        :width="computedWidth"
        :bodyStyle="{ height: '400px' }"
        :closable="false"
        @cancel="closeModal"
      >
        <template #title>   
          <div class="flex items-center justify-between bg-[#80C8F5] p-3 text-white text-lg">
            <span>{{ title }}</span>
            <Button type="text" class="text-dark bg-white cursor-pointer" @click="closeModal">
              Close
            </Button>
          </div>
        </template>
        <slot name="content"></slot>
        <template #footer>
          <form @submit="handleSubmit">
            <Button
              type="primary"
              html-type="submit"
              class="bg-blue-500 h-12 flex items-center w-[98%] px-4 justify-center mx-auto"
            >
              Attach a receipt
            </Button>
          </form>
        </template>
      </Modal>
    </div>
  </template>
  
  <script lang="ts" setup>
  import { defineProps, defineEmits, computed } from "vue";
  import { Button, Modal } from "ant-design-vue";
  
  const props = defineProps({
    modelValue: Boolean,
    title: String,
    size: {
      type: String,
      default: "middle", 
    },
  });
  
  const emit = defineEmits(["update:modelValue"]);
  const isOpen = computed({
    get: () => props.modelValue,
    set: (value) => emit("update:modelValue", value),
  });
  
  const computedWidth = computed(() => {
    if (props.size === "small") return 350;
    if (props.size === "large") return 900;
    return 600; 
  });
  
  const openModal = () => emit("update:modelValue", true);
  const closeModal = () => emit("update:modelValue", false);
  
  const handleSubmit = (event: Event) => {
    event.preventDefault();
    console.log("Form Submitted!");
    closeModal();
  };
  </script>
  
  <style>
  .ant-modal .ant-modal-content {
    padding: 0;
  }
  .ant-modal-footer {
    padding: 15px;
  }
  </style>
  