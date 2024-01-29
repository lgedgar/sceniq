<script setup>
// import { RouterLink, RouterView } from 'vue-router'
import {RouterLink} from 'vue-router'
// import { mapStores } from 'pinia'
// import {useQordialAuthStore} from 'qordial'
// import appsettings from './appsettings'
</script>

<template>
  <main>
    <p class="block">
      I would like to eventually add other features, but
      for now there is just the one:
    </p>
    <o-button variant="primary"
              @click="$router.push('/manager')">
      Video Manager
    </o-button>
  </main>
</template>
