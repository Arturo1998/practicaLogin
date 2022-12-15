<template>
  <div v-if="visible">
    <h1>Login Usuarios</h1>
    <div class="flex flex-col w-40">
      <input
        class="border-2 border-gray-800 hover:bg-cyan-100"
        type="text"
        placeholder="Usuario"
        v-model="usuario"
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
        @click="getUsuario"
      >
        LOG IN
      </button>
    </div>
  </div>
  <div v-else class="flex">
    <MiRegistro @cerrar="salir" :usuario="usuarios" />
  </div>
</template>

<script setup>
import { ref } from "vue";
import axios from "axios";
import MiRegistro from "./components/MiRegistro.vue";

let usuarios = ref({});
let usuario = ref("");
let contraseña = ref("");
let visible = ref(true);

const getUsuario = async () => {
  const respuesta = await axios.get(
    `http://localhost:3000/personas?usuario=${usuario.value}&contraseña=${contraseña.value}`
  );
  usuarios.value = respuesta.data;
  usuarios.value.length > 0
    ? (visible.value = false)
    : (visible.value = true) & alert("usuario o contraseña incorrecta");
};

const salir = (data) => {
  visible.value = data;
  console.log(visible.value);
};
</script>

<style scoped></style>
