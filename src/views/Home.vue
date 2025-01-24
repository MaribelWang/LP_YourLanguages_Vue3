<template>
  <div class="container-fluid">
    <!-- Filters Section -->
    <div class="text-center mt-4">
      <h2>Look for tutors & teachers for your lessons</h2>
      <div class="filters-container mt-4">
        <button class="btn btn-outline-secondary filter-btn">All</button>

        <!-- Subject Dropdown -->
        <div class="dropdown">
          <button
            class="btn btn-outline-secondary filter-btn dropdown-toggle"
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
            class="btn btn-outline-secondary filter-btn dropdown-toggle"
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
            class="btn btn-outline-secondary filter-btn dropdown-toggle"
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
            class="btn btn-outline-secondary filter-btn dropdown-toggle"
            type="button"
            id="communityDropdown"
            data-bs-toggle="dropdown"
            aria-expanded="false"
          >
            Community
          </button>
          <ul class="dropdown-menu" aria-labelledby="communityDropdown">
            <li><a class="dropdown-item" href="#">Students</a></li>
            <li><a class="dropdown-item" href="#">Teachers</a></li>
            <li><a class="dropdown-item" href="#">Parents</a></li>
          </ul>
        </div>
      </div>
    </div>

    <!-- Tutor Cards Section -->
    <div class="container mt-4">
      <div class="row g-4">
        <div v-for="(tutor, index) in tutors" :key="index" class="col-12 col-md-6 col-lg-4">
          <div class="card shadow-sm h-100">
            <div class="card-header bg-primary text-white d-flex align-items-center">
              <!-- Avatar -->
              <img
                :src="tutor.avatar"
                alt="Tutor Avatar"
                class="rounded-circle me-3 avatar"
              />
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

    <!-- Pagination Section -->
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
import avatar1 from '../assets/avatar1.png';
import avatar2 from '../assets/avatar2.png';
import avatar3 from '../assets/avatar3.png';

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
    avatar: avatar1,
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
    avatar: avatar2,
  },
  {
    name: 'David muñoz',
    rating: 4.5,
    reviews: 41,
    class: 'Catalan',
    languages: ['Spanish', 'English', 'French'],
    location: 'Barcelona, Spain',
    price: 19,
    duration: 60,
    description: "I'm a Spanish teacher with 5 years of experience.",
    avatar: avatar3,
  },
]);


const totalPages = ref(5);
</script>

<style scoped>
.filters-container {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  margin: 0 auto;
  max-width: 100%;
}

.filter-btn {
  min-width: 150px;
  text-align: center;
}

.dropdown-menu {
  min-width: 150px;
  text-align: center;
  border-radius: 5px;
  box-shadow: none;
}

.container {
  margin-top: 30px;
}

.row {
  display: flex;
  justify-content: center;
}

.card {
  transition: transform 0.2s;
}

.card:hover {
  transform: scale(1.05);
}

.card-header {
  font-weight: bold;
  display: flex;
  align-items: center;
}

.avatar {
  width: 50px;
  height: 50px;
  object-fit: cover;
  border: 2px solid white;
}

h2 {
  margin-bottom: 20px;
  font-weight: 700;
  text-align: center;
}

.pagination {
  margin-top: 20px;
}
</style>

