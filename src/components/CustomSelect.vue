<script setup lang="ts">
import { computed } from 'vue';

interface Props {
  label: string;
  modelValue: number;
  options: Array<{ id: number | string; name: string }>;
}
const props = defineProps<Props>();
const emit = defineEmits(['update:modelValue']);

const value = computed({
  get() {
    return props.modelValue;
  },
  set(value) {
    emit('update:modelValue', value);
  },
});
</script>

<template>
  <div class="select">
    <p class="select__label">
      {{ props.label }}
    </p>
    <select
      v-model="value"
      class="select__input"
    >
      <option
        v-for="option in props.options"
        :key="option.id"
        :value="option.id"
        class="select__option"
      >
        {{ option.name }}
      </option>
    </select>
  </div>
</template>

<style scoped>
.select__input {
  width: 288px;
  background-color: #f2f2f2;
  padding: 10px 16px;
  appearance: none;
  background-size: 20px 20px;
  background-image: url('../assets/svg/arrows-24-arrows-chevron-bottom.svg');
  background-position: right 16px center;
  background-size: 20px 20px;
  background-repeat: no-repeat;
  border: none;
  outline: none;
}
.select__label {
  color: #4f4f4f;
  font-size: 12px;
  font-style: normal;
  font-weight: 400;
  line-height: 150%;
  letter-spacing: 0.36px;
  margin-left: 16px;
}
.select_option {
  border: none;
}
</style>
