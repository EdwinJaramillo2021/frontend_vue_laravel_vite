<template>
  <br />
  <pre>{{ usuario }}</pre>
  <h1>Login</h1>
  <form @submit.prevent="funIngresar()">
    <label for="e">Ingrese su correo</label>
    <input type="email" id="e" required v-model="usuario.email" />
    <br />
    <label for="pass">Ingrese su contraseña</label>
    <input type="password" id="pass" required v-model="usuario.password" />
    <br />
    <input type="submit" value="Ingresar" />
    <a href="">¿Olvidaste tu Contraseña?</a>
  </form>
</template>

<script setup>
import authService from "./../../services/auth.service";
import { ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();

const usuario = ref({ email: "", password: "" });

async function funIngresar() {
  try {
    const { data } = await authService.login(usuario.value);
    console.log(data.access_token);
    localStorage.setItem("access_token", data.access_token);
    router.push("/servicios");
  } catch (error) {
    alert("Credenciales Incorrectas");
  }
}
</script>
