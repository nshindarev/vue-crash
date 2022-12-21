<template>
    <header>
        <h1> {{ title }} </h1>
        <Button v-show="homePage" @btn-click="$emit('toggle-add-task')" :text="showAddTasks ? 'Close' : 'Add Task'"
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

    computed: {
        homePage() {
            if (this.$route.path === '/') {
                return true
            } else {
                return false
            }
        },
    }

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