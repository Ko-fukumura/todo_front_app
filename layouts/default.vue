<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title v-text="title" />
      <div class="flex-grow-1" />
      <span v-if="loggedIn" @click="logout()">Logout</span>
    </v-app-bar>
    <v-content>
      <nuxt />
    </v-content>
    <v-footer center>
      <v-layout justify-center>
        <span>&copy; 2019 Yuhei Okazaki. All Rights Reserved.</span>
      </v-layout>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      title: 'Tasks'
    }
  },
  computed: {
    loggedIn() {
      return this.$auth.loggedIn
    }
  },
  methods: {
    async logout() {
      try {
        await this.$auth.logout()
        await this.$apolloHelpers.onLogout()
        this.$router.push('/login')
      } catch (e) {
        window.console.log(e)
      }
    }
  }
}
</script>