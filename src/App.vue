<template>
  <v-app>
    <v-app-bar
      app
      color="rgb(84, 84, 84);"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="http://www.oficina5.com.br/img/logo-oficina5-sol.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="http://www.oficina5.com.br/"
        target="_blank"
        text
      >
        <span class="mr-2">Oficina 5</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-content>
      <Home/>
    </v-content>
  </v-app>
</template>

<script>
import Home from './views/Home';


export default {
  name: 'App',

  components: {
    Home
  },

  data: () => ({
    //
  }),
};
</script>
