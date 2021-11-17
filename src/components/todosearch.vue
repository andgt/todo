<template>
  <form class="form">
    <label class="visually-hidden" for="search-form">Search</label>
    <input type="search" name="search" id="search-form" placeholder="Search">
  </form>
</template>

<style scoped>
  .visually-hidden {
    position: absolute;
    clip: rect(0, 0, 0, 0);
    width: 1px;
    height: 1px;
    margin: -1px;
    font-size: 0;
  }

  .form {
    margin: 0 0 25px 0;
  }
</style>
