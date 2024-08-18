<script setup>
import { ref } from "vue";

const item = ref("");

const emit = defineEmits(["item"]);

const emitItem = () => {
  if (item.value.length > 25) {
    alert("Limit is 25 characters :/");
    item.value = "";
  } else {
    emit("item", item.value);
    item.value = "";
  }
};
</script>
<template>
  <div class="container">
    <input
      class="add"
      type="text"
      v-model="item"
      placeholder="add an item...."
      @keydown.enter="emitItem"
    />
  </div>
</template>