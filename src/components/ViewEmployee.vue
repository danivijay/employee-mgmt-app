<template>
  <v-container>
    <v-layout>
      <v-flex xs12 sm8 md6 offset-sm2 offset-md3>

        <v-card>
          <v-card-title>
            <h2>{{ employee.employee_id }}. {{ employee.name }}</h2>
          </v-card-title>

          <v-card-text>
            Department: <b>{{ employee.dept }}</b>
            <br>
            Position: <b>{{ employee.position }}</b>
          </v-card-text>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn to="/" flat>Back</v-btn>
            <v-btn @click="deleteEmployee" dark class="red">Delete</v-btn>
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
      employee: {
        employee_id: '',
        name: '',
        dept: '',
        position: ''
      }
    }
  },
  beforeRouteEnter (to, from, next) {
    db.collection('employees').where('employee_id', '==', to.params.employee_id).get()
      .then(querySnapshot => {
        querySnapshot.forEach(doc => {
          next(vm => {
            vm.employee.employee_id = doc.data().employee_id
            vm.employee.name = doc.data().name
            vm.employee.dept = doc.data().dept
            vm.employee.position = doc.data().position
          })
        })
      })
  },
  watch: {
    '$route': 'fetchData'
  },
  methods: {
    fetchData () {
      db.collection('employees').where('employee_id', '==', this.$route.params.employee_id).get()
        .then(querySnapshot => {
          querySnapshot.forEach(doc => {
            this.employee.employee_id = doc.data().employee_id
            this.employee.name = doc.data().name
            this.employee.dept = doc.data().dept
            this.employee.position = doc.data().position
          })
        })
    },
    deleteEmployee () {
      if (confirm('Are you sure?')) {
        db.collection('employees').where('employee_id', '==', this.$route.params.employee_id).get()
          .then(querySnapshot => {
            querySnapshot.forEach(doc => {
              doc.ref.delete()
              this.$router.push('/')
            })
          })
      }
    }
  }
}
</script>

<style>

</style>
