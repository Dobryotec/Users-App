<template>
  <div>
    <header><UserForm /></header>
    <main>
      <FiltrationUsers :users="users" @updateName="updateName" />
      <ul class="list">
        <User
          v-for="{ avatar, email, first_name, id, last_name } in filteredUsers"
          :key="id"
          :avatar="avatar"
          :email="email"
          :first-name="first_name"
          :last-name="last_name"
          :id="id"
        >
        </User>
      </ul>
      <BaseSpinner v-if="isLoading" />
    </main>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import User from "./User.vue";
import UserForm from "./UserForm.vue";
import FiltrationUsers from "./FiltrationUsers.vue";
import BaseSpinner from "../components/ui/BaseSpinner.vue";

const users = ref([]);
const filteredUsers = ref([]);
const name = ref("");
const isLoading = ref(true);

async function loadUsers() {
  try {
    const response = await fetch("https://reqres.in/api/users");

    const responseData = await response.json();
    users.value = responseData.data;
    filteredUsers.value = [...users.value];
      isLoading.value = false;
    
  } catch (error) {
    console.log(error);
    isLoading.value = false;
  }
}

function updateName(newName) {
  name.value = newName;
  filterUsers();
}

onMounted(() => {
  loadUsers();
});

const filterUsers = () => {
  return (filteredUsers.value = users.value.filter((user) =>
    user.first_name.toLowerCase().includes(name.value.toLowerCase())
  ));
};
</script>

<style scoped lang="scss">
.list {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  gap: 30px;
  margin-top: 70px;
}
</style>
