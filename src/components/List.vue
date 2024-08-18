<script setup>
const { items } = defineProps(["items"]);

const emit = defineEmits(["deleteItem"]);

const handleDelete = (item) => {
  emit("deleteItem", item);
};
</script>
<template>
  <ul>
    <li v-for="item of items" :key="item.name">
      <input type="checkbox" :id="item.name" v-model="item.completed" />
      <label :class="{ red: item.completed, green: !item.completed }">{{
        item.name
      }}</label>
      <button @click="handleDelete(item)">Delete</button>
    </li>
  </ul>
</template>