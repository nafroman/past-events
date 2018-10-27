<template>
  <v-app class="grey darken-4">
    <v-toolbar app class = "grey grey lighten-1">
      <v-toolbar-title class="headline text-uppercase">
        <span class="font-weight-light">Contract Event Visualisation</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
     
       
    </v-toolbar>

    <v-content>
      <HelloWorld/>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data () {
    return {
      //
    }
  }
}
</script>