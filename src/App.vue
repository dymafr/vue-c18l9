<template>
  <!--  OUVREZ le lien du projet à droite dans un nouvel onglet pour voir la modification de l'URL lors de la navigation   -->
  <nav class="d-flex flex-row align-items p-20">
    <router-link to="/a" class="mr-10"> Page A</router-link>
    <router-link class="mr-10" to="/b"> Page B</router-link>
    <router-link
      class="mr-10"
      v-for="user in state.users"
      :to="{ path: `/b/${user._id}` }"
      >{{ user.name }}</router-link
    >
  </nav>
  <div class="d-flex flex-row">
    <router-view></router-view>
  </div>
</template>

<script setup lang="ts">
import { watchEffect, reactive } from 'vue';

const state = reactive<{ users: any[] }>({
  users: null,
});

watchEffect(async () => {
  await fetch(`https://restapi.fr/generator`, {
    method: 'POST',
    body: JSON.stringify({
      times: 2,
      resourceName: 'usertest',
      name: 'firstName',
    }),
    headers: {
      'Content-Type': 'application/json',
    },
  });
  const response = await fetch('https://restapi.fr/api/usertest/');
  state.users = await response.json();
});
</script>

<style lang="scss">
@import './assets/scss/base.scss';

nav {
  background-color: var(--primary-1);
  a {
    color: white;
  }
}
</style>
