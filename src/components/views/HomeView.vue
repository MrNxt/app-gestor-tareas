<template>
    <div class="container mt-5">
      <div class="text-center">
        <h1 class="display-4 text-primary mb-4">Agrega tus tareas con la App de Alejr-dev</h1>
        <p class="lead text-secondary mb-4">
          Haz tus listas para poder cumplir con tus objetivos.<br>
          Add tus tareas de forma manual o desde una API. 
        </p>
        <img 
          src="https://cdn.pixabay.com/photo/2020/03/06/08/00/laptop-4906312_1280.jpg" 
          class="img-fluid mb-4 logo" 
          alt="Imagen de fondo" 
        />

        <h2 class="text-info mt-4">Secciones de la App</h2>
        <p class="text-muted">
            <strong>Añadir Tarea:</strong>Permite ingresar nuevas tareas manualmente al usuario. <br />
            <strong>Lista de Tareas:</strong>Muestra todas las tareas extraídas desde la API, permitiendo marcarlas como completadas o eliminarlas. <br />
            <strong>Vista Combinada:</strong>Combina las funcionalidades de añadir tareas manualmente y ver las tareas de la API al mismo tiempo.
        </p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "HomeView",
  };
  </script>
  
  <style scoped>
  .container {
    max-width: 900px;
  }
  
  .display-4 {
    font-weight: bold;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.2);
  }
  
  .lead {
    font-size: 1.25rem;
  }
  
  .logo {
    border-radius: 50%; 
    box-shadow: 0 0 20px rgba(6, 162, 139, 0.5);
    transition: transform 0.3s, box-shadow 0.3s; 
    max-width: 200px; 
  }
  
  .logo:hover {
    transform: scale(1.1); 
    box-shadow: 0 0 30px rgba(6, 162, 139, 0.5); 
  }
  
  h2 {
    font-weight: bold;
  }
  
  .text-muted {
    font-size: 1rem;
  }
  </style>