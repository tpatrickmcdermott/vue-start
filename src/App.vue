<template>
  <div id="app" class="medium-container">
    <h1>Employees</h1>

    <employee-form @add:employee="addEmployee" />
    <employee-table
      v-bind:employees="employees"
      v-on:delete:employee="deleteEmployee"
      @edit:employee="editEmployee"
    />
    <!-- <employee-table v-bind:employees="employees" /> -->
  </div>
</template>

<script>

  import EmployeeTable from '@/components/EmployeeTable.vue';
  import EmployeeForm from '@/components/EmployeeForm.vue';

  export default {
    name: 'App',
    components: {
      EmployeeTable,
      EmployeeForm
    },
    methods: {
      addEmployee(employee) {
        const lastId =
          this.employees.length > 0
            ? this.employees[this.employees.length - 1].id
            : 0;
        const id = lastId + 1;
        const newEmployee = { ...employee, id };
        this.employees = [...this.employees, newEmployee];

        console.log(this);
        console.log(this.employees);
      },
      deleteEmployee(id) {
        this.employees = this.employees.filter(
          employee => employee.id !== id
        )
      },
      editEmployee(id, updatedEmployee) {
        this.employees = this.employees.map(employee =>
          employee.id === id ? updatedEmployee : employee
        )
      },
    },
    data() {
      return {
        employees: [
          {
            id: 1,
            name: 'Richard Hendricks',
            email: 'richard@piedpiper.com',
          },
          {
            id: 2,
            name: 'Bertram Gilfoyle',
            email: 'gilfoyle@piedpiper.com',
          },
          {
            id: 3,
            name: 'Dinesh Chugtai',
            email: 'dinesh@piedpiper.com',
          },
        ],
      }
    },
  }


</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
    max-width: 680px;
  }
</style>
