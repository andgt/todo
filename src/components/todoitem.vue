<template>
  <li class="app__item">
    <div class="app__item-inner">
      <span class="app__item-title">{{task.title}}</span>
      <fieldset class="task__range-field">
        <input class="task__range" v-on:click="$emit('task-to-end', task)" v-on:change="task.completed = !task.completed" v-bind:class="{task__done: task.completed}" type="range" name="taskrange" min="1" max="2" step="1" value="1" aria-label="task-toggle">
      </fieldset>
    </div>
  </li>
</template>

<script>
export default {
  props: {
    task: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
  .app__item {
    margin: 0;
    padding: 17px 18px 22px 24px;
    border-radius: 4px;
    background-color: #ffffff;
  }

  .app__item-inner {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }

  .app__item-title {
    max-width: 60%;
  }

  .task__range-field {
    width: 66px;
    height: 33px;
    margin: 0;
    padding: 0;
    border: 0;
  }

  .task__range {
    -moz-appearance: none;
    -webkit-appearance: none;
    width: 66px;
    height: 33px;
    margin: 0;
    padding: 0 3px;
    border-radius: 16.5px;
    background-color: #ececec;
    cursor: pointer;
  }

  .task__range::-webkit-slider-thumb {
    -moz-appearance: none;
    -webkit-appearance: none;
    appearance: none;
    width: 28px;
    height: 28px;
    margin: 0;
    border-radius: 50%;
    background-color: #ffffff;
  }

  .task__range::-moz-range-thumb {
    -moz-appearance: none;
    -webkit-appearance: none;
    appearance: none;
    width: 28px;
    height: 28px;
    margin: 0 -3px 0 3px;
    border-radius: 50%;
    background-color: #ffffff;
  }

  .task__done {
    background-color: rgba(0, 179, 219, 0.12);
  }

  @media (min-width: 1440px) {
    .app__item-title {
      max-width: 400px;
    }
  }
</style>
