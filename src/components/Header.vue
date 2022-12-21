<template>
    <header>
        <h1> {{ title }} </h1>
        <Button @btn-click="$emit('toggle-add-task')" 
        :text="showAddTasks ? 'Close' : 'Add Task'" 
        :color="showAddTasks ? 'red' : 'green'" />
    </header>
</template>
 
<script>
import Button from './Button.vue'

export default {
    name: 'Header',
    props: {
        title: String,
        showAddTasks: Boolean,
    },
    components: {
        Button,
    },

    // if default is needed:
    /* props: {
        title:{
            type: String,
            default: 'Hello world'
        }
    } */

}
</script>

<style scoped>
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}
</style>