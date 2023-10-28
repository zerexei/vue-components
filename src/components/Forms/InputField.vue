<script setup lang="ts">
interface InputFieldProps {
  type?: string;
  minLength?: string;
  maxLength?: string;
  required?: boolean;
  pattern?: string;
}

withDefaults(defineProps<InputFieldProps>(), {
  type: 'text',
  required: false,
});

const label = 'Email Address';
const icon = false;
const iconPosition = 'right';
const error = 'Email address is required';
</script>

<template>
  <form @submit.prevent="" class="flex flex-col">
    <button
      type="submit"
      class="py-1.5 px-3.5 rounded-md bg-indigo-500 text-white mb-6"
    >
      Submit
    </button>
    <div class="mb-4">
      <!-- InputField.vue -->
      <label class="label">Email Address</label>
      <input :type="type" class="input" />
    </div>

    <!-- <InputUrl v-if="type === 'URL'" />
    <InputField v-else /> -->

    <div class="mb-4">
      <!-- InputEmail.vue -->
      <label class="label">Email</label>
      <input
        type="email"
        class="input invalid:border-red-500 invalid:ring-red-500 valid:border-green-500"
        autocomplete="email"
      />
    </div>

    <!-- 

  icon:
  icon-position: left




 -->
    <div class="relative mb-6">
      <!-- Label -->
      <label v-if="label" class="label">{{ label }}</label>

      <!-- Icon -->
      <div
        v-if="icon"
        :class="[
          'absolute inset-y-0 flex items-center pointer-events-none',
          iconPosition === 'left' ? 'left-0 pl-3.5' : 'right-0 pr-3.5',
        ]"
      >
        <slot name="icon" />
      </div>

      <!-- Input -->
      <input
        :type="type"
        :required="required"
        :minLength="minLength"
        :maxlength="maxLength"
        :pattern="pattern"
        :class="[
          'bg-gray-50 border text-gray-900 text-sm rounded-lg focus:ring-1 focus:ring-indigo-500 block w-full p-2.5 focus-visible:outline-none focus:border-indigo-500',
          icon && (iconPosition === 'left' ? '!pl-10' : '!pr-10'),
          error ? 'border-red-400' : 'border-gray-300',
        ]"
        placeholder="name@flowbite.com"
      />

      <p v-if="error" class="mt-2 text-sm text-red-600">
        {{ error }}
      </p>
    </div>

    <div class="mb-4">
      <!-- InputPassword.vue -->
      <label class="label">Password</label>
      <input type="password" class="input" autocomplete="current-password" />
    </div>

    <div class="mb-4">
      <label class="label">Number</label>
      <input type="number" class="input" />
    </div>

    <div class="mb-4">
      <label class="label">URL</label>
      <input type="url" class="input" />
    </div>

    <div class="flex gap-4">
      <div class="flex-1 mb-4">
        <label class="label">Date</label>
        <input type="date" class="input" />
      </div>
      <div class="flex-1 mb-4">
        <label class="label">Date</label>
        <input type="date" class="input" />
      </div>
    </div>

    <div class="mb-4">
      <label class="label">Search</label>
      <input type="search" class="input" />
    </div>

    <div class="mb-4">
      <label class="label">File</label>
      <input type="file" accept=".doc,.docx" multiple class="input" />
    </div>

    <hr class="block my-6 border-b-2 border-b-slate-700/80" />

    <input type="number" inputmode="numeric" pattern="\d*" class="input" />

    <input type="checkbox" class="" />
    <input type="radio" class="" />
  </form>
</template>
