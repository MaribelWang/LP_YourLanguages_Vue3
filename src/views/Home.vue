<template>
  <div class="container-fluid">
    <!-- Navbar -->
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container">
        <a class="navbar-brand fw-bold" href="#">Your Languages</a>
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

    <!--Filters section-->
    <div class="text-center mt-4">
      <h2>Look for tutors & teachers for your lessons</h2>
      <div class="d-flex justify-content-center gap-2 mt-3">
        <button class="btn btn-outline-secondary">All</button>
        <button class="btn btn-outline-secondary">Subject ▼</button>
        <button class="btn btn-outline-secondary">Distance ▼</button>
        <button class="btn btn-outline-secondary">Price ▼</button>
        <button class="btn btn-outline-secondary">Community ▼</button>
      </div>
    </div>

    <!-- Tutor Cards-->
    <div class="container mt-4">
      <div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-4">
        <div v-for="(tutor, index) in tutors" :key="index" class="col">
          <div class="card shadow-sm">
            <div class="card-header bg-primary text-white d-flex align-items-center">
              <div class="rounded-circle bg-light me-3" style="width: 50px; height: 50px;"></div>
              <div>
                <h5 class="mb-0">{{ tutor.name }}</h5>
                <p class="mb-0 small">⭐⭐⭐{ tutor.rating }} ({{ tutor.reviews }} reviews)</p>
              </div>
            </div>
            <div class="card-body">
              <p><strong>Class:</strong> {{ tutor.class }}</p>
              <p><strong>Speaks:</strong> {{ tutor.languages.join(', ') }}</p>
              <p><strong>Location:</strong> {{ tutor.location }}</p>
              <p class="fw-bold">€{{ tutor.price }} / {{ tutor.duration }} mins class</p>
              <p>{{ tutor.description }}</p>
              <a href="#" class="text-primary">More details...</a>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- page 1-5-->
    <div class="d-flex justify-content-center mt-4">
      <nav aria-label="Page navigation">
        <ul class="pagination">
          <li class="page-item"><a class="page-link" href="#">«</a></li>
          <li v-for="page in totalPages" :key="page" class="page-item">
            <a class="page-link" href="#">{{ page }}</a>
          </li>
          <li class="page-item"><a class="page-link" href="#">»</a></li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// Mockdata of tutors
const tutors = ref([
  { name: 'Hernan Fernandez', rating: 4.5, reviews: 41, class: 'Spanish', languages: ['Spanish', 'English', 'French'], location: 'Barcelona, Spain', price: 19, duration: 60, description: "I'm a Spanish teacher with 5 years of experience." },
  { name: 'Jingwei Wang', rating: 4.9, reviews: 34, class: 'Chinese, English', languages: ['Spanish', 'English', 'Chinese'], location: 'Barcelona, Spain', price: 28, duration: 50, description: "I'm a Chinese and English teacher with years of experience." },
  { name: 'Hernan Fernandez', rating: 4.5, reviews: 41, class: 'Catalan', languages: ['Spanish', 'English', 'French'], location: 'Barcelona, Spain', price: 19, duration: 60, description: "I'm a Spanish teacher with 5 years of experience." },
]);

const totalPages = ref(5);
</script>
