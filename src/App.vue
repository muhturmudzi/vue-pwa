<template>
  <div id="app">
    <div v-if="showInstaller">
      Add Apps to homescreen?

      <button @click="installPWA">Yes, install</button>
      <button @click="dismissPrompt">No, thanks</button>
    </div>
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </nav>
    <router-view/>
  </div>
</template>

<script>
export default {
  data () {
    return {
      showInstaller: false,
      installEvent: null
    }
  },
  watch: {
    // showInstaller (e) {
    //   console.log(e, 'showInstaller')
    // }
  },
  created () {
    console.log('hello')
    window.addEventListener('beforeinstallprompt', (e) => {
      e.preventDefault()
      this.installEvent = e
      this.showInstaller = true
      console.log(this.showInstaller, this.installEvent, 'created')
    })
  },
  methods: {
    dismissPrompt () {
      this.showInstaller = false
    },
    installPWA () {
      this.installEvent.prompt()
      this.installEvent.userChoice.then((choice) => {
        console.log(choice, 'choice')
        this.dismissPrompt() // Hide the prompt once the user's clicked
        if (choice.outcome === 'accepted') {
          // Do something additional if the user chose to install
          console.log('accepted')
        } else {
          // Do something additional if the user declined
          console.log('denied')
        }
      })
    }
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
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
