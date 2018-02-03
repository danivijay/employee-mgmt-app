<template>
  <v-container>
    <v-layout>
      <v-flex xs12 sm8 md6 offset-sm2 offset-md3>

        <v-card>
          <v-card-title>
            <h2>Add Employee</h2>
          </v-card-title>

          <v-card-content>
            <v-form class="pl-3 pr-3">
              <v-text-field
                label="Employee ID#"
                type="number"
                v-model="employee_id"
              ></v-text-field>
              <v-text-field
                label="Name"
                v-model="name"
              ></v-text-field>
              <v-text-field
                label="Position"
                v-model="position"
              ></v-text-field>
              <v-text-field
                label="Department"
                v-model="dept"
              ></v-text-field>
            </v-form>
          </v-card-content>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn flat to="/">Back</v-btn>
            <v-btn dark class="green" @click.prevent="onSubmit">Add</v-btn>
          </v-card-actions>
        </v-card>

      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import db from './firebaseinit'

export default {
  data () {
    return {
      employee_id: null,
      name: null,
      dept: null,
      position: null
    }
  },
  methods: {
    onSubmit () {
      db.collection('employees').add({
        employee_id: this.employee_id,
        name: this.name,
        dept: this.dept,
        position: this.position
      })
        .then(docRef => this.$router.push('/'))
        .catch(err => console.log(err))
    }
  }
}
</script>

<style>

</style>
