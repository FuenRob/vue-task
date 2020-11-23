<template>
    <div>
        <h1 class="display-4 text-center">Listado de Tareas</h1>
        <hr>
        <div class="row">
            <div class="col-lg-8 offset-lg-2">
                <div class="card mt-4">
                    <div class="card-body">
                        <div class="input-group">
                            <input type="text" v-model="task" class="form-control form-control-lg" placeholder="Agregar tarea">
                            <div class="input-group-append">
                                <button v-on:click="addTask()" class="btn btn-success btn-lg">Agregar</button>
                            </div>
                        </div>
                        <br>
                        <p v-if="listTask.length == 0">No hay tareas</p>
                        <ul class="list-group">
                            <li v-for="(task,index) of listTask" :key="index" class="list-group-item d-flex justify-content-between">
                                <span class="cursor" v-bind:class="{'text-success': task.completed}" v-on:click="completeTask(index, task)">
                                    <i v-bind:class="[task.completed ? 'far fa-check-circle' : 'far fa-circle']"></i>
                                </span>
                                <span v-bind:class="{'line-through': task.completed}">{{ task.name }}</span>
                                <span class="text-danger cursor" v-on:click="deleteTask(index)">
                                    <i class="fas fa-trash-alt"></i>
                                </span>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Task',
        data() {
            return{
                task: '',
                listTask: []
            }
        },
        methods: {
            addTask() {
                const taskObj = {
                    name: this.task,
                    completed: false
                }

                this.listTask.push(taskObj);
                this.task = '';
            },
            deleteTask(index) {
                this.listTask.splice(index, 1);
            },
            completeTask(index, task) {
                this.listTask[index].completed = !task.completed;
            }
        }
    }
</script>

<style scoped>
    .cursor{
        cursor: pointer;
    }
    .line-through{
        text-decoration:line-through;
    }
</style>