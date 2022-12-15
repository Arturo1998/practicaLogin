<template>
  <div>
    <h1>Ha accedido correctamente, su nivel es {{ persona[0].nivel }}</h1>
    <button
      class="ml-4 border-2 border-gray-800 rounded bg-cyan-400 hover:bg-cyan-600"
      @click="chao"
    >
      LOG OUT
    </button>
    <button
      class="ml-4 border-2 border-gray-800 rounded bg-cyan-400 hover:bg-cyan-600"
      @click="aniadeUsuario"
    >
      ALTA NUEVO
    </button>
    <div v-if="alta">
      <h1>Nombre</h1>
      <input
        type="text"
        class="border-2 border-gray-800 rounded hover:bg-cyan-100"
        v-model="nombre"
      />
      <h1>Contraseña</h1>
      <input
        type="text"
        class="border-2 border-gray-800 rounded hover:bg-cyan-100"
        v-model="password"
      />
      <h1>Nivel</h1>
      <select name="" id="" v-model="nivel">
        <option value="admin">Administrador</option>
        <option value="pro">Programador</option>
        <option value="usu">Usuario</option>
      </select>
      <button
        @click="registro"
        class="border-2 border-gray-800 rounded bg-cyan-400 hover:bg-cyan-600"
      >
        Registrar
      </button>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
import { ref } from "vue";

const logOut = ref(true);
let alta = ref(false);

const props = defineProps({
  usuario: {
    type: Object,
  },
});

const persona = ref(props.usuario);
const nombre = ref("");
const password = ref("");
const nivel = ref("");
const emits = defineEmits(["cerrar", "registrar"]);

const chao = () => {
  emits("cerrar", logOut.value);
};

const aniadeUsuario = () => {
  alta.value = !alta.value;
};

const registro = async () => {
  try {
    await axios.post(" http://localhost:3000/personas", {
      id: "",
      usuario: nombre.value,
      contraseña: password.value,
      nivel: nivel.value,
    });
  } catch (e) {
    console.log(e);
  }
};
</script>

<style lang="scss" scoped></style>
