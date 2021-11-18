<template>
  <div>
    <ul class="app__list">
      <DeletedItem
        v-for="del of deleted"
        :key="del.title"
        v-bind:del="del"
      />
    </ul>
  </div>
</template>

<script>
import DeletedItem from '@/components/deleteditem'
export default {
  props: ['deleted'],
  components: {
    DeletedItem
  }
}
</script>

<style scoped>
  .app__list {
    display: flex;
    flex-direction: column;
    gap: 4px;
    max-width: 574px;
    margin: 0;
    padding: 0;
    list-style: none;
  }
</style>
