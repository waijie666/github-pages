<template>
  <div id="nav">
    <template v-for="route in currentRoutes" :key="route.name">
      <template v-if="!route.routerLinkExcept">
        <router-link :to="route.path">{{ route.name }}</router-link> | 
      </template>
    </template>
  </div>
  <router-view/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>

<script>

export default {
  name: 'app',
  mounted() {

  },
  created () {
    if (sessionStorage.redirect) {
        const redirect = sessionStorage.redirect
        delete sessionStorage.redirect
        this.$router.push(redirect)
    }
  },
  computed: {
    currentRoutes() {
      return this.$router.options.routes
    }
  }
}
</script>

