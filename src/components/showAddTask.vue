<template>
    <div class="" v-if="showAddTask">
        <AddTask />
    </div>
</template>
<script>
import AddTask from './AddTask.vue'
export default {
   name:'showAddTask',
   components:{
       AddTask,
   }
}
</script>
