<template>
  <div>
    <h5>
      <button @click="isExpanded = !isExpanded">
        {{ department.departmentName }}
        <i :class="{'fa fa-caret-down': isExpanded, 'fa fa-caret-right': !isExpanded}"></i>
      </button>
    </h5>
    <ul v-show="isExpanded">
      <li v-for="(employee, index) in department.employees" :key="index">{{ employee.name }} - {{ employee.position }}</li>
    </ul>
    <div v-show="isExpanded && department.childDepartments.length > 0">
      <department-item v-for="(childDepartment, index) in department.childDepartments" :key="index" :department="childDepartment"></department-item>
    </div>
  </div>
</template>


<button @click="toggleExpand">
  {{ department.departmentName }}
  <i :class="{'fa fa-caret-down': isExpanded, 'fa fa-caret-right': !isExpanded}"></i>
</button>

<script>
import DepartmentItem from './DepartmentItem.vue'

export default {
  name: 'DepartmentItem',
  components: {
    DepartmentItem
  },
  props: {
    department: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      isExpanded: false
    }
  },
  methods: {
    toggleExpand() {
      this.isExpanded = !this.isExpanded
    }
  }
}
</script>