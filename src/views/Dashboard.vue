<template>
  <VContainer>
    Dashboard
    <VBtn @click="logout">Logout</VBtn>
    <pre>
      {{meStore.user}}
    </pre>
  </VContainer>
</template>

<script setup>
import {userAuth} from "@/store/auth";
import {useRouter} from "vue-router";
import {useMe} from "@/store/me";

const authStore = userAuth();
const router = useRouter()
const meStore = useMe();

function logout() {
  authStore.logout().then(() => {
    router.push({name: 'login'})

  })
}
</script>
