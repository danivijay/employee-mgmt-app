<template>
  <v-app>
    <v-toolbar
      app
    >
      <v-toolbar-title to="/" v-text="title"></v-toolbar-title>
      <v-spacer></v-spacer>
    </v-toolbar>
    <v-content>
      <router-view/>
    </v-content>
    <v-footer :fixed="fixed" app>
      <span>&copy; 2017</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      fixed: false,
      title: 'Emp-Mgr'
    }
  },
  name: 'App'
}
</script>
