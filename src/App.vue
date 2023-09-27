<template>
  <UserProfile />
</template>

<script>
import UserProfile from './views/UserProfile.vue'
export default {
  name: 'App',
  components: {
    UserProfile,
  }
}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Raleway:wght@100;300&display=swap");

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: -8px;
  font-family: 'Raleway', sans-serif;
  height: 100vh;
}
</style>
