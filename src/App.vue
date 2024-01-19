<template>
  <BaseContainer>
    <Users />
  </BaseContainer>
</template>

<script setup>
import BaseContainer from "./components/ui/BaseContainer.vue";
import Users from "./components/Users.vue";
</script>

<style>
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  border: none;
  box-sizing: border-box;
}
li {
  list-style: none;
}
a {
  color: inherit;
}
a:link,
a:visited {
  text-decoration: none;
}
a:hover {
  text-decoration: none;
}
img {
  vertical-align: top;
}
h1,
h2,
h3,
h4,
h5,
h6 {
  font-weight: inherit;
  font-size: inherit;
}
input,
button,
textarea {
  font-family: inherit;
  font-size: inherit;
}
button {
  cursor: pointer;
  color: inherit;
  background-color: inherit;
}
body {
  font-family: Open Sans, sans-serif;
  line-height: 1;
  color: rgb(42, 42, 51);
}
</style>
