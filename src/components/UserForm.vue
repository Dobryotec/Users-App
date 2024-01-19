<template>
  <form class="form" @submit.prevent="addUser">
    <input class="input" type="text" placeholder="Name" v-model.trim="name" />
    <input class="input" type="text" placeholder="Email" v-model.trim="email" />
    <button class="button" type="submit">Add</button>
    <BaseDialog v-if="errorMessage || successMessage">
      <p class="text">{{ errorMessage || successMessage }}</p>
    </BaseDialog>
  </form>
</template>

<script setup>
import { ref, provide } from "vue";
import BaseDialog from "./ui/BaseDialog.vue";
const name = ref("");
const email = ref("");
const errorMessage = ref("");
const successMessage = ref("");

provide("errorMessage", errorMessage);
provide("successMessage", successMessage);

const handleError = () => {
  errorMessage.value = "";
};

const handleSuccess = () => {
  successMessage.value = "";
};

const handleClose = () => {
  if (errorMessage.value) {
    handleError();
  } else {
    handleSuccess();
  }
};

provide("handleClose", handleClose);

const addUser = async () => {
  try {
    if (!name.value || !email.value) {
      errorMessage.value = "Please enter both name and email :)";
      return;
    }

    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailRegex.test(email.value)) {
      errorMessage.value = "Please enter a valid email address :)";
      return;
    }

    const response = await fetch("https://reqres.in/api/users", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        name: name.value,
        email: email.value,
      }),
    });

    if (response.ok) {
      name.value = "";
      email.value = "";
      successMessage.value = "Profile added successfully!";
    }
  } catch (error) {
    errorMessage.value = error.message;
  }
};
</script>

<style scoped lang="scss">
.form {
  max-width: 400px;
  margin: 0 auto;
  display: flex;

  flex-direction: column;
  gap: 20px;
  margin-bottom: 20px;

  @media screen and (min-width: 767px) {
    max-width: 800px;
    flex-direction: row;
  }
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

.text {
  font-size: 30px;
  font-weight: 700;
  text-align: center;
  color: rgb(128, 128, 128);
}
</style>
