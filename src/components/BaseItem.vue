<template>
  <div class="base-item" :class="{ 'base-item--selected': isSelected }">
    {{ item.name }}
  </div>
</template>

<script setup lang="ts">
import type { BaseItemType } from '@/components/BaseItemType';

interface Props {
  item: BaseItemType;
  isSelected?: boolean;
}

defineProps<Props>();
</script>

<style scoped lang="scss">
.base-item {
  display: flex;
  align-items: center;
  border: 5px solid black;
  padding: 10px;
  white-space: nowrap;
  cursor: pointer;

  &--selected {
    background-color: lightgray;
  }
}
</style>
