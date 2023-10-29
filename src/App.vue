<template>
<div>
  <Button :text="showEmployees?'Hide':'Show'" @btn-clicked="toggleShowEmployees" :showEmployees="showEmployees"/>
  <div v-if="showEmployees">
    <Employee/>
  </div>
</div>
</template>

<script>
import Employee from './components/EmployeeView.vue'
import Button from './components/ButtonView.vue'
export default {
  name: "App",
  components: {Employee,Button},
  data(){
    return{
      showEmployees: false
    }
  },
  methods:{
    toggleShowEmployees(){
      this.showEmployees = !this.showEmployees
    },
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
