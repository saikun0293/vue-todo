<template>
  <div class="to-do-item" v-bind:class="{ 'is-complete': toDoItem.completed }">
    <p>
      <input
        type="checkbox"
        name="tick"
        v-on:change="toggleStrike"
        :checked="toDoItem.completed ? true : false"
      />
      {{ toDoItem.title }}
      <button @click="$emit('del-todo')" class="del" type="submit">
        x
      </button>
    </p>
  </div>
</template>
<script>
export default {
  name: "to-do-item",
  props: ["toDoItem"],
  methods: {
    toggleStrike() {
      this.toDoItem.completed = !this.toDoItem.completed;
    },
  },
};
</script>
<style scoped>
.to-do-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}
.is-complete {
  text-decoration: line-through;
}
.del {
  border-radius: 50%;
  width: 20px;
  height: 20px;
  background-color: rgb(255, 38, 0);
  position: absolute;
  right: 20px;
  outline: none;
  text-decoration: none;
  color: white;
  border: none;
}
</style>
