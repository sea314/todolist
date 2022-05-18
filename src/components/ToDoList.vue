<script setup>
import { ref } from "vue";

const items = ref([
  { name: "やること1", isfinished: false, limit: "2022/12" },
  { name: "やること2", isfinished: false, limit: "2022/123213113131424" },
]);
const newItemName = ref("");
const newItemLimit = ref("");

const addItem = () => {
  if (newItemName.value.length > 0) {
    items.value.push({
      name: newItemName.value,
      isfinished: false,
      limit: newItemLimit.value,
    });
    newItemName.value = "";
    newItemLimit.value = "";
  }
};
</script>

<template>
  <div>ToDoList</div>
  未完了
  <div v-for="item in items" :key="item.name">
    <div v-if="!item.isfinished">
      <label>
        <input v-model="item.isfinished" type="checkbox" />
        {{ item.name }} 期限：{{ item.limit }}
      </label>
    </div>
  </div>
  完了
  <div v-for="item in items" :key="item.name">
    <div v-if="item.isfinished">
      <label>
        <input v-model="item.isfinished" type="checkbox" />
        {{ item.name }} 期限：{{ item.limit }}
      </label>
    </div>
  </div>

  <div>
    <label>
      名前
      <input v-model="newItemName" type="text" />
    </label>
    <label>
      期限
      <input v-model="newItemLimit" type="text" />
    </label>
    <button @click="addItem">add</button>
  </div>
</template>

<style>
.over500 {
  color: red;
}
</style>
