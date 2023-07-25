<template>
  <VContainer>
    <VTextField v-model="email"/>
    <VTextField type="password" v-model="password"/>
    <VBtn @click="login">Login</VBtn>
  </VContainer>
</template>

<script setup>
import {ref} from "vue";
import {userAuth} from "@/store/auth";
import {useRouter} from "vue-router";

const authStore = userAuth();
const router = useRouter()

const email = ref('test@example.com');
const password = ref('password');

function login() {
  authStore.login(email.value, password.value).then(() => {
    router.push({name: 'dashboard'})
  });
}

</script>
