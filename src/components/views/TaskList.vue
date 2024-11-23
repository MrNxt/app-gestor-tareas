<template>
    <div class="container mt-4">
        <h1 class="text-center text-custom title mb-4">Lista de Tareas</h1>

        <button @click="fetchTasks" class="btn btn-custom-refresh mb-3">
            <i class="bi bi-arrow-clockwise me-2"></i>Cargar Tareas
        </button>

        <div class="row">
            <div class="col-12 mb-4" v-for="task in tasks" :key="task.id">
                <TodoItem :title="task.todo" :completed="task.completed" @toggle-completion="toggleTaskCompletion(task)"
                    @delTodo="deleteTask(task)" />
            </div>
        </div>
    </div>
</template>

<script>
import TodoItem from "@/components/TodoItem.vue";
import axios from "axios";

export default {
    name: "TaskList",
    components: { TodoItem },
    data() {
        return {
            tasks: [],
        };
    },
    methods: {
        fetchTasks() {
            axios
                .get("https://dummyjson.com/todos")
                .then((response) => {
                    this.tasks = response.data.todos;
                })
                .catch((error) => {
                    console.error("Error fetching tasks:", error);
                });
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
    background-color: #f9f9f9;
    border-radius: 15px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.title {
    font-size: 2.5rem;
    font-weight: bold;
    color: #0b8e93;
    text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.2);
    margin-bottom: 30px;
}

.btn-custom-refresh {
    background-color: #0b8e93;
    color: white;
    border: none;
    border-radius: 25px;
    padding: 10px 20px;
    transition: background-color 0.3s ease, box-shadow 0.3s ease;
}

.btn-custom-refresh:hover {
    background-color: #086b6f;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
}
</style>
