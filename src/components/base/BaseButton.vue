<template>
  <div class="base-button" :class="{ 'base-button--disabled': disabled }" @click="handleClick" :style="colorScheme">
    {{ text }}
  </div>
</template>
<script lang="ts" setup>
import { computed } from "vue";
import type { StyleValue } from "vue";

import { buttonColorSchemes } from "@/settings/colors";

const emit = defineEmits(["click"]);

const props = defineProps({
  text: String,
  colorScheme: { type: String, required: true },
  disabled: [Boolean, Number, String],
});

const colorScheme = computed<StyleValue>(() => {
  if (buttonColorSchemes[props.colorScheme]) {
    return buttonColorSchemes[props.colorScheme] as StyleValue;
  }

  return buttonColorSchemes.grey as StyleValue;
});

const handleClick = () => {
  if (!props.disabled) {
    emit("click");
  }
};
</script>
<style lang="scss" scoped>
@import "@/scss/variables";
.base-button {
  padding: 0 $px-10;
  height: $button-height-normal;
  cursor: pointer;
  border-radius: $px-5;
  text-transform: uppercase;
  display: flex;
  justify-content: center;
  align-items: center;

  &--disabled {
    background-color: #999 !important;
  }
}

.base-button:hover {
  opacity: 0.8;
}

.base-button--disabled:hover {
  opacity: 1 !important;
}
</style>
