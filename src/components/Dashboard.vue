<template>
  <v-layout row wrap>
      <v-flex xs12 sm8 md6 offset-sm2 offset-md3>
        <v-toolbar color="white" class="mt-2">
            <v-toolbar-title>Employees</v-toolbar-title>
            <v-btn
              to="/new"
              color="pink"
              dark
              small
              absolute
              bottom
              right
              fab
            >
              <v-icon>add</v-icon>
            </v-btn>
          </v-toolbar>

          <v-list two-line>
            <v-list-tile to='/view/1'>
              <v-list-tile-content>
                <v-list-tile-title>
                  Hello
                </v-list-tile-title>
                <v-list-tile-sub-title>
                  World
                </v-list-tile-sub-title>
              </v-list-tile-content>
            </v-list-tile>
          </v-list>

      </v-flex>
  </v-layout>
</template>

<script>
export default {

}
</script>

<style>

</style>
