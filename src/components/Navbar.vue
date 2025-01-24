<template>
     <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container">
      <!-- Add photo as logo -->
      <router-link class="navbar-brand d-flex align-items-center" to="/">
        <img src="../assets/logo_name.jpg" alt="Your Languages Logo" class="logo me-2" />
      </router-link>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item"><a class="nav-link" href="">About Us</a></li>
            <li class="nav-item"><a class="nav-link" href="">I'm a Tutor</a></li>
            <li class="nav-item"><a class="nav-link" href="">Impact</a></li>
            <li class="nav-item"><a class="nav-link" href="">Locations</a></li>
            <li class="nav-item"><a class="nav-link" href="/login">Login</a></li>
            <li class="nav-item"><a class="nav-link" href="/register">Register</a></li>
          </ul>
        </div>
      </div>
    </nav>
</template>

<style scoped>
.logo {
  height: 45px; 
  width: auto; 
}

.brand-name {
  font-weight: bold;
  font-size: 1.2rem; 
  color: #000; 
}

.navbar {
  padding: 0.5rem 1rem;
}

.container {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
