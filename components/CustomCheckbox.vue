<template>
  <div>
    <div v-for="(box, index) in boxes" :key="index">
      <input
        type="checkbox"
        :checked="value"
        
      />
      <label>{{ box.label }}</label>
    </div>
  </div>
</template>

<script setup>
import { ref, watchEffect } from "vue";

const props = defineProps({
  modelValue: Boolean,
});

const emit = defineEmits(["update:modelValue"]);

let value = ref(props.modelValue);

watchEffect(() => {
  value.value = props.modelValue;
});

const updateValue = (newValue) => {
  emit("update:modelValue", newValue);
};

const boxes = [
  { label: "Checkbox 1" },
  { label: "Checkbox 2" },
  { label: "Checkbox 3" },
  { label: "Checkbox 4" },
  { label: "Checkbox 5" },
];
</script>
