<template>
  <div>
    <h1>
      Hola {{ persona[0].usuario }}, ha accedido correctamente. Su nivel es
      {{ persona[0].nivel }}.
    </h1>
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
    <div class="border-2 border-cyan-400 mt-4 text-center">
      <ul v-for="item in lista" :key="item.id">
        <li class="hover:bg-cyan-400 border-2 border-cyan-300">
          {{ item.usuario }} - {{ item.nivel }}
        </li>
        <button class="bg-red-300 rounded">Borrar</button>
      </ul>
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
    type: Array,
  },
  listaUsuario: {
    type: Array,
  },
});

const persona = ref(props.usuario);
const lista = ref(props.listaUsuario);
const nombre = ref("");
const password = ref("");
const nivel = ref("");
let usuarioExiste = ref([]);
const emits = defineEmits(["cerrar", "registrar", "borrar"]);

const chao = () => {
  emits("cerrar", logOut.value);
};

const aniadeUsuario = () => {
  alta.value = !alta.value;
  console.log(lista.value);
};

const registro = async () => {
  try {
    const respuesta = await axios.get(
      `http://localhost:3000/personas?usuario=${nombre.value}`
    );
    usuarioExiste.value = respuesta.data;
    if (usuarioExiste.value.length > 0) {
      alert("El nombre de usuario está en uso");
    } else {
      await axios.post(" http://localhost:3000/personas", {
        id: "",
        usuario: nombre.value,
        contraseña: password.value,
        nivel: nivel.value,
      });
    }
  } catch (e) {
    console.log(e);
  }
};
</script>

<style lang="scss" scoped></style>
