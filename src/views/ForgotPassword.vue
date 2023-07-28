<template>
  <div>
    <template v-if="state === 'forgotPassword'">
      <div>Esqueceu sua senha?</div>
      <br>
      <VTextField v-model="email"></VTextField>
      <VBtn @click="forgotPassword">Confirmar Email</VBtn>
    </template>

    <template v-else-if="state === 'resetPassword'">
      <div>Redenifir senha</div>
      <VTextField v-model="token"></VTextField>
      <VTextField v-model="password" type="password"></VTextField>
      <VBtn @click="resetPassword">Redefinir senha</VBtn>
      <a href="" @click.stop.prevent="changeToForgotPassword">voltar</a>
    </template>
  </div>
</template>

<script setup>

import {ref} from "vue";
import {userAuth} from "@/store/auth";
import router from "@/router";

const email = ref();
const state = ref('forgotPassword');
const token = ref();
const password = ref();

function forgotPassword() {
  const authStore = userAuth();
  authStore.forgotPassword(email.value).then(() => {
    changeToResetPassword()
  })
}

function resetPassword() {
  const authStore = userAuth();
  authStore.resetPassword(token.value, password.value).then(() => {
    changeToForgotPassword()
    router.push({name: 'login'})
  })
}

function changeToResetPassword() {
  state.value = 'resetPassword'
}

function changeToForgotPassword() {
  email.value = '';
  password.value = '';
  token.value = '';
  state.value = 'forgotPassword'
}
</script>
