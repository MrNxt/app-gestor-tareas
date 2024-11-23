<template>
    <div class="container mt-4">
        <h1 class="h1">Lista de Tareas</h1>

        <div class="input-group mb-3">
            <input v-model="newTask" @keyup.enter="addTask" placeholder="Añadir nueva tarea"
                class="form-control task-input" aria-label="Nueva tarea" />
            <button @click="addTask" class="btn btn-custom">Añadir</button>
        </div>

        <div class="row mt-4">
            <div class="col-12 mb-4" v-for="task in tasks" :key="task.id">
                <div class="card task-card mb-3">
                    <div class="card-body d-flex justify-content-between align-items-center">
                        <div class="flex-grow-1 me-2">
                            <h5 class="card-title m-0" :class="{ 'text-decoration-line-through': task.completed }">
                                {{ task.todo }}
                            </h5>
                            <span class="badge"
                                :class="{ 'bg-custom-completed': task.completed, 'bg-custom-pending': !task.completed }">
                                {{ task.completed ? 'Completada' : 'Pendiente' }}
                            </span>
                        </div>
                        <div class="d-flex">
                            <button @click="toggleTaskCompletion(task)" class="btn btn-outline-custom me-2"
                                aria-label="Marcar como completada">
                                <i :class="task.completed ? 'bi bi-check-circle-fill' : 'bi bi-check-circle'"></i>
                            </button>
                            <button @click="deleteTask(task)" class="btn btn-outline-danger"
                                aria-label="Eliminar tarea">
                                <i class="bi bi-trash"></i>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "CombinedView",
    data() {
        return {
            newTask: "",
            tasks: [],
        };
    },
    created() {
        this.fetchTasks();
    },
    methods: {
        fetchTasks() {
            axios.get("https://dummyjson.com/todos")
                .then((response) => {
                    this.tasks = response.data.todos;
                })
                .catch((error) => {
                    console.error("Error fetching tasks:", error);
                });
        },
        addTask() {
            if (this.newTask.trim() === "") return;

            const newTask = {
                todo: this.newTask,
                completed: false,
                id: Date.now(),
            };

            this.tasks.unshift(newTask);
            this.newTask = "";
        },
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        },
    },
};
</script>

<style scoped>
.container {
    max-width: 800px;
    padding: 20px;
}

h1 {
    font-size: 2.5rem;
    font-weight: bold;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.3);
    color: #4f9c46
}

.task-input {
    border-radius: 25px;
    border: 2px solid #0b8e93;
    transition: box-shadow 0.3s, border-color 0.3s;
}

.task-input:focus {
    outline: none;
    box-shadow: 0 0 8px rgba(11, 142, 147, 0.6);
    border-color: #0b8e93;
}

.btn-custom {
    background-color: #0b8e93;
    border: none;
    color: white;
    border-radius: 25px;
    transition: background-color 0.3s ease;
}

.btn-custom:hover {
    background-color: #086b6f;
}

.card-title {
    font-weight: bold;
    overflow-wrap: break-word;
    max-height: 3em;
    overflow: hidden;
}

.task-card {
    border-radius: 15px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.text-decoration-line-through {
    text-decoration: line-through;
    color: #6c757d;
}

.bg-custom-completed {
    background-color: #28a745;
    color: white;
}

.bg-custom-pending {
    background-color: #ffc107;
    color: black;
}

.btn-outline-custom {
    border-color: #0b8e93;
    color: #0b8e93;
    transition: background-color 0.3s, color 0.3s;
}

.btn-outline-custom:hover {
    background-color: #0b8e93;
    color: white;
}
</style>
