<template>
  <div class="layout">
    <div class="row">
      <div class="container column">
        <div class="row">
          <BaseItem
            v-for="item in leftSelectedItems"
            :key="item.id"
            :item="item"
            @click="leftColumnItemClick(item.id)"
          />
        </div>
        <p>selected: {{ leftSelectedItemIds.length }} / {{ maxLeftSelectedAmount }}</p>
      </div>

      <BaseItem
        v-if="rightSelectedItem"
        :item="rightSelectedItem"
        @click="clearRightSelectedItem"
      />
      <div v-else class="container">EMPTY</div>
    </div>
    <div class="row">
      <div class="container">
        <BaseItem
          v-for="item in leftColumn"
          :key="item.id"
          :item="item"
          :is-selected="leftSelectedItemIds.includes(item.id)"
          @click="leftColumnItemClick(item.id)"
        />
      </div>
      <div class="container">
        <BaseItem
          v-for="item in rightColumn"
          :key="item.id"
          :item="item"
          :is-selected="rightSelectedItemId === item.id"
          @click="rightColumnClick(item.id)"
        />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import BaseItem from '@/components/BaseItem.vue';
import { computed, ref } from 'vue';
import type { BaseItemType } from '@/components/BaseItemType';

const leftSelectedItemIds = ref<number[]>([]);
const rightSelectedItemId = ref(-1);

const leftColumnItemClick = (id: number) => {
  const index = leftSelectedItemIds.value.indexOf(id);
  if (index !== -1) {
    leftSelectedItemIds.value.splice(index, 1);
    return;
  }

  if (leftSelectedItemIds.value.length < maxLeftSelectedAmount.value) {
    leftSelectedItemIds.value.push(id);
  }
};

const rightColumnClick = (id: number) => {
  if (rightSelectedItemId.value === id) {
    clearRightSelectedItem();
    return;
  }

  rightSelectedItemId.value = id;
};

const clearRightSelectedItem = () => {
  rightSelectedItemId.value = -1;
};

const leftSelectedItems = computed<BaseItemType[]>(() => {
  const foundItems = leftSelectedItemIds.value.map((id: number) =>
    leftColumn.find((item) => item.id === id)
  );
  return foundItems.filter((item): item is BaseItemType => item !== undefined);
});

const rightSelectedItem = computed<BaseItemType | undefined>(() =>
  rightSelectedItemId.value !== -1
    ? rightColumn.find((item) => item.id === rightSelectedItemId.value)
    : undefined
);

const maxLeftSelectedAmount = ref(6);

const leftColumn = [
  {
    id: 1,
    name: 'Shoes 1',
  },
  {
    id: 2,
    name: 'Shoes 2',
  },
  {
    id: 3,
    name: 'Shoes 3',
  },
  {
    id: 4,
    name: 'Shoes 4',
  },
  {
    id: 5,
    name: 'T-shirt 1',
  },
  {
    id: 6,
    name: 'T-shirt 2',
  },
  {
    id: 7,
    name: 'T-shirt 3',
  },
  {
    id: 8,
    name: 'T-shirt 4',
  },
];

const rightColumn = [
  {
    id: 11,
    name: 'Jacket 1',
  },
  {
    id: 12,
    name: 'Jacket 2',
  },
  {
    id: 13,
    name: 'Jacket 3',
  },
  {
    id: 14,
    name: 'Jacket 4',
  },
  {
    id: 15,
    name: 'Hoodie 1',
  },
  {
    id: 16,
    name: 'Hoodie 2',
  },
  {
    id: 17,
    name: 'Hoodie 3',
  },
  {
    id: 18,
    name: 'Hoodie 4',
  },
];
</script>

<style lang="scss">
.layout {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 20px;
  grid-gap: 20px;
}

.row {
  display: flex;
  justify-content: space-between;
  flex: 1;
  grid-gap: 20px;
}

.column {
  display: flex;
  flex-direction: column;
  grid-gap: 20px;
}

.container {
  display: flex;
  padding: 2rem;
  grid-gap: 12px;
  flex-wrap: wrap;
  align-items: center;

  border: 5px solid black;
}
</style>
