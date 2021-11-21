<template>
  <form class="form">
    <label class="visually-hidden" for="search-form">Search</label>
    <input class="form__input-search" type="search" name="search" id="search-form" placeholder="Search">
  </form>
</template>

<style scoped>
  .form {
    margin: 0 0 auto 0;
    border: 0;
    border-radius: 5px;
    background-color: #ffffff;
  }

  .form__input-search {
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
    .form {
      max-width: 161px;
    }

    .form__input-search {
      max-width: 161px;
    }
  }
</style>
