<template>
  <v-app>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-avatar class="mr-5">
      <img
        src="/blockchain-logo.png"
        alt="John"
      >
    </v-avatar>
      <v-toolbar-title v-text="title" />
      <v-spacer />
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer :absolute="!fixed">
      <lable>Praveen | 2021</lable>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: false,
      title: 'Blockchain'
    }
  }
}
</script>
