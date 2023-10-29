<template>
  <div>
    <form @submit="onSubmit" class="add-form">
        <div class="inp">
            <input type="text" v-model="Name" name="Name" placeholder="Enter name">
        </div>
        <div class="inp">
            <input type="text" v-model="Division" name="Division" placeholder="Enter Division">
        </div>
        <div class="inp">
            <input type="text" v-model="Salary" name="Salary" placeholder="Enter Salary">
        </div>
        <div>
            <input type="submit" class="btn btn-info btn-block" name="save" >
        </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'Update',
  props: ['empId','empSal','empName','empDiv'],
  data(){
    return{
        Id: this.empId,
        Name: this.empName,
        Salary: this.empSal,
        Division: this.empDiv
    }
  },
  methods:{
    onSubmit(e){
        e.preventDefault()
        const updatedEmp = {
            Id: this.Id,
            Name: this.Name,
            Salary: parseInt(this.Salary),
            Division: this.Division
        }
        this.$emit('updated-task', updatedEmp)
    }
  }
}
</script>

<style scoped>
.add-form{
    margin-bottom: 40px;
    text-align: center;
}
.inp{
    margin: 20px 0;
}
label{
    display: block;
}
input{
    height: 40px;
    width: 430px;
    padding: 3px 7px;
    font-size: 17px;
    border: none;
    border-bottom: 1px solid black;
}
</style>