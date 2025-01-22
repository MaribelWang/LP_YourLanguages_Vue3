<template>
  <div class="container-fluid d-flex justify-content-center align-items-center vh-100">
    <div class="row w-100">
      <div class="col-md-6 d-flex flex-column justify-content-center text-center">
        <h1 class="fw-bold">Mininum cost to find the best tutor of languages nearby!</h1>
      </div>
      <div class="col-md-6 d-flex flex-column justify-content-center">
        <div class="card p-4 shadow-lg">
          <h3 class="text-primary text-center fw-bold">Login here</h3>
          <form @submit.prevent="login">
            <div class="mb-3">
              <input type="email" class="form-control" placeholder="Email" v-model="email" required>
            </div>
            <div class="mb-3">
              <input type="password" class="form-control" placeholder="Password" v-model="password" required>
            </div>
            <div class="text-danger" v-if="errorMessage">{{ errorMessage }}</div>
            <div class="text-end">
              <a href="#" class="text-primary">Forgot your password?</a>
            </div>
            <button class="btn btn-primary w-100">Sign in</button>
            <button class="btn btn-light w-100 mt-2" @click="navigateToRegister">Create new account</button>
          </form>
          <div class="text-center mt-3">
            <p>Or continue with</p>
            <div class="d-flex justify-content-center gap-2">
              <button class="btn btn-light">
                <i class="bi bi-google"></i>
              </button>
              <button class="btn btn-light">
                <i class="bi bi-wechat"></i>
              </button>
              <button class="btn btn-light">
                <i class="bi bi-apple"></i>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import axios from 'axios';

const router = useRouter();
const email = ref('');
const password = ref('');
const errorMessage = ref('');

const login = async () => {
  errorMessage.value = '';

  try {
    const response = await axios.post('https://reqres.in/api/login', {
      email: email.value,
      password: password.value
    });

    if (response.data.token) {
      // Save token to local storage
      localStorage.setItem('token', response.data.token);
      
// Redirect to home page
      router.push('/');
    }
  } catch (error) {
    errorMessage.value = 'Invalid email or password. Please try again.';
  }
};

const navigateToRegister = () => {
  router.push('/register');
};
</script>
