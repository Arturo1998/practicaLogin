<template>
  <div>
    <h1>Login Usuarios</h1>
    <div class="flex flex-col w-40">
      <input
        class="border-2 border-gray-800 hover:bg-cyan-100"
        type="text"
        placeholder="Usuario"
        v-model="usuario"
        ref="inputNombre"
      />
      <input
        class="border-2 border-gray-800 hover:bg-cyan-100"
        type="password"
        placeholder="Password"
        v-model="contraseña"
      />
    </div>
    <div class="">
      <button
        class="border-2 border-gray-800 rounded bg-cyan-400 hover:bg-cyan-600"
        @click="login"
      >
        LOG IN
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
let usuario = ref("");
let contraseña = ref("");
let inputNombre = ref(null);
const emits = defineEmits(["hacerLogin"]);

const login = () => {
  emits("hacerLogin", usuario.value, contraseña.value);
  usuario.value = "";
  contraseña.value = "";
  inputNombre.value.focus();
};
</script>

<style lang="scss" scoped></style>
