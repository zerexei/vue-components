<script setup lang="ts">
interface InputFieldProps {
  type?: string;
}

withDefaults(defineProps<InputFieldProps>(), {
  type: 'text',
});
</script>

<template>
  <input type="type" class="input" />
</template>
