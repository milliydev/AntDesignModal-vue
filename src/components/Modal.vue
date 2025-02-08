<template>
    <div>
        <Button type="primary" @click="$emit('update:modelValue', true)">Modal</Button>
        <Modal :visible="modelValue" :bodyStyle="{ height: '400px'}" :closable="false"
            @cancel="$emit('update:modelValue', false)">
            <template #title>
                <div class="flex items-center justify-between bg-[#80C8F5] p-3 text-white text-lg">
                    <span>{{ HeaderTitle }}</span>
                    <Button type="text" class="text-dark bg-white cursor-pointer"
                        @click="$emit('update:modelValue', false)">
                        Close
                    </Button>
                </div>
            </template>
            <template #footer>
                <form @submit="handleSubmit">
                    <Button type="primary" html-type="submit"
                        class="bg-blue-500 h-12 flex items-center w-[98%] px-4 justify-center mx-auto">
                        Attach a receipt
                    </Button>
                </form>
            </template>
            <template>
                <slot name="MainTitle">
                    Default title
                </slot>
            </template>
        </Modal>
    </div>
</template>
<script lang="ts" setup>
import { defineProps, defineEmits } from 'vue'
import { Button, Modal } from 'ant-design-vue'

defineProps({
    modelValue: Boolean,
    HeaderTitle: String
});
const emit = defineEmits(["update:modelValue"]);
const handleSubmit = (event: Event) => {
    event.preventDefault();
    console.log("Form Submitted!");
    emit("update:modelValue", false);
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
