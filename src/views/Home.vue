<template>
    <AddTask v-show="showAddTasks" @add-task="onAddTask" />
    <Tasks @toggle-reminder="toggleReminder" 
    @delete-task="deleteTask" 
    :tasks="tasks" 
    />
</template>

<script>
import Tasks from '../components/Tasks'
import AddTask from '../components/AddTask.vue'
export default {
    name: 'Home',
    components: { Tasks, AddTask },
    data() {
        return {
            tasks: [],
        }
    },
    props:{
        showAddTasks: Boolean
    },
    methods: {
        async deleteTask(id) {
            if (confirm('Are you sure?')) {
                const res = await fetch(`api/tasks/${id}`, {
                    method: 'DELETE'
                })
                res.status === 200 ? (this.tasks = this.tasks.filter((task) => { return task.id !== id }))
                    : alert('Error deleting tasks')
            }
        },

        async toggleReminder(id) {
            console.log(id);

            const taskToToggle = await this.fetchTask(id);
            const updTask = { ...taskToToggle, reminder: !taskToToggle.reminder }

            console.log({ taskToToggle, updTask });

            const res = await fetch(`/api/tasks/${id}`, {
                method: 'PUT',
                headers: {
                    'Content-type': 'application/json',
                },
                body: JSON.stringify(updTask),
            })

            const data = await res.json()

            this.tasks = this.tasks.map((task) =>
                task.id === id ? { ...task, reminder: data.reminder } : task)
        },

        async onAddTask(task) {
            const res = await fetch(`/api/tasks/`, {
                method: 'POST',
                headers: {
                    'Content-type': 'application/json',
                },
                body: JSON.stringify(task),
            })

            const data = await res.json()

            this.tasks = [...this.tasks, data];
        },

        async fetchTasks() {
            const res = await fetch('/api/tasks');
            const data = await res.json()

            return data;
        },

        async fetchTask(id) {
            const res = await fetch(`/api/tasks/${id}`);
            const data = await res.json()

            return data;
        }
    },
    async created() {
        this.tasks = await this.fetchTasks();
    }
}


</script>