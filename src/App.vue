<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-dark bg-custom shadow">
      <div class="container">
        <router-link class="navbar-brand d-flex align-items-center" to="/">
          <img src="/src/assets/vue.svg" alt="Vue logo" width="30" height="30" class="d-inline-block align-top me-2" />
          Gestor de Tareas by Alejr-dev
        </router-link>

        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item">
              <router-link class="nav-link d-flex align-items-center" to="/addtask">
                <i class="bi bi-plus-circle me-2"></i>Añadir Tarea
              </router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link d-flex align-items-center" to="/tasklist">
                <i class="bi bi-card-list me-2"></i>Lista de Tareas
              </router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link d-flex align-items-center" to="/combined">
                <i class="bi bi-grid me-2"></i>Vista Combinada
              </router-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: 'Poppins', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #0b8e93;
}

.navbar {
  background-color: #0b8e93;
  padding: 15px 20px;
  border-radius: 8px;
}

.navbar-brand {
  font-size: 1.2rem;
  font-weight: 600;
}

.nav-link {
  font-weight: 500;
  font-size: 1rem;
  color: white;
  transition: all 0.3s ease;
}

.nav-link:hover {
  color: #f8f9fa;
}

.nav-link.router-link-exact-active {
  color: #ffd700;
  text-decoration: underline;
}

.navbar-toggler {
  border: none;
}

.shadow {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}
</style>
