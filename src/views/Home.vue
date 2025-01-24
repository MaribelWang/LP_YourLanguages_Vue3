<template>
  <div class="container-fluid">
    <!-- Filters Section -->
    <div class="text-center mt-4">
      <h2>Look for tutors & teachers for your lessons</h2>
      <div class="d-flex justify-content-center gap-2 mt-3">
        <!-- All Button -->
        <button class="btn btn-outline-secondary">All</button>

        <!-- Subject Dropdown -->
        <div class="dropdown">
          <button
            class="btn btn-outline-secondary dropdown-toggle"
            type="button"
            id="subjectDropdown"
            data-bs-toggle="dropdown"
            aria-expanded="false"
          >
            Subject
          </button>
          <ul class="dropdown-menu" aria-labelledby="subjectDropdown">
            <li><a class="dropdown-item" href="#">Spanish</a></li>
            <li><a class="dropdown-item" href="#">English</a></li>
            <li><a class="dropdown-item" href="#">French</a></li>
          </ul>
        </div>

        <!-- Distance Dropdown -->
        <div class="dropdown">
          <button
            class="btn btn-outline-secondary dropdown-toggle"
            type="button"
            id="distanceDropdown"
            data-bs-toggle="dropdown"
            aria-expanded="false"
          >
            Distance
          </button>
          <ul class="dropdown-menu" aria-labelledby="distanceDropdown">
            <li><a class="dropdown-item" href="#">0-5 km</a></li>
            <li><a class="dropdown-item" href="#">5-10 km</a></li>
            <li><a class="dropdown-item" href="#">10-20 km</a></li>
          </ul>
        </div>

        <!-- Price Dropdown -->
        <div class="dropdown">
          <button
            class="btn btn-outline-secondary dropdown-toggle"
            type="button"
            id="priceDropdown"
            data-bs-toggle="dropdown"
            aria-expanded="false"
          >
            Price
          </button>
          <ul class="dropdown-menu" aria-labelledby="priceDropdown">
            <li><a class="dropdown-item" href="#">€0-€10</a></li>
            <li><a class="dropdown-item" href="#">€10-€20</a></li>
            <li><a class="dropdown-item" href="#">€20-€30</a></li>
          </ul>
        </div>

        <!-- Community Dropdown -->
        <div class="dropdown">
          <button
            class="btn btn-outline-secondary dropdown-toggle"
            type="button"
            id="communityDropdown"
            data-bs-toggle="dropdown"
            aria-expanded="false"
          >
            Location
          </button>
          <ul class="dropdown-menu" aria-labelledby="CityDropdown">
            <li><a class="dropdown-item" href="#">Barcelona</a></li>
            <li><a class="dropdown-item" href="#">Madrid</a></li>
            <li><a class="dropdown-item" href="#">Tarragona</a></li>
          </ul>
        </div>
      </div>
    </div>

    <!-- Tutor Cards -->
    <div class="container mt-4">
      <div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-4">
        <div v-for="(tutor, index) in tutors" :key="index" class="col">
          <div class="card shadow-sm">
            <div class="card-header bg-primary text-white d-flex align-items-center">
              <div
                class="rounded-circle bg-light me-3"
                style="width: 50px; height: 50px;"
              ></div>
              <div>
                <h5 class="mb-0">{{ tutor.name }}</h5>
                <p class="mb-0 small">⭐⭐⭐{{ tutor.rating }} ({{ tutor.reviews }} reviews)</p>
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

    <!-- About Us Section -->
    <section id="about-us" class="text-center mt-5 p-4 bg-light">
      <h3>Why Choose Your Languages?</h3>
      <p>
        Find the best tutors nearby! Learn languages face to face from
        experienced professionals with a minimum cost.
      </p>
      <p>
        We offer personalized lessons, flexible schedules, and a community of
        passionate learners.
      </p>
    </section>

    <!-- Pagination -->
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

// Mock data for tutors
const tutors = ref([
  {
    name: 'Hernan Fernandez',
    rating: 4.5,
    reviews: 41,
    class: 'Spanish',
    languages: ['Spanish', 'English', 'French'],
    location: 'Barcelona, Spain',
    price: 19,
    duration: 60,
    description: "I'm a Spanish teacher with 5 years of experience.",
  },
  {
    name: 'Jingwei Wang',
    rating: 4.9,
    reviews: 34,
    class: 'Chinese, English',
    languages: ['Spanish', 'English', 'Chinese'],
    location: 'Barcelona, Spain',
    price: 28,
    duration: 50,
    description: "I'm a Chinese and English teacher with years of experience.",
  },
  {
    name: 'Hernan Fernandez',
    rating: 4.5,
    reviews: 41,
    class: 'Catalan',
    languages: ['Spanish', 'English', 'French'],
    location: 'Barcelona, Spain',
    price: 19,
    duration: 60,
    description: "I'm a Spanish teacher with 5 years of experience.",
  },
]);

const totalPages = ref(5);
</script>
