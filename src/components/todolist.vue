<template>
<div>
  <ul class="app__list app__list--tasks">
    <TodoItem
      v-for="task of searchTask"
      :key="task.id"
      v-bind:task="task"
      v-on:task-to-end="taskToEnd"
    />
  </ul>
</div>
</template>

<script>
import TodoItem from '@/components/todoitem'
export default {
  props: ['searchTask'],
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
    width: 100%;
    margin: 0;
    padding: 0;
    list-style: none;
  }
  .app__list--tasks {
    margin-bottom: 4px;
  }

  @media (min-width: 1440px) {
    .app__list {
      max-width: 574px;
    }
  }
</style>
