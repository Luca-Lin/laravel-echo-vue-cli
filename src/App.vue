<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Echo from 'laravel-echo'
import Pusher from 'pusher-js'

window.Pusher = Pusher;
window.Echo = new Echo({
    broadcaster: 'pusher',
    key: process.env.VUE_APP_WEBSOCKETS_KEY,
    wsHost: process.env.VUE_APP_WEBSOCKETS__SERVER,
    wsPort: 6001,
    forceTLS: false,
    disableStats: true,
    enabledTransports: ['ws']
})

export default {
  name: 'App',
  components: {
    HelloWorld
  },

  mounted() {
    window.Echo.channel('channel')
      .listen('LineBotMessage', (e) => {
        console.log(e);
      })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
