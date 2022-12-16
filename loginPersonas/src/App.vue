<template>
  <div v-if="visible">
    <MiLogin @hacerLogin="getUsuario" />
  </div>
  <div v-else class="flex">
    <MiRegistro @cerrar="salir" :usuario="usuarios" :listaUsuario="listaApi" />
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import MiLogin from "./components/MiLogin.vue";
import MiRegistro from "./components/MiRegistro.vue";

let usuarios = ref([]);
let listaApi = ref([]);
let visible = ref(true);

onMounted(() => {
  getLista();
});

const getLista = async () => {
  const respuesta = await axios.get("http://localhost:3000/personas");
  listaApi.value = respuesta.data;
};

const getUsuario = async (data1, data2) => {
  const respuesta = await axios.get(
    `http://localhost:3000/personas?usuario=${data1}&contraseña=${data2}`
  );
  usuarios.value = respuesta.data;
  usuarios.value.length > 0
    ? (visible.value = false)
    : (visible.value = true) & alert("usuario o contraseña incorrecta");
};

const salir = (data) => {
  visible.value = data;
};
</script>

<style scoped></style>
