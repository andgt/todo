<template>
<div>
  <ul class="app__list">
    <TodoItem
      v-for="task of tasks"
      :key="task.title"
      v-bind:task="task"
      v-on:task-to-end="taskToEnd"
    />
  </ul>
</div>
</template>

<script>
import TodoItem from '@/components/todoitem'
export default {
  props: ['tasks'],
  components: {
    TodoItem
  },
  methods: {
    taskToEnd (id) {
      this.$emit('task-to-end', id)
    }
  }
}
</script>

<style scoped>
  .app__list {
    display: flex;
    flex-direction: column;
    gap: 4px;
    max-width: 574px;
    margin: 0;
    padding: 0;
    list-style: none;
  }
</style>
