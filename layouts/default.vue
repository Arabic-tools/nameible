<template>
  <v-app>
    <v-app-bar  fixed app>
      <h1 style="color:#FF6437">{{title}}</h1>
      
      <v-spacer />
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>

    <v-footer :absolute="!fixed" app>

      <v-row>
        <v-col style="text-align:center">
                              <!-- الموقع برعاية :

          <a href="https://wasetshera.com?myad=53196"> وسيط شراء من الإنترنت</a>
          <br /> -->
         contact us :
          <a href="mailto:nameible@inboxeen.com">nameible@inboxeen.com</a>

          <br />
              © 2021 Nameible. All rights reserved.
        </v-col>
      </v-row>
  
      <!-- <span>&copy; {{ new Date().getFullYear() }}</span> -->
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,

      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Nameible',
    }
  },
}
</script>
