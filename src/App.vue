<template>
  <div class="app" id="app">
    <h1 class="app__title">Todo App</h1>
    <AddTask
      @add-task="addTask"
    />
    <section class="app__section app__section--main">
      <h2 class="app__subtitle">My todos</h2>
      <TodoSearch/>
      <FilterTasks
        v-bind:filterInputs="filterInputs"
        @filtering="filtering"
      />
      <Todolist
        v-show="chooseTasks==='true'"
        v-if="tasks.length"
        v-bind:tasks="tasks "
        @task-to-end="taskToEnd"
      />
      <p class="app__no-task" v-else>No active tasks</p>
      <DeletedTasks
        v-bind:deleted="deleted"
        v-show="chooseDeleted==='true'"
      />
    </section>
  </div>
</template>

<script>
import AddTask from '@/components/addtask'
import TodoSearch from '@/components/todosearch'
import FilterTasks from '@/components/filtertasks'
import Todolist from '@/components/todolist'
import DeletedTasks from '@/components/deletedtasks'
export default {
  name: 'App',
  data () {
    return {
      chooseTasks: 'true',
      chooseDeleted: 'true',
      todos: [],
      tasks: [],
      deleted: [],
      filterInputs: [
        { title: 'Все', active: true },
        { title: 'Выполненные', active: false },
        { title: 'Невыполненные', active: false }
      ]
    }
  },
  mounted () {
    fetch('https://jsonplaceholder.typicode.com/todos')
      .then(response => response.json())
      .then(json => {
        this.todos = json
        localStorage.setItem('tasksLocal', JSON.stringify(this.todos))

        const dataActive = localStorage.getItem('tasksLocal')
        const dataDeleted = localStorage.getItem('deletedLocal')

        const parseActive = JSON.parse(dataActive)
        const parseDeleted = JSON.parse(dataDeleted)

        this.tasks = parseActive
        const tasksActive = this.tasks
        let count = 0

        for (let i = 0; i < tasksActive.length; i++) {
          if (dataDeleted) {
            this.deleted = parseDeleted
            const tasksDeleted = this.deleted
            for (let j = 0; j < tasksDeleted.length; j++) {
              if (tasksActive[i].id === tasksDeleted[j].id) {
                count--
                tasksActive[i].userId = count
              }
            }
          } else {
            return null
          }
        } return tasksActive
      })
  },
  beforeUpdate () {
    const tasks = this.tasks
    tasks.sort(function (a, b) {
      if (a.userId < b.userId) {
        return -1
      }
    })

    let countId = 0

    tasks.forEach(el => {
      el.completed = false

      if (el.userId < 0) {
        countId++
      }
    })

    tasks.splice(0, countId)
  },
  methods: {
    taskToEnd (task) {
      this.deleted.push(task)
      this.tasks = this.tasks.filter(el => el !== task)

      localStorage.setItem('deletedLocal', JSON.stringify(this.deleted))
      localStorage.setItem('tasksLocal', JSON.stringify(this.tasks))
    },
    addTask (task) {
      task.userId = 1
      this.tasks.push(task)
      localStorage.setItem('tasksLocal', JSON.stringify(this.tasks))
    },
    filtering (filterInput) {
      const inputs = this.filterInputs
      inputs.forEach(el => {
        el.active = false
      })
      filterInput.active = !filterInput.active

      if (filterInput.active === true) {
        if (filterInput.title === 'Выполненные') {
          this.chooseTasks = false
        } else {
          this.chooseTasks = 'true'
        }
      }

      if (filterInput.active === true) {
        if (filterInput.title === 'Невыполненные') {
          this.chooseDeleted = false
        } else {
          this.chooseDeleted = 'true'
        }
      }
    }
  },
  components: {
    AddTask,
    TodoSearch,
    FilterTasks,
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
  font-weight: 700;
  font-size: 30px;
  line-height: 35px;
  text-align: left;
  margin: 60px 0 0 0;
}

.app__subtitle {
  margin: 0 0 25px 0;
  font-weight: 700;
  font-size: 20px;
  line-height: 23px;
}

.app__no-task {
  margin: 0 0 30px 0;
  padding: 0 0 0 20px;
  font-size: 18px;
  line-height: 22px;
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
