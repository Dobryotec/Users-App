<template>
  <div class="wrapper-input">
    <input
      class="input"
      type="text"
      placeholder="Enter name please..."
      v-model.trim="name"
      @input="handleName"
    />
  </div>
</template>

<script setup>
import { defineProps, ref, defineEmits } from "vue";

const emits = defineEmits();

const name = ref("");
const { users } = defineProps(["users"]);

const handleName = () => {
  emits("updateName", name.value);
};
</script>

<style scoped lang="scss">
.wrapper-input {
  max-width: 400px;
  margin: 0 auto;
}
.input {
  font-size: 20px;
  width: 100%;

  padding: 10px;
  border-radius: 5px;
  outline: transparent;
  border: 2px solid rgb(128, 128, 128);
  transition: box-shadow 0.3s;
  cursor: pointer;
  color: rgb(128, 128, 128);

  &:focus,
  &:hover {
    box-shadow: rgb(255, 255, 255) 0px 0px 0px 1px,
      rgb(166, 229, 255) 0px 0px 2px 3px, rgb(0, 106, 255) 0px 0px 2px 4px;
  }
}
</style>
