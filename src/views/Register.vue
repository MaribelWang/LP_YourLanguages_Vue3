<template>
  <div class="container-fluid d-flex justify-content-center align-items-center vh-100">
    <div class="row w-100">
      <div class="col-md-6 d-flex flex-column justify-content-center text-center">
        <h1 class="fw-bold">Welcome back to where you strive yourself!</h1>
      </div>
      <div class="col-md-6 d-flex flex-column justify-content-center">
        <div class="card p-4 shadow-lg">
          <h3 class="text-primary text-center fw-bold">Create Account</h3>
          <form @submit.prevent="register">
            <div class="mb-3">
              <input type="email" class="form-control" placeholder="Email" v-model="email" required>
            </div>
            <div class="mb-3">
              <input type="text" class="form-control" placeholder="First Name" v-model="firstName" required>
            </div>
            <div class="mb-3">
              <input type="text" class="form-control" placeholder="Last Name" v-model="lastName" required>
            </div>
            <div class="mb-3">
              <input type="password" class="form-control" placeholder="Password" v-model="password" required>
            </div>
            <div class="mb-3">
              <input type="password" class="form-control" placeholder="Confirm Password" v-model="confirmPassword" required>
            </div>
            <button class="btn btn-primary w-100">Sign up</button>
            <button class="btn btn-light w-100 mt-2" @click="navigateToLogin">Already have an account</button>
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

const router = useRouter();
const email = ref('');
const firstName = ref('');
const lastName = ref('');
const password = ref('');
const confirmPassword = ref('');

const register = () => {
  if (password.value !== confirmPassword.value) {
    alert('Passwords do not match');
    return;
  }
  alert(`Registering ${firstName.value} ${lastName.value}`);
};

const navigateToLogin = () => {
  router.push('/login');
};
</script>
