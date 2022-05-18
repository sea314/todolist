<script setup>
import { ref } from "vue";

const items = ref([
  { name: "やること1", isfinished: false, limit: "2022/12", priority: 0 },
  { name: "やること2", isfinished: false, limit: "2022/11", priority: 0 },
]);
const newItemName = ref("");
const newItemLimit = ref("");
const newItemPriority = ref(0);

const addItem = () => {
  if (newItemName.value.length > 0) {
    items.value.push({
      name: newItemName.value,
      isfinished: false,
      limit: newItemLimit.value,
      priority: newItemPriority.value,
    });
    newItemName.value = "";
    newItemLimit.value = "";
    newItemPriority.value = 0;
    items.value.sort((a, b) => b.priority - a.priority);
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
        {{ item.name }} 優先度：{{ item.priority }} 期限：{{ item.limit }}
      </label>
    </div>
  </div>
  完了
  <div v-for="item in items" :key="item.name">
    <div v-if="item.isfinished">
      <label>
        <input v-model="item.isfinished" type="checkbox" />
        {{ item.name }} 優先度：{{ item.priority }} 期限：{{ item.limit }}
      </label>
    </div>
  </div>

  <div>
    <label>
      名前
      <input v-model="newItemName" type="text" />
    </label>
    <label>
      優先度
      <input v-model="newItemPriority" type="number" />
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
