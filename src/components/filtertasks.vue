<template>
  <div class="filter">
    <FilterItem
      v-for="filterInput of filterInputs"
      :key="filterInput.title"
      v-bind:filterInput="filterInput"
      v-on:filtering="filtering"
    />
  </div>
</template>

<script>
import FilterItem from '@/components/filteritem'
export default {
  props: ['filterInputs'],
  components: {
    FilterItem
  },
  methods: {
    filtering (filterInput) {
      this.$emit('filtering', filterInput)
    }
  }
}
</script>

<style scoped>
  .filter {
    display: flex;
    flex-wrap: wrap;
    margin-bottom: 22px;
  }
</style>
