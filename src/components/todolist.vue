<template>
<div>
  <ul class="app__list app__list--tasks">
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
    taskToEnd (task) {
      this.$emit('task-to-end', task)
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
  .app__list--tasks {
    margin-bottom: 4px;
  }
</style>
