<template>
<form @submit = "onSubmit">
    <input type="text" v-model="text">
    <input type ="text" name="date" v-model="day"> 
    <input type="checkbox" name = "reminder" v-model="reminder">
    <button type="submit">Add Task</button>
</form>
</template>
<script>
    export default{
        name: 'AddTask',
        data(){
            return{
                text: '',
                day: '',
                reminder: false,
            }
        },
        methods:{
            onSubmit(e){
                e.preventDefault()
                if(!this.text){
                    alert('Please Add A Task')
                    return
                }
                const newTask = {
                    id:Math.floor(Math.random() * 10000),
                    text: this.text,
                    day: this.day,
                    reminder: this.reminder

                }
                // console.log(newTask)
                this.$emit('add-task',newTask)
                //this thing will reset the inputs as defaults
                this.text = ''
                this.day = ''
                this.reminder = false
            }
        }
    }
</script>