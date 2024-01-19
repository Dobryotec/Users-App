<template>
  <div class="details">
    <button class="button" :style="margin" @click="openDetails">
      {{ details }}
    </button>
    <div v-if="isOpen" class="details">
      <img :src="avatar" class="image" />
      <p class="text">{{ email }}</p>
      <p class="text">{{ fullName }}</p>
      <input class="input" type="text" placeholder="Phone" v-model="phone" />
      <input
        class="input"
        type="text"
        placeholder="Address"
        v-model="address"
      />
    </div>
  </div>
</template>

<script setup>
import { defineProps, ref, computed } from "vue";

const phone = ref("");
const address = ref("");

const isOpen = ref(false);

const props = defineProps(["id", "email", "fullName", "avatar"]);

const openDetails = () => {
  isOpen.value = !isOpen.value;
};

const details = computed(() => {
  return isOpen.value ? "Hide details" : "Show details";
});

const margin = computed(() => {
  return isOpen.value ? { "margin-bottom": "20px" } : {};
});
</script>

<style scoped lang="scss">
.details {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}
.image {
  border-radius: 5px;
  box-shadow: rgba(0, 0, 0, 0.3) 0px 2px 4px 0px;
}

.button {
  font-size: 18px;
  max-width: 140px;
  padding: 10px 15px;
  outline: transparent;
  border-radius: 5px;
  border: 1px solid rgb(128, 128, 128);
  color: rgb(128, 128, 128);
  transition: all 0.3s;

  &:focus,
  &:hover {
    background-color: rgb(128, 128, 128);
    color: rgb(255, 255, 255);
  }
}
.text {
  font-size: 16px;
  color: rgb(128, 128, 128);
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
