<template>
  <teleport to="body">
    <div class="backdrop" @click="handleClose"></div>
    <transition name="dialog">
      <dialog v-if="errorMessage || successMessage">
        <slot />
        <div class="wrapper-icon" @click="handleClose">
          <img :src="svg" class="icon" />
        </div>
      </dialog>
    </transition>
  </teleport>
</template>

<script setup>
import { inject, onBeforeUnmount, ref } from "vue";
import svg from "../../assets/close.svg";

const errorMessage = inject("errorMessage");
const successMessage = inject("successMessage");
const handleClose = inject("handleClose");

if (errorMessage.value || successMessage.value)
  document.body.style.overflow = "hidden";

onBeforeUnmount(() => {
  document.body.style.overflow = "";
});
</script>

<style scoped lang="scss">
.backdrop {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.75);
  z-index: 10;
}
dialog {
  display: block;
  padding: 100px 20px;
  top: 20vh;
  left: 10%;
  width: 80%;
  z-index: 100;
  border-radius: 12px;
  border: none;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  overflow: hidden;
  background-color: white;

  @media screen and (min-width: 767px) {
    left: calc(50% - 20rem);
    width: 40rem;
  }
}

.icon {
  width: 20px;
  height: 20px;
}

.dialog-enter-from,
.dialog-leave-to {
  opacity: 0;
  transform: scale(0.8);
}

.dialog-enter-active {
  transition: all 0.3s ease-out;
}
.dialog-leave-active {
  transition: all 0.3s ease-in;
}

.dialog-enter-to,
.dialog-leave-from {
  opacity: 1;
}

.wrapper-icon {
  position: absolute;
  top: 20px;
  right: 20px;
  width: 40px;
  height: 40px;
  padding: 10px;
  cursor: pointer;
  transition: all 0.3s;

  &:hover {
    background-color: rgb(128, 128, 128);
    border-radius: 50%;
    box-shadow: rgba(0, 0, 0, 0.3) 0px 2px 4px 0px;
  }
}
</style>
