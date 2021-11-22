<template>
  <section class="app__section app__section--add">
    <h2 class="app__subtitle">Add todo</h2>
    <form class="form-add" aria-label="For added new task" @submit.prevent="onSubmit">
      <div class="form-add__input-wrapper">
        <label for="form-add" class="visually-hidden">Todo name</label>
        <input class="form-add__input" type="text" name="task-name" id="form-add" placeholder="Todo name" required v-model="title">
      </div>
      <button class="form-add__button button" type="submit" aria-label="Added task">
        <svg width="12" height="12" viewBox="0 0 22 22" fill="none" xmlns="http://www.w3.org/2000/svg">
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
  .app {
    font-family: "Roboto", "Arial", sans-serif;
    color: #000000;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  .app__section {
    background-color: #ededed;
    border-radius: 6px;
  }

  .app__section--add {
    width: 100%;
    min-height: 157px;
    padding: 26px 23px;
  }

  .app__subtitle {
    margin: 0 0 27px 0;
    font-weight: 700;
    font-size: 20px;
    line-height: 23px;
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
    display: flex;
    flex-grow: 1;
  }

  .form-add__input {
    width: 100%;
    padding: 18px 0 17px 18px;
    font-weight: 400;
    border: 0;
    border-radius: 5px;
  }

  .form-add__input::placeholder {
    font-size: 16px;
    line-height: 19px;
    color: rgba(0, 0, 0, 0.5);
  }

  .form-add__button {
    grid-row: 1/2;
    grid-column: 1/2;
    justify-self: end;
    margin-right: 9px;
    transition: 0.3s ease;
  }

  .form-add__button:hover {
    transform: scale(1.02);
  }

  @media (min-width: 768px) {
    .app__section--add {
      max-width: 518px;
      min-height: 171px;
      margin-bottom: auto;
      padding: 32px 29px 31px 33px;
    }

    .app__subtitle {
      margin-bottom: 30px;
    }

    .form-add__input-wrapper {
      flex-grow: 1;
      max-width:456px;
    }

    .form-add__button {
      margin-right: 13px;
    }
  }
</style>
