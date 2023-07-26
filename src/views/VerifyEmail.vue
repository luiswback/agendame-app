<template>
  <div>
    <div v-if="isLoading">Verificando</div>
    <div v-else-if="!isReady">Token inválido</div>
    <div v-else>Email verificado com sucesso! <br>
      Obrigado, {{ state.data.first_name }} por verificar seu email.
      <!--      TODO: mapear erros-->
      <!--     Você já verificou seu email-->
    </div>
  </div>
</template>

<script setup>
import {userAuth} from "@/store/auth";
import {useRoute} from "vue-router";
import {ref} from "vue";
import {useAsyncState} from "@vueuse/core";

const authStore = userAuth();
const route = useRoute();

const {state, isReady, isLoading} = useAsyncState(
  authStore.verifyEmail(route.query.token).then(r => r.data),
)

</script>
