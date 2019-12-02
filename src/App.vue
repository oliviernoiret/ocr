<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      ligth
    >
    <h1 color="primary">
    Récupération du texte d'un fichier pdf
    </h1>
    </v-app-bar>

    <v-content>
      <v-container fluid>
        <router-view>
        </router-view>
      </v-container>
    </v-content>

   </v-app>
</template>

<script>

export default {
  name: 'App',

  components: {
  },

  data: () => ({
    //
  })
}
</script>
