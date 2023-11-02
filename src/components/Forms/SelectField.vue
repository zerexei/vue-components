<script setup lang="ts">
type ItemProp =
  | {
      id: number;
      title: string;
      value: string | number | boolean;
      [key: string]: any;
    }
  | string;

interface SelectFieldProps {
  modelValue: ItemProp;
  items: ItemProp[];
  titleKey?: string;
  valueKey?: string;
  required?: boolean;
  error?: string;
}

withDefaults(defineProps<SelectFieldProps>(), {
  titleKey: 'title',
  valueKey: 'value',
  required: false,
});

const emits = defineEmits(['update:modelValue']);
</script>

<template>
  <div class="relative w-full">
    <!--  -->
    <select
      :value="modelValue[valueKey] || modelValue"
      @change="($event) => emits('update:modelValue', $event.target.value)"
      class="w-full px-4 py-2 pr-8 text-sm border rounded-lg outline-none appearance-none cursor-pointer"
      :required="required"
    >
      <option value="">Please select an option</option>
      <option
        v-for="(item, index) in items"
        :key="item?.id || item[valueKey] || index"
        :class="[
          (item[valueKey] || item) === (modelValue[valueKey] || modelValue) &&
            'text-indigo-500',
        ]"
        :value="item[valueKey] || item"
      >
        {{ item[titleKey] || item }}
      </option>
    </select>

    <!--  -->
    <div
      class="absolute inset-y-0 right-0 flex items-center px-2 pointer-events-none text-slate-500"
    >
      <svg
        class="w-4 h-4 fill-current"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 20 20"
      >
        <path
          d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
        />
      </svg>
    </div>
  </div>
</template>
