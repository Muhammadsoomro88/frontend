<template>
<div v-if="employees && employees.length" class="container">
    <div>
      <h1>Employee page</h1>
      <button class="btn btn-primary" @click="toggleCreateUser">+ Create</button>
      <div v-if="createUser">
        <CreateEmp @created-task="addUser"/>
      </div>
    </div>
    <div v-for="employee in employees" :key="employee.id" :class="[employee.division === 'CAKE' ? 'cake' : 'dzoo', 'emp']">
      <h2>{{ employee.name }}</h2>
      <Image :division="employee.division"/>
      <h4><strong>$</strong>{{ employee.salary }}</h4>
      <div>
        <button class="btn btn-danger" @click="deleteUser(employee.id)">Delete</button>&nbsp;
        <button class="btn btn-success" @click="toggleUpdateUser">Update</button>
        <div v-if="updateUser">
          <UpdateEmp :empId="employee.id" :empSal="employee.salary" :empName="employee.name" :empDiv="employee.division" @updated-task="updateUserRecord"/>
        </div>
      </div>
    </div>
</div>
</template>

<script>
import axios from "axios";
import Image from './ImageView.vue'
import UpdateEmp from './UpdateEmp.vue'
import CreateEmp from './CreateEmp.vue'
export default {
  name: "Employee",
  components: {Image, UpdateEmp, CreateEmp},
  data() {
    return {
      employees: [],
      updateUser: false,
      createUser: false,
    }
  },
  methods:{
    async deleteUser(id){
      if (confirm('Are you sure?')) {
        const delResponse = await axios.delete(`http://localhost:8081/emp/${id}`)
        this.employees = delResponse.data
      }
    },
    toggleUpdateUser(){
      this.updateUser = !this.updateUser
    },
    toggleCreateUser(){
      this.createUser = !this.createUser
    },
    async updateUserRecord(emp){
      const updatedEmp = await axios.put(`http://localhost:8081/emp/${emp.Id}`,{
        name: emp.Name,
        division: emp.Division,
        salary: emp.Salary
      })
      this.employees = updatedEmp.data
    },
    async addUser(emp){
      const createdEmp = await axios.post(`http://localhost:8081/emp`,{
        name: emp.name,
        division: emp.division,
        salary: emp.salary
      })
      this.employees = createdEmp.data
      alert('User is added!')
      this.createUser = false
    }
  },
  async mounted() {
    const response = await axios.get("http://localhost:8081/emp")
    this.employees = response.data
  },
};
</script>

<style>
.container {
  border: 1px solid black;
  border-radius: 5px;
  margin: 30px auto;
  min-height: 300px;
  padding: 30px;
}
.emp{
  border: 1px solid gray;
  margin: 10px;
  padding: 10px;
  text-align: left;
}
.dzoo{
  border-left: 10px solid rgb(36, 234, 18)
}
.cake{
  border-left: 10px solid rgb(54, 178, 239)
}
</style>