<script setup lang="ts">
withDefaults(
  defineProps<{
    modelValue: string;
    label: string;
    labelCss?: string;
  }>(),
  {
    labelCss: 'w-full ml-2 text-sm font-medium select-none',
  }
);

const emits = defineEmits(['update:modelValue']);
</script>

<template>
  <label class="flex items-center p-2 rounded cursor-pointer hover:bg-gray-100">
    <input
      type="checkbox"
      @change="(e) => emits('update:modelValue', String(e.target.checked))"
      :value="modelValue"
      class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500"
    />
    <span :class="labelCss">{{ label }}</span>
  </label>
</template>
