<script setup lang="ts">
import { ref } from 'vue';

import InputField from './Forms/InputField.vue';

const inputField = ref('');
</script>

<template>
  <!-- Heading -->
  <section class="section">
    <h1 class="heading-1">Heading 1</h1>
    <h2 class="heading-2">Heading 2</h2>
    <h3 class="heading-3">Heading 3</h3>
  </section>

  <!-- Forms -->
  <section class="section">
    <InputField :value="inputField" />
  </section>
</template>
