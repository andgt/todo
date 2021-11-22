<template>
  <div class="app container" id="app">
    <h1 class="app__title">Todo App</h1>
    <div class="main__block">
      <AddTask
        @add-task="addTask"
      />
      <div class="app__section--inner">
        <section class="app__section app__section--main">
          <div class="app__list-header">
            <h2 class="app__subtitle app__subtitle--list">My todos</h2>
            <form class="form">
              <label class="visually-hidden" for="search-form">Search</label>
              <input class="form__input-search" type="search" name="search" id="search-form" placeholder="Search" v-model="searchItem">
            </form>
          </div>
          <FilterTasks
            v-bind:filterInputs="filterInputs"
            @filtering="filtering"
          />
          <Todolist
            v-show="chooseTasks==='true'"
            v-if="tasks.length"
            v-bind:searchTask="searchTask "
            @task-to-end="taskToEnd"
          />
          <p class="app__no-task" v-else>No active tasks</p>
          <DeletedTasks
            v-bind:deleted="deleted"
            v-show="chooseDeleted==='true'"
          />
        </section>
      </div>
    </div>
  </div>
</template>

<script>
import AddTask from '@/components/addtask'
import FilterTasks from '@/components/filtertasks'
import Todolist from '@/components/todolist'
import DeletedTasks from '@/components/deletedtasks'
export default {
  name: 'App',
  data () {
    return {
      chooseTasks: 'true',
      chooseDeleted: 'true',
      searchItem: '',
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
  computed: {
    searchTask () {
      const tasks = this.tasks
      return tasks.filter(item => item.title.toLowerCase().includes(this.searchItem.toLowerCase()))
    }
  },
  components: {
    AddTask,
    FilterTasks,
    Todolist,
    DeletedTasks
  }
}
</script>

<style>
  @import './assets/css/main.css';
</style>

<style scoped>
  .main__block {
    display: flex;
    flex-wrap: wrap;
    flex-direction: column;
    row-gap: 6px;
  }

  .app__section {
    background-color: #ededed;
  }

  .app__section--inner {
    position: relative;
    flex-grow: 1;
    height: 636px;
  }

  .app__section--inner::after {
    content: "";
    position: absolute;
    top: auto;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 57px;
    background: linear-gradient(0deg, #ededed 0%, rgba(237, 237, 237, 0) 164.04%);
  }

  .app__section--main {
    height: 636px;
    padding: 0 18px 38px 16px;
    overflow-y: scroll;
    scrollbar-color: #00b3db transparent;
    scrollbar-width: thin;
  }

  .app__title {
    margin: 94px 0 30px 0;
    font-weight: 700;
    font-size: 30px;
    line-height: 35px;
    text-align: left;
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

  .app__list-header {
    position: sticky;
    width: 100%;
    top: 0;
    left: 0;
    display: flex;
    flex-wrap: wrap;
    flex-direction: column;
    margin-bottom: 15px;
    padding: 38px 0 15px 0;
    background-color: #ededed;
    z-index: 200;
  }

  .form {
    display: flex;
    margin: 0 0 auto 0;
    border: 0;
    border-radius: 5px;
    background-color: #ffffff;
  }

  .form__input-search {
    flex-grow: 1;
    padding: 12px 20px 14px 27px;
    border: 0;
    border-radius: 5px;
  }

  .form__input-search::placeholder {
    font-weight: normal;
    font-size: 16px;
    line-height: 19px;
    color: rgba(0, 0, 0, 0.5);
  }

  @media (min-width: 768px) {
    .app {
      padding-bottom: 151px;
    }

    .main__block {
      display: flex;
      flex-wrap: wrap;
      flex-direction: row;
      column-gap: 10px;
      max-width: 1191px;
      margin: 0 auto;
    }

    .app__section--main {
      padding: 0 33px 58px 33px;
    }

    .app__title {
      margin: 126px 0 60px;
      font-size: 45px;
      line-height: 53px;
    }

    .app__list-header {
      flex-direction: row;
      justify-content: space-between;
      margin-bottom: 22px;
    }

    .app__subtitle--list {
      align-self: flex-end;
      margin-bottom: 0;
    }

    .form-add__input-wrapper {
      flex-grow: 1;
      max-width:456px;
    }

    .form {
      max-width: 161px;
    }

    .form__input-search {
      max-width: 161px;
    }
  }

  @media (min-width: 1440px) {
    .main__block {
      column-gap: 33px;
    }

    .app__section--main {
      max-width: 640px;
    }
  }
</style>
