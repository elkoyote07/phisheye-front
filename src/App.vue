<template>
  <div id="app">
    <div id="nav">
      <router-link v-if="authenticated" to="/">Home</router-link>
      <router-link to="/about">About</router-link>
      <router-link v-if="authenticated" to="/login" v-on:click.native="logout()" replace>Logout</router-link>
      <router-link v-else to="/login">Login</router-link>
    </div>
    <router-view @authenticated="setAuthenticated"/>
  </div>
</template>

<script>
    export default {
        name: 'App',
        data() {
            return {
                authenticated: false,
                mockAccount: {
                    username: "admin",
                    password: "admin"
                }
            }
        },
        methods: {
            setAuthenticated(status) {
                this.authenticated = status;
            },
            logout() {
                this.authenticated = false;
            }
        }
    }
</script>

<style>
body {
  margin: 0; /* Remove default margin */
  padding: 0; /* Remove default padding */
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #42b983;
  
  /* Background image */
  background-image: url('./assets/background.jpg');
  background-size: cover; /* Adjust the size of the image to cover the entire viewport */
  background-position: center; /* Center the background image */
  height: 100vh; /* Set the height to cover the entire viewport height */
}
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
  color: white;
  padding-right: 10px;
}

#nav a:not(:first-child) {
  border-left: 1px solid gray;
  padding-left: 10px; 
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>