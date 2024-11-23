<template>
    <div class="container mt-4">
        <h1 class="title">Gestor de Tareas</h1>

        <div class="input-group mb-4">
            <input 
                v-model="newTask" 
                @keyup.enter="addTask" 
                placeholder="Escribe una nueva tarea..." 
                class="form-control task-input" 
                aria-label="Nueva tarea" 
            />
            <button @click="addTask" class="btn btn-success btn-add-task">Añadir</button>
        </div>

        <div v-if="tasks.length === 0" class="text-center text-muted">
            <p>No hay tareas pendientes. ¡Añade una!</p>
        </div>

        <div class="row mt-4" v-if="tasks.length > 0">
            <div class="col-12 mb-3" v-for="task in tasks" :key="task.id">
                <div class="card task-card">
                    <div class="card-body d-flex justify-content-between align-items-center">
                        <div class="flex-grow-1">
                            <h5 
                                class="card-title" 
                                :class="{ 'text-decoration-line-through': task.completed }">
                                {{ task.todo }}
                            </h5>
                            <span class="badge task-badge" 
                                :class="task.completed ? 'bg-success' : 'bg-warning'">
                                {{ task.completed ? 'Completada' : 'Pendiente' }}
                            </span>
                        </div>
                        <div class="d-flex">
                            <button 
                                @click="toggleTaskCompletion(task)" 
                                class="btn btn-outline-success me-2 btn-action" 
                                aria-label="Marcar como completada">
                                <i 
                                    :class="task.completed ? 'bi bi-check-circle-fill' : 'bi bi-check-circle'">
                                </i>
                            </button>
                            <button 
                                @click="deleteTask(task)" 
                                class="btn btn-outline-danger btn-action" 
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
export default {
    name: "AddTask",
    data() {
        return {
            newTask: "",
            tasks: [],
        };
    },
    methods: {
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
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        },
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },
    },
};
</script>

<style scoped>

.container {
    max-width: 700px;
    margin: 0 auto;
    padding: 20px;
    background-color: #f5f5f5;
    border-radius: 15px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}


.title {
    font-size: 2.2rem;
    font-weight: bold;
    text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.2);
    color: #4f9c46;
}

.task-input {
    border-radius: 25px;
    padding: 10px;
    transition: all 0.3s ease-in-out;
}

.task-input:focus {
    border-color: #0b8e93;
    box-shadow: 0 0 8px rgba(25, 135, 84, 0.5);
}

.btn-add-task {
    border-radius: 25px;
    padding: 10px 20px;
    background-color: #0b8e93;
    border: none;
    color: white;
    transition: background-color 0.3s ease-in-out;
}

.btn-add-task:hover {
    background-color: #155d40;
}

.task-card {
    border: none;
    border-radius: 10px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    background-color: #ffffff;
}

.card-title {
    font-size: 1.2rem;
    font-weight: bold;
    color: #343a40; 
}

.text-decoration-line-through {
    text-decoration: line-through;
    color: #999999;
}

.task-badge {
    font-size: 0.9rem;
    padding: 5px 10px;
    border-radius: 20px;
}

.btn-action {
    transition: all 0.2s ease-in-out;
}

.btn-action:hover {
    transform: scale(1.1);
}
</style>
