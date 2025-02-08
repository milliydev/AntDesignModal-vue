<template>
  <div>
    <Button type="primary" @click="$emit('update:modelValue', true)">Two Modal</Button>
    <Modal :open="modelValue" :bodyStyle="{ height: '400px' }" :closable="false" :width="900"
      @cancel="$emit('update:modelValue', false)">
      <template #title>
        <div class="flex items-center justify-between bg-[#80C8F5] p-3 text-white text-lg">
          <span>{{ HeaderTitle }}</span>
          <Form id="modalForm" :model="formState" layout="vertical" @finish="handleSubmit">
            <div class="flex justify-end gap-3">
              <Button type="text" class="text-dark bg-[#fff]" @click="$emit('update:modelValue', false)">
                Cancel
              </Button>
              <Button type="primary" html-type="submit" :loading="loading">
                Save
              </Button>
            </div>
          </Form>
        </div>

      </template>


      <template #footer></template>
    </Modal>
  </div>
</template>

<script lang="ts" setup>
import { reactive, ref, defineProps, defineEmits } from "vue";
import { Button, Modal, Form } from "ant-design-vue";

defineProps({
  modelValue: Boolean,
  HeaderTitle: String,
});

const emit = defineEmits(["update:modelValue"]);

const loading = ref(false);
const formState = reactive({
  name: "",
  email: "",
});

const handleSubmit = () => {
  loading.value = true;
  setTimeout(() => {
    console.log("Form submitted:", formState);
    loading.value = false;
    emit("update:modelValue", false);
  }, 2000);
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
