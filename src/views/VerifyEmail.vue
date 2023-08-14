<template>
  <div class="authentication">
    <v-container fluid class="pa-3">
      <v-row class="h-100vh d-flex justify-center align-center">
        <v-col cols="12" lg="4" xl="3" class="d-flex align-center">
          <v-card rounded="md" elevation="10" class="px-sm-1 px-0 withbg mx-auto" max-width="500">
            <v-card-item class="pa-sm-8">
              <div class="d-flex justify-center py-4">
                <Logo/>
              </div>

              <div v-if="isLoading">Verificando</div>
              <div v-else-if="!isReady" class="text-error text-center">Token inválido</div>
              <div v-else class="text-success text-center">Email verificado com sucesso! <br>
                Obrigado, {{ state.data.first_name }} por verificar seu email.
                <!--      TODO: mapear erros-->
                <!--     Você já verificou seu email-->
              </div>
            </v-card-item>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>

</template>

<script setup>
import {userAuth} from "@/store/auth";
import {useRoute} from "vue-router";
import {ref} from "vue";
import Logo from '@/components/logo/Logo.vue'
import {useAsyncState} from "@vueuse/core";

const authStore = userAuth();
const route = useRoute();

const {state, isReady, isLoading} = useAsyncState(
  authStore.verifyEmail(route.query.token).then(r => r.data),
)

</script>
