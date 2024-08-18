<script setup>
import Header from "./components/Header.vue";
import List from "./components/List.vue";
import AddItem from "./components/AddItem.vue";
import { reactive, watch } from "vue";

const loadItems = () => {
  const getItems = localStorage.getItem("items");
  return getItems ? JSON.parse(getItems) : [];
};

const items = reactive(loadItems());

watch(items, () => {
  localStorage.setItem("items", JSON.stringify(items));
});

const handleItem = (item) => {
  items.push({ name: item, completed: false });
};

const deleteItem = (item) => {
  items.forEach((element, index) => {
    if (element === item) {
      items.splice(index, 1);
    }
  });
};
</script>

<template>
  <Header />
  <AddItem @item="handleItem" />
  <List :items @delete-item="deleteItem" />
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  background-color: #333;
  max-width: 700px;
  margin: 10px auto;
}
h1 {
  border: solid 2px white;
  text-align: center;
  color: papayawhip;
  margin: 20px auto;
}
ul {
  list-style-type: none;
  display: flex;
  flex-direction: column;
  gap: 15px;
}
li {
  display: grid;
  grid-template-columns: 1fr 4fr 1fr;
  margin-bottom: 20px;
  border: 2px solid gray;
  padding: 10px;
}

label {
  text-align: center;
  font-size: x-large;
}
button {
  background-color: red;
  text-align: center;
  font-size: large;
}
button:hover {
  transform: scale(110%);
}
input {
  text-align: center;
}
input:hover {
  transform: scale(110%);
}

.green {
  color: lightgreen;
}
.red {
  color: red;
  text-decoration: line-through;
}
.add {
  padding: 10px 80px;
  margin-bottom: 20px;
  border-style: none;
  border-radius: 20px;
}

.container {
  display: flex;
  justify-content: center;
}
</style>
