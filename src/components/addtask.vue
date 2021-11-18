<template>
  <section class="app__section app__section--add">
    <h2 class="app__subtitle">Add todo</h2>
    <form class="form-add" aria-label="For added new task" @submit.prevent="onSubmit">
      <div class="form-add__input-wrapper">
        <label for="form-add" class="visually-hidden">Todo name</label>
        <input type="text" name="task-name" id="form-add" placeholder="Todo name" required v-model="title">
      </div>
      <button class="form-add__button button" type="submit" aria-label="Added task">
        <svg width="8" height="10" viewBox="0 0 22 22" fill="none" xmlns="http://www.w3.org/2000/svg">
          <rect x="10.0833" y="3.66663" width="1.83333" height="14.6667" fill="white" />
          <rect x="18.3333" y="10.0833" width="1.83333" height="14.6667" transform="rotate(90 18.3333 10.0833)"
            fill="white"/>
        </svg>
      </button>
    </form>
  </section>
</template>

<script>
export default {
  data () {
    return {
      title: ''
    }
  },
  methods: {
    onSubmit () {
      if (this.title.trim()) {
        const newTask = {
          title: this.title,
          completed: false
        }

        this.$emit('add-task', newTask)
        this.title = ''
      }
    }
  }
}
</script>

<style scoped>
  .visually-hidden {
    position: absolute;
    clip: rect(0, 0, 0, 0);
    width: 1px;
    height: 1px;
    margin: -1px;
    font-size: 0;
  }

  .app {
    font-family: "Roboto", "Arial", sans-serif;
    color: #000000;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  .app__section {
    background-color: #ededed;
  }

  .app__section--add {
    max-width: 343px;
    margin-bottom: 40px;
    padding: 26px 23px;
  }

  .button {
    width: 46px;
    height: 41px;
    border: 0;
    border-radius: 5px;
    background-color: #00b3db;
    cursor: pointer;
  }

  .form-add {
    display: grid;
    align-items: center;
  }

  .form-add__input-wrapper {
    grid-row: 1/2;
    grid-column: 1/2;
    max-width: 297px;
  }

  .form-add__input-wrapper input {
    width: 100%;
    padding: 18px 0 17px 18px;
    border: 0;
    border-radius: 5px;
  }

  .form-add__button {
    grid-row: 1/2;
    grid-column: 1/2;
    justify-self: end;
    margin-right: 60px;
  }

  @media (min-width: 768px) {
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
