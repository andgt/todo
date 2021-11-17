<template>
  <div class="app" id="app">
    <h1 class="app__title">Todo App</h1>
    <section class="app__section app__section--main">
      <h2 class="app__subtitle">My todos</h2>
      <TodoSearch/>
      <Breadcrumbs/>
      <Todolist
        v-bind:tasks="tasks "
        @task-to-end="taskToEnd"
      />
    </section>
  </div>
</template>

<script>
import TodoSearch from '@/components/todosearch'
import Breadcrumbs from '@/components/breadcrumbs'
import Todolist from '@/components/todolist'
export default {
  name: 'App',
  data () {
    return {
      tasks: [
        { id: 1, title: 'Learn Vue', completed: false },
        { id: 2, title: 'Learn Webpack', completed: false },
        { id: 3, title: 'Read book', completed: false }
      ]
    }
  },
  methods: {
    taskToEnd (id) {
      this.tasks = this.tasks.filter(t => t.id !== id)
    }
  },
  components: {
    TodoSearch,
    Breadcrumbs,
    Todolist
  }
}
</script>

<style scoped>
.app {
  font-family: "Roboto", "Arial", sans-serif;
  color: #000000;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.app__section {
  background-color: #ededed;
}

.app__section--main {
  max-width: 640px;
  padding: 38px 18px 37px 16px;
}

.app__title {
  font-weight: 600;
  font-size: 30px;
  line-height: 35px;
  text-align: left;
  margin: 60px 0 0 0;
}

.app__subtitle {
  margin: 0 0 25px 0;
  font-weight: 600;
  font-size: 20px;
  line-height: 23px;
}

@media (min-width: 768px) {
  .app__title {
    font-size: 45px;
    line-height: 53px;
  }
}
</style>
