<template>
    <table class="table">
        <thead>
            <tr>
            <th scope="col">ID</th>
            <th scope="col">Task</th>
            <th scope="col">Action</th>
            </tr>
        </thead>
        <tbody v-for="task in tasks" :key="task.id">
            <tr >
                <th scope="row">{{ task.id }}</th>
                <td v-on:click="getRowData (task.id)" class="table-row">{{ task.title }}</td>
                <td><button class="btn btn-danger" v-on:click="deleteTask(task.id)">Delete</button></td>
            </tr>
        </tbody>
    </table>
</template>

<script>
    export default {
        name : "task",
        props : {
            tasks : Array
        },
        data() {
            return {

            }
        },
        methods : {
            deleteTask (id) {
                this.$emit('getId', id);
            },
            getRowData(id) {
                var newtask = {};
                this.tasks.forEach(task => {
                    if (task.id === id) {
                        newtask = task;
                    }
                });
                this.$emit('getData', newtask);
            }
        }
    }
</script>

<style>
    .table-row {
        cursor : pointer
    }
</style>