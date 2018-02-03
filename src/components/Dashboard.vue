<template>
  <v-layout row wrap>
      <v-flex xs12 sm8 md6 offset-sm2 offset-md3>

        <v-card>
          <v-toolbar color="white" class="mt-2 elevation-0">
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

          <v-divider></v-divider>

          <v-list two-line>
            <v-list-tile
              v-for="employee in employees"
              :to="{
                name: 'view-employee',
                params: {
                    employee_id: employee.employee_id
                  }
                }"
              :key="employee.id">

              <v-list-tile-content>
                <v-list-tile-title>
                  {{ employee.employee_id }}. {{ employee.name }}
                </v-list-tile-title>

                <v-list-tile-sub-title>
                  <v-chip>{{ employee.dept }}</v-chip> {{ employee.position }}
                </v-list-tile-sub-title>
              </v-list-tile-content>

            </v-list-tile>
          </v-list>
        </v-card>

      </v-flex>
  </v-layout>
</template>

<script>
import db from './firebaseinit'

export default {
  data () {
    return {
      employees: []
    }
  },
  created () {
    db.collection('employees').orderBy('dept').get()
      .then(querySnapshot => {
        querySnapshot.forEach(doc => {
          const data = {
            'id': doc.id,
            'employee_id': doc.data().employee_id,
            'name': doc.data().name,
            'dept': doc.data().dept,
            'position': doc.data().position
          }
          this.employees.push(data)
        })
      })
  }
}
</script>

<style>

</style>
