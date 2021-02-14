<template>
  <div>
    <div v-for="item in todos" :key="item.id">
      <ToDoItem
        v-bind:toDoItem="item"
        v-on:del-todo="$emit('del-todo', item.id)"
      />
    </div>
  </div>
</template>
<script>
import ToDoItem from "./Todoitem";

export default {
  name: "to-do-list",
  props: ["todos"],
  components: {
    ToDoItem,
  },
};
</script>
<style scoped></style>
