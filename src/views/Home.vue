<template>
  <div class="container-fluid">
    <!-- Filters Section -->
    <div class="text-center mt-4">
      <h2>Look for tutors & teachers for your lessons</h2>
      <div class="filters-container mt-4">
        <button class="btn btn-outline-secondary filter-btn" @click="resetFilters">All</button>

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
            <li><a class="dropdown-item" href="#" @click.prevent="filterBySubject('Spanish')">Spanish</a></li>
            <li><a class="dropdown-item" href="#" @click.prevent="filterBySubject('English')">English</a></li>
            <li><a class="dropdown-item" href="#" @click.prevent="filterBySubject('French')">French</a></li>
          </ul>
        </div>

        <!-- Location Dropdown -->
        <div class="dropdown">
          <button
            class="btn btn-outline-secondary filter-btn dropdown-toggle"
            type="button"
            id="communityDropdown"
            data-bs-toggle="dropdown"
            aria-expanded="false"
          >
            Location
          </button>
          <ul class="dropdown-menu" aria-labelledby="communityDropdown">
            <li><a class="dropdown-item" href="#" @click.prevent="filterByLocation('Barcelona')">Barcelona</a></li>
          
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
            <li><a class="dropdown-item" href="#" @click.prevent="filterByDistance('0-5 km')">0-5 km</a></li>
            <li><a class="dropdown-item" href="#" @click.prevent="filterByDistance('5-10 km')">5-10 km</a></li>
            <li><a class="dropdown-item" href="#" @click.prevent="filterByDistance('10-20 km')">10-20 km</a></li>
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
            <li><a class="dropdown-item" href="#" @click.prevent="filterByPrice(10, 20)">€10-€20</a></li>
            <li><a class="dropdown-item" href="#" @click.prevent="filterByPrice(20, 30)">€20-€30</a></li>
            <li><a class="dropdown-item" href="#" @click.prevent="filterByPrice(30, 40)">€30-€40</a></li>
          </ul>
        </div>
      </div>
    </div>

    <!-- Tutor Cards Section -->
    <div class="container mt-4">
      <div class="row g-4">
        <div v-for="(tutor, index) in paginatedTutors" :key="index" class="col-12 col-md-6 col-lg-4">
          <div class="card shadow-sm h-100">
            <div class="card-header bg-primary text-white d-flex align-items-center">
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
          <li class="page-item" :class="{ disabled: currentPage === 1 }">
            <a class="page-link" href="#" @click.prevent="prevPage">«</a>
          </li>
          <li
            v-for="page in totalPages"
            :key="page"
            class="page-item"
            :class="{ active: currentPage === page }"
          >
            <a class="page-link" href="#" @click.prevent="changePage(page)">{{ page }}</a>
          </li>
          <li class="page-item" :class="{ disabled: currentPage === totalPages }">
            <a class="page-link" href="#" @click.prevent="nextPage">»</a>
          </li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
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
    location: 'Barcelona',
    price: 19,
    duration: 60,
    description: "I'm a Spanish teacher with 5 years of experience.",
    avatar: avatar1,
  },
    {
    name: 'Hernan Fernandez',
    rating: 4.5,
    reviews: 41,
    class: 'Spanish',
    languages: ['Spanish', 'English', 'French'],
    location: 'Barcelona',
    price: 19,
    duration: 60,
    description: "I'm a Spanish teacher with 5 years of experience.",
    avatar: avatar1,
  },  {
    name: 'Hernan Fernandez',
    rating: 4.5,
    reviews: 41,
    class: 'Spanish',
    languages: ['Spanish', 'English', 'French'],
    location: 'Barcelona',
    price: 19,
    duration: 60,
    description: "I'm a Spanish teacher with 5 years of experience.",
    avatar: avatar1,
  },  {
    name: 'Hernan Fernandez',
    rating: 4.5,
    reviews: 41,
    class: 'Spanish',
    languages: ['Spanish', 'English', 'French'],
    location: 'Barcelona',
    price: 19,
    duration: 60,
    description: "I'm a Spanish teacher with 5 years of experience.",
    avatar: avatar1,
  },
  {
    name: 'Jingwei Wang',
    rating: 4.9,
    reviews: 34,
    class: 'English',
    languages: ['Spanish', 'English', 'Chinese'],
    location: 'Tarragona',
    price: 28,
    duration: 50,
    description: "I'm a Chinese and English teacher with years of experience.",
    avatar: avatar2,
  },
  {
    name: 'David Muñoz',
    rating: 4.7,
    reviews: 29,
    class: 'French',
    languages: ['French', 'English', 'Spanish'],
    location: 'Barcelona',
    price: 22,
    duration: 45,
    description: "Teaching French with passion for over a decade.",
    avatar: avatar3,
  },
    {
    name: 'David Muñoz',
    rating: 4.7,
    reviews: 29,
    class: 'French',
    languages: ['French', 'English', 'Spanish'],
    location: 'Barcelona',
    price: 29,
    duration: 45,
    description: "Teaching French with passion for over a decade.",
    avatar: avatar3,
  },
     {
    name: 'David Muñoz',
    rating: 4.7,
    reviews: 29,
    class: 'French',
    languages: ['French', 'English', 'Spanish'],
    location: 'Barcelona',
    price: 39,
    duration: 45,
    description: "Teaching French with passion for over a decade.",
    avatar: avatar3,
  },
     {
    name: 'David Muñoz',
    rating: 4.7,
    reviews: 29,
    class: 'French',
    languages: ['French', 'English', 'Spanish'],
    location: 'Barcelona',
    price: 22,
    duration: 45,
    description: "Teaching French with passion for over a decade.",
    avatar: avatar3,
  },
     {
    name: 'David Muñoz',
    rating: 4.7,
    reviews: 29,
    class: 'French',
    languages: ['French', 'English', 'Spanish'],
    location: 'Barcelona',
    price: 38,
    duration: 45,
    description: "Teaching French with passion for over a decade.",
    avatar: avatar3,
  },
    {
    name: 'Jingwei Wang',
    rating: 4.9,
    reviews: 34,
    class: 'English',
    languages: ['Spanish', 'English', 'Chinese'],
    location: 'Tarragona',
    price: 37,
    duration: 50,
    description: "I'm a Chinese and English teacher with years of experience.",
    avatar: avatar2,
  },
    {
    name: 'Jingwei Wang',
    rating: 4.9,
    reviews: 34,
    class: 'English',
    languages: ['Spanish', 'English', 'Chinese'],
    location: 'Tarragona',
    price: 28,
    duration: 50,
    description: "I'm a Chinese and English teacher with years of experience.",
    avatar: avatar2,
  },
    {
    name: 'Jingwei Wang',
    rating: 4.9,
    reviews: 34,
    class: 'English',
    languages: ['Spanish', 'English', 'Chinese'],
    location: 'Tarragona',
    price: 28,
    duration: 50,
    description: "I'm a Chinese and English teacher with years of experience.",
    avatar: avatar2,
  },  {
    name: 'Jingwei Wang',
    rating: 4.9,
    reviews: 34,
    class: 'English',
    languages: ['Spanish', 'English', 'Chinese'],
    location: 'Tarragona',
    price: 28,
    duration: 50,
    description: "I'm a Chinese and English teacher with years of experience.",
    avatar: avatar2,
  },  {
    name: 'Jingwei Wang',
    rating: 4.9,
    reviews: 34,
    class: 'English',
    languages: ['Spanish', 'English', 'Chinese'],
    location: 'Tarragona',
    price: 28,
    duration: 50,
    description: "I'm a Chinese and English teacher with years of experience.",
    avatar: avatar2,
  },
]);



