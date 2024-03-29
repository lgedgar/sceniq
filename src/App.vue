<script setup>
import { RouterLink, RouterView } from 'vue-router'
import { mapStores } from 'pinia'
import {useQordialAuthStore} from 'qordial'
import appsettings from './appsettings'
</script>

<script>
export default {

    data() {
        return {
            appsettings,
            darkMode: false,
        }
    },

    computed: {
        ...mapStores(useQordialAuthStore),
    },

    mounted() {
        // nb. for some reason the current route does not load automatically
        // in the context of a published q-app, so we do that explicitly
        this.$router.push(window._qdnPath)

        // set dark mode if applicable
        if (window._qdnTheme == 'dark') {
            this.setDarkMode(true)
        }
    },

    methods: {

        async authButtonClick() {
            if (!this.qordialAuthStore.address) {
                await this.$qordial.authenticate()
            } else {
                await qortalRequest({
                    action: 'OPEN_PROFILE',
                    name: this.qordialAuthStore.username,
                })
            }
        },

        setDarkMode(dark) {
            this.darkMode = dark
            const body = document.querySelector('body')
            body.className = dark ? 'dark' : ''
        },
    },
}
</script>

<template>
   <header>
    <div style="display: flex; gap: 1rem; align-items: center;">

      <h1 class="is-size-1"
          style="flex-grow: 1;">
        {{ appsettings.appTitle }}
      </h1>

      <a v-if="!darkMode"
         href="#" @click.prevent="setDarkMode(true)">
        <o-icon icon="moon" size="large" />
      </a>
      <a v-if="darkMode"
         href="#" @click.prevent="setDarkMode(false)">
        <o-icon icon="sun" size="large" />
      </a>

      <o-button icon-left="user"
                @click="authButtonClick">
        {{ qordialAuthStore.username || "not authenticated" }}
      </o-button>

    </div>

    <nav>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/manager">Video Manager</RouterLink>
      <RouterLink to="/about">About</RouterLink>
    </nav>
  </header>

  <div style="padding: 2rem;">
    <RouterView />
  </div>
</template>

<style scoped>

header {
    padding: 1rem;
}

nav {
  text-align: left;
  margin-top: 1rem;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

</style>
