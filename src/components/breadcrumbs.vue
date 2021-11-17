<template>
  <div class="breadcrumbs" id="breadcrumbs">
    <ul class="breadcrumbs__list" itemscope="" itemtype="http://schema.org/BreadcrumbList">
      <li itemprop="itemListElement" itemscope="" itemtype="http://schema.org/ListItem"><a itemprop="item" href="main.html"><span itemprop="name">Все</span></a>
        <meta itemprop="position" content="1">
      </li>
      <li itemprop="itemListElement" itemscope="" itemtype="http://schema.org/ListItem"><a itemprop="item" href="#"><span itemprop="name">Выполненные</span></a>
        <meta itemprop="position" content="2">
      </li>
      <li itemprop="itemListElement" itemscope="" itemtype="http://schema.org/ListItem"><a itemprop="item" href="#"><span itemprop="name">Невыполненные</span></a>
        <meta itemprop="position" content="3">
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .breadcrumbs {
    margin: 0 0 22px 0;
  }

  .breadcrumbs__list {
    margin: 0;
    padding: 0;
    list-style: 0;
  }
</style>
