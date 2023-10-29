<template>
    <div class="container">
        <form @submit="onSubmit" class="add-form">
            <div class="inp">
                <input type="text" v-model="name" name="Name" placeholder="Enter name">
            </div>
            <div class="inp">
                <input type="text" v-model="division" name="Division" placeholder="Enter division">
            </div>
            <div class="inp">
                <input type="text" v-model="salary" name="Salary" placeholder="Enter salary">
            </div>
            <div>
                <input type="submit" class="btn btn-success" name="create">
            </div>
        </form>
    </div>
</template>

<script>
export default {
    name: "Create",
    data(){
        return{
            name:'',
            division:'',
            salary: 0
        }
    },
    methods: {
        onSubmit(e){
            e.preventDefault()
            const createdEmp = {
                name: this.name,
                division: this.division,
                salary: parseInt(this.salary)
            }
            console.log(createdEmp)
            this.$emit('created-task', createdEmp)
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
.container{
    border: 2px solid black;
    max-width: 500px;
}
</style>