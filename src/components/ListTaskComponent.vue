<template>
    <h1>List task</h1>
    <task 
    v-bind:tasks="tasks"
    v-on:getData="getData"
    v-on:getId="getId"/>
</template>

<script>
    import Task from "./TaskComponent.vue";
    export default {
        name : "list-task",
        props : {
            tasks : Array
        },
        components : {
            Task,
        },
        data() {
            return {
            }
        },
        methods : {
            getData(data) {
                this.$emit('getDataUpdate', data);
            },
            getId(data) {
                this.$emit('getIdDelete', data);
            }
        }
    }
</script>

<style>
</style>