<template>
  <div class="container">
    <slot />
  </div>
</template>

<style scoped>
.container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 30px 15px;

  @media screen and (min-width: 767px) {
    padding: 100px 15px;
  }
}
</style>
