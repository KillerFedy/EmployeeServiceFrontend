<template>
  <div>
    <h1>Department Hierarchy</h1>
    <div v-if="departments.length > 0">
      <department-item v-for="(department, index) in departments" :key="index" :department="department"></department-item>
    </div>
    <div v-else>
      No departments found
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import DepartmentItem from './DepartmentItem.vue'

export default {
  name: 'DepartmentList',
  components: {
    DepartmentItem
  },
  data() {
    return {
      departments: [],
      isExpanded: false
    }
  },
  mounted() {
    this.getDepartments()
  },
  methods: {
    getDepartments() {
      axios.get('http://localhost:8080/departments')
        .then(response => {
          this.departments = response.data
        })
        .catch(error => {
          console.log(error)
        })
    }
  }
}
</script>
