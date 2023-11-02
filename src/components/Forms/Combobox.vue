<script setup lang="ts">
import { ref, reactive, computed } from 'vue';
import { vOnClickOutside } from '@vueuse/components';

import { filterByText } from '@/Utils';

import Search from '@/Icons/Search.vue';

type ItemProp =
  | {
      id: number;
      title: string;
      value: string | number | boolean;
      [key: string]: any;
    }
  | string;

interface ComboboxProps {
  modelValue: ItemProp;
  items: ItemProp[];
  size?: string;
  titleKey?: string;
  valueKey?: string;
  error?: string;
}

const props = withDefaults(defineProps<ComboboxProps>(), {
  size: 'max-w-xs',
  titleKey: 'title',
  valueKey: 'value',
});

const emits = defineEmits(['update:modelValue']);

const dialog = ref<boolean>(false);
const input = ref<string>('');

const reset = () => {
  input.value = '';
  filters.search = '';
  dialog.value = false;
  emits('update:modelValue', '');
};

const update = (item: ItemProp) => {
  filters.search = '';
  dialog.value = false;

  // @ts-ignore
  input.value = item[props.titleKey] || item;

  emits('update:modelValue', item);
};

type FilterProp = {
  search: string;
};

const filters = reactive<FilterProp>({
  search: '',
});

const filteredItems = computed((): ItemProp[] => {
  let items: ItemProp[] = props.items as ItemProp[];

  if (filters.search) {
    items = filterByText(items, filters.search) as ItemProp[];
  }

  return items;
});

// __constructor
(() => {
  // @ts-ignore
  input.value = props.modelValue[props.titleKey] || props.modelValue;
})();
</script>

<template>
  <div :class="['relative', size]" v-on-click-outside="() => (dialog = false)">
    <!--  -->
    <div @click="dialog = !dialog" class="relative mb-1">
      <!--  -->
      <button
        @click.stop="reset"
        class="absolute inset-y-0 right-0 z-10 flex items-center px-2.5 hover:text-red-500 font-extrabold text-xs text-slate-500"
      >
        <span>&#x2715;</span>
      </button>

      <!-- // @ts-ignore -->
      <input
        :value="input"
        readonly
        placeholder="Please select an option"
        type="text"
        class="bg-gray-50 border text-sm rounded-lg focus:ring-1 focus:ring-indigo-500 focus:border-indigo-500 block w-full pr-10 p-2.5 focus-visible:outline-none cursor-pointer"
        :class="[error ? 'border-red-400' : 'border-gray-300']"
      />
    </div>

    <!--  -->
    <div
      v-if="dialog"
      :class="[
        'absolute border border-gray-300 rounded-lg bg-gray-50 shadow w-full',
        size,
      ]"
    >
      <ul class="max-h-[15rem] overflow-y-auto custom-scrollbar p-2.5">
        <!--  -->
        <li class="relative mb-1">
          <input
            v-model="filters.search"
            type="search"
            placeholder="Search..."
            class="!pl-10 focus:bg-white input"
          />
          <Search
            class="absolute inset-y-0 left-0 w-5 h-full pointer-events-none ml-2.5 text-slate-500"
          />
        </li>
        <li
          v-for="(item, index) in filteredItems"
          :key="item?.id || item[valueKey] || index"
          :class="[
            'p-2.5 hover:bg-gray-200 rounded-md truncate cursor-pointer',
            (item[valueKey] || item) === (modelValue[valueKey] || modelValue) &&
              'text-indigo-500',
          ]"
          @click="update(item)"
        >
          {{ item[titleKey] || item }}
        </li>
      </ul>
    </div>

    <p v-if="error" class="mt-2 ml-1 text-sm text-red-400">
      {{ error }}
    </p>
  </div>
</template>
