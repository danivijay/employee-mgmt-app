<template>
  <v-container>
    <v-layout>
      <v-flex xs12 sm8 md6 offset-sm2 offset-md3>

        <v-card>
          <v-card-title>
            <h2>Edit Employee</h2>
          </v-card-title>

          <v-card-text>
            <v-form>
              <v-text-field
                label="Employee ID#"
                type="number"
                v-model="employee.employee_id"
                disabled
              ></v-text-field>
              <v-text-field
                label="Name"
                v-model="employee.name"
              ></v-text-field>
              <v-text-field
                label="Position"
                v-model="employee.position"
              ></v-text-field>
              <v-text-field
                label="Department"
                v-model="employee.dept"
              ></v-text-field>
            </v-form>
          </v-card-text>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn flat to="/">Back</v-btn>
            <v-btn dark class="orange" @click.prevent="onSubmit">Update</v-btn>
          </v-card-actions>
        </v-card>

      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import db from './firebaseinit'

export default {
  name: 'edit-employee',
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
    onSubmit () {
      db.collection('employees').where('employee_id', '==', this.$route.params.employee_id).get()
        .then(querySnapshot => {
          querySnapshot.forEach(doc => {
            doc.ref.update({
              employee_id: this.employee.employee_id,
              name: this.employee.name,
              dept: this.employee.dept,
              position: this.employee.position
            })
              .then(() => {
                this.$router.push({
                  name: 'view-employee',
                  params: {
                    employee_id: this.employee.employee_id
                  }
                })
              })
              .catch(err => console.log(err))
          })
        })
    }
  }
}
</script>

<style>

</style>