// Pagination state
const currentPage = ref(1);
const itemsPerPage = 6;

const totalPages = computed(() => Math.ceil(filteredTutors.value.length / itemsPerPage));

const paginatedTutors = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage;
  const end = start + itemsPerPage;
  return filteredTutors.value.slice(start, end);
});

// Filter state
const filters = ref({
  subject: null,
  location: null,
  price: { min: null, max: null },
});
const filteredTutors = computed(() => {
  return tutors.value.filter((tutor) => {
    const matchesSubject = !filters.value.subject || tutor.class === filters.value.subject;
    const matchesLocation = !filters.value.location || tutor.location === filters.value.location;
    const matchesPrice =
      (filters.value.price.min === null || tutor.price >= filters.value.price.min) &&
      (filters.value.price.max === null || tutor.price <= filters.value.price.max);

    return matchesSubject && matchesLocation && matchesPrice;
  });
});
const filterBySubject = (subject) => {
  filters.value.subject = subject;
  currentPage.value = 1;
};

const filterByLocation = (location) => {
  filters.value.location = location;
  currentPage.value = 1;
};

const filterByPrice = (min, max) => {
  filters.value.price = { min, max };
  currentPage.value = 1;
};

const resetFilters = () => {
  filters.value = { subject: null, location: null, price: { min: null, max: null } };
  currentPage.value = 1;
};

// Pagination functions
const changePage = (page) => {
  if (page >= 1 && page <= totalPages.value) {
    currentPage.value = page;
  }
};

const nextPage = () => {
  if (currentPage.value < totalPages.value) {
    currentPage.value++;
  }
};

const prevPage = () => {
  if (currentPage.value > 1) {
    currentPage.value--;
  }
};
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
   min-height: 700px; 
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