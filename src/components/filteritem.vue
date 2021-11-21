<template>
  <div class="filter__wrapper">
    <button class="filter__button" :class="{ 'filter__active': filterInput.active }" v-on:click="$emit('filtering', filterInput)"><span>{{filterInput.title}}</span></button>
  </div>
</template>

<script>
export default {
  props: {
    filterInput: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
  .filter__wrapper {
    position: relative;
    margin: 0;
    padding: 0 10px 0 0;
    color: #000000;
  }

  .filter__wrapper:not(:last-child) {
    margin-right: 5px;
  }

  .filter__wrapper:not(:last-child)::before {
    content: "/";
    position: absolute;
    top: 0;
    right: 0;
    width: 6px;
    height: auto;
    font-weight: 400;
    color: #000000;
  }

  .filter__button {
    font-size: 12px;
    line-height: 18px;
    border: 0;
    background-color: transparent;
    cursor: pointer;
  }

  .filter__active {
    font-weight: 700;
    color: #00b3db;
  }

  @media (min-width: 768px) {
    .filter__button {
      font-size: 15px;
      line-height: 25px;
    }

    .filter__wrapper:not(:last-child)::before {
      top: 5px;
    }
  }
</style>
