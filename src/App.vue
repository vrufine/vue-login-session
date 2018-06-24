<template>
  <v-app>
    <v-content>
      <router-view/>
    </v-content>
  </v-app>
</template>

<script>

  export default {
    name: 'App',
    data() {
      return {
        clipped: false,
        drawer: true,
        fixed: false,
        items: [{
          icon: 'bubble_chart',
          title: 'Inspire'
        }],
        miniVariant: false,
        right: true,
        rightDrawer: false,
        title: 'Vuetify.js'
      }
    }
  }
</script>