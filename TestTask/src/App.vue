<template>
  <div class="wrapper">
    <div class="top-blocks">
      <div class="selected-user">
        <div class="item" v-for="item in selectedUserItems" :key="item.id">{{ item.name }}</div>
        <div class="selected-count">selected: {{ selectedUserItems.length }} / 6</div>
      </div>
      <div class="selected-option">
        <div>SELECTED ITEM</div>
        <div v-if="selectedOptionItem" class="item">{{ selectedOptionItem.name }}</div>
      </div>
    </div>

    <div class="bottom-blocks">
      <div class="block">
        <div
          class="item"
          v-for="item in userItems"
          :key="item.id"
          :class="{ active: isUserItemSelected(item) }"
          @click="toggleUserItem(item)"
        >
          {{ item.name }}
        </div>
      </div>
      <div class="block">
        <div
          class="item"
          v-for="item in optionItems"
          :key="item.id"
          :class="{ active: selectedOptionItem?.id === item.id }"
          @click="selectOptionItem(item)"
        >
          {{ item.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const userItems = [
  { id: 1, name: 'Shoes 1' },
  { id: 2, name: 'Shoes 2' },
  { id: 3, name: 'Shoes 3' },
  { id: 4, name: 'Shoes 4' },
  { id: 5, name: 'T-shirt 1' },
  { id: 6, name: 'T-shirt 2' },
  { id: 7, name: 'T-shirt 3' },
  { id: 8, name: 'T-shirt 4' },
]

const optionItems = [
  { id: 11, name: 'Jacket 1' },
  { id: 12, name: 'Jacket 2' },
  { id: 13, name: 'Jacket 3' },
  { id: 14, name: 'Jacket 4' },
  { id: 15, name: 'Hoodie 1' },
  { id: 16, name: 'Hoodie 2' },
  { id: 17, name: 'Hoodie 3' },
  { id: 18, name: 'Hoodie 4' },
]

const selectedUserItems = ref([])
const selectedOptionItem = ref(null)

const toggleUserItem = (item) => {
  const index = selectedUserItems.value.findIndex(i => i.id === item.id)
  if (index >= 0) {
    selectedUserItems.value.splice(index, 1)
  } else if (selectedUserItems.value.length < 6) {
    selectedUserItems.value.push(item)
  }
}

const isUserItemSelected = (item) => {
  return selectedUserItems.value.some(i => i.id === item.id)
}

const selectOptionItem = (item) => {
  selectedOptionItem.value = item
}
</script>

<style scoped>
.wrapper {
  max-width: 900px;
  margin: auto;
  padding: 20px;
  font-family: sans-serif;
}
.top-blocks {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}
.selected-user, .selected-option {
  border: 2px solid black;
  padding: 10px;
  width: 45%;
  min-height: 80px;
}
.selected-count {
  margin-top: 10px;
}
.bottom-blocks {
  display: flex;
  justify-content: space-between;
}
.block {
  border: 2px solid black;
  padding: 10px;
  width: 45%;
  min-height: 300px;
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}
.item {
  padding: 5px 10px;
  border: 2px solid black;
  cursor: pointer;
  user-select: none;
}
.item.active {
  background-color: #797272;
}
</style>
