<template>
  <li class="item">
    <img class="image" :src="avatar" />
    <p class="text">{{ email }}</p>
    <p class="text">{{ fullName }}</p>
    <button class="button" @click="deleteUser">Delete</button>
    <transition name="details">
      <UserDetails
        :id="id"
        :email="email"
        :avatar="avatar"
        :full-name="fullName"
      />
    </transition>
  </li>
</template>

<script setup>
import { defineProps, computed } from "vue";
import { useToast } from "vue-toastification";
import UserDetails from "./UserDetails.vue";
const props = defineProps(["id", "email", "avatar", "firstName", "lastName"]);

const toast = useToast();

const fullName = computed(() => {
  return props.firstName + " " + props.lastName;
});

const deleteUser = async () => {
  try {
    const response = await fetch(`https://reqres.in/api/users/${props.id}`, {
      method: "DELETE",
    });

    if (response.ok) {
      toast.success("User profile deleted successfully :)", {
        timeout: 2000,
      });
    }
  } catch (error) {
    console.log(error);
  }
};
</script>

<style scoped lang="scss">
.item {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 330px;
  min-height: 450px;
  padding: 24px;
  gap: 20px;
  box-shadow: rgba(0, 0, 0, 0.3) 0px 2px 4px 0px;
  transition: all 0.2s ease-in-out;
  cursor: pointer;
  border-radius: 4px;
  background-color: rgb(255, 255, 255);

  &:hover,
  &:focus {
    transform: scale(1.05) translate(0px, -8px);
  }
}

.image {
  border-radius: 5px;
  box-shadow: rgba(0, 0, 0, 0.3) 0px 2px 4px 0px;
}

.text {
  font-size: 20px;
  color: rgb(128, 128, 128);
}

.button {
  width: 150px;
  margin: 0 auto;
  font-size: 20px;
  font-weight: 600;
  background-color: rgb(255, 255, 255);
  border: 2px solid rgb(0, 106, 255);
  color: rgb(0, 106, 255);
  outline: transparent;
  border-radius: 5px;
  padding: 10px;
  transition: all 0.3s;

  &:focus,
  &:hover {
    background-color: rgb(0, 106, 255);
    color: rgb(255, 255, 255);
  }
}

.details-enter-from,
.details-leave-to {
  opacity: 0;
}

.details-enter-active {
  transition: all 0.3s ease-out;
}
.details-leave-active {
  transition: all 0.3s ease-in;
}

.details-enter-to,
.details-leave-from {
  opacity: 1;
}
</style>
