<template>
  <div>
    <Button type="primary" @click="$emit('update:modelValue', true)">Two Modal</Button>
    <Modal :open="modelValue" :bodyStyle="{ height: '400px' }" :width="computedWidth" :closable="closable"
      @cancel="handleCancel">
      <template #title>
        <div class="flex items-center justify-between bg-[#80C8F5] p-3 text-white text-lg">
          <span>{{ title }}</span>
        </div>
      </template>

      <slot name="content"></slot>

      <template #footer>
        <div class="flex justify-end gap-3 p-3">
          <Button type="text" class="text-dark bg-[#fff]" @click="handleCancel">
            {{ cancelBtnText }}
          </Button>
          <Button type="primary" html-type="submit" :loading="loading" @click="handleSave">
            {{ saveBtnText }}
          </Button>
        </div>
      </template>
    </Modal>
  </div>
</template>

<script lang="ts" setup>
import { computed, defineProps, defineEmits, ref } from "vue";
import { Modal, Button } from "ant-design-vue";

const props = defineProps({
  modelValue: Boolean,
  title: String,
  size: {
    type: String,
    default: "middle",
  },
  closable: {
    type: Boolean,
    default: true,
  },
  saveBtnText: {
    type: String,
    default: "Save",
  },
  cancelBtnText: {
    type: String,
    default: "Cancel",
  },
});

const emit = defineEmits(["update:modelValue"]);
const loading = ref(false);
const computedWidth = computed(() => {
  return props.size === "small" ? 350 : props.size === "large" ? 900 : 600;
});
const handleSave = () => {
  loading.value = true;
  setTimeout(() => {
    loading.value = false;
    emit("update:modelValue", false);
  }, 2000);
};
const handleCancel = () => {
  emit("update:modelValue", false);
};
</script>
