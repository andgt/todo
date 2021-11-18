<template>
  <div class="app" id="app">
    <h1 class="app__title">Todo App</h1>
    <AddTask
      @add-task="addTask"
    />
    <section class="app__section app__section--main">
      <h2 class="app__subtitle">My todos</h2>
      <TodoSearch/>
      <Breadcrumbs/>
      <Todolist
        v-bind:tasks="tasks "
        @task-to-end="taskToEnd"
      />
      <DeletedTasks
        v-bind:deleted="deleted"
      />
    </section>
  </div>
</template>

<script>
import AddTask from '@/components/addtask'
import TodoSearch from '@/components/todosearch'
import Breadcrumbs from '@/components/breadcrumbs'
import Todolist from '@/components/todolist'
import DeletedTasks from '@/components/deletedtasks'
export default {
  name: 'App',
  data () {
    return {
      tasks: [],
      deleted: []
    }
  },
  mounted () {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=10')
      .then(response => response.json())
      .then(json => {
        this.tasks = json
      })
  },
  beforeUpdate () {
    const tasks = this.tasks
    tasks.forEach(el => {
      el.completed = false
    })
  },
  methods: {
    taskToEnd (task) {
      this.deleted.push(task)
      this.tasks = this.tasks.filter(el => el !== task)
    },
    addTask (task) {
      task.id = this.tasks.length
      this.tasks.push(task)
      console.log(this.tasks)
    }
  },
  components: {
    AddTask,
    TodoSearch,
    Breadcrumbs,
    Todolist,
    DeletedTasks
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
  height: 636px;
  padding: 38px 18px 37px 16px;
  overflow-y: scroll;
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

  .app__section--add {
    max-width: 518px;
    padding: 32px 29px 31px 33px;
  }

  .form-add__input-wrapper {
    flex-grow: 1;
    max-width:456px;
  }
}
</style>
