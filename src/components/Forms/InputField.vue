<script setup lang="ts">
interface InputFieldProps {
  modelValue: string;

  label?: string;

  icon?: object;
  iconPosition?: string;

  type?: string;

  minLength?: string;
  maxLength?: string;
  required?: boolean;
  placeholder?: string;
  pattern?: string;

  error?: string;
}

withDefaults(defineProps<InputFieldProps>(), {
  type: 'text',
  required: false,
  iconPosition: 'left',
});

const emits = defineEmits(['update:modelValue']);
</script>

<template>
  <div class="w-full">
    <slot name="label">
      <label class="label">
        {{ label }}
      </label>
    </slot>

    <div class="relative">
      <!--  -->
      <div
        v-if="icon"
        class="absolute inset-y-0 flex items-center pointer-events-none"
        :class="[iconPosition === 'right' ? 'right-0 pr-3.5' : 'left-0 pl-3.5']"
      >
        <component :is="icon" class="w-5 h-5 text-slate-500"></component>
      </div>
      <!--  -->
      <input
        :value="modelValue"
        @input="(event) => emits('update:modelValue', event.target.value)"
        :type="type"
        class="input"
        :class="[
          icon && (iconPosition === 'right' ? '!pr-10' : '!pl-10'),
          error ? 'border-red-400' : 'border-gray-300',
        ]"
        :placeholder="placeholder"
        :required="required"
        :pattern="pattern"
        :maxlength="maxLength"
        :minlength="minLength"
      />
    </div>

    <!--  -->
    <p class="ml-1 -mt-px text-sm text-red-400">
      {{ error }}
    </p>
  </div>
</template>
