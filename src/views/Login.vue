<template>
  <div class="container-fluid d-flex justify-content-center align-items-center vh-100">
    <div class="row w-100">
      <div class="col-md-6 d-flex flex-column justify-content-center text-center">
        <h1 class="fw-bold">Minimum cost to find the best tutor of languages nearby!</h1>
      </div>
      <div class="col-md-6 d-flex flex-column justify-content-center">
        <div class="card p-4 shadow-lg">
          <h3 class="text-primary text-center fw-bold">Login here</h3>
          <form @submit.prevent="handleFormSubmit">
            <div class="mb-3">
              <input
                v-model="email"
                type="email"
                class="form-control"
                placeholder="Email"
              />
              <span v-if="emailError" class="text-danger">{{ emailError }}</span>
            </div>
            <div class="mb-3">
              <input
                v-model="password"
                type="password"
                class="form-control"
                placeholder="Password"
              />
              <span v-if="passwordError" class="text-danger">{{ passwordError }}</span>
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
import { useForm, useField } from 'vee-validate';
import * as yup from 'yup';
import axios from 'axios';

// Vue Router
const router = useRouter();

// Validation schema
const schema = yup.object({
  email: yup.string().email('Please enter a valid email').required('Email is required'),
  password: yup.string().required('Password is required'),
});

// VeeValidate form setup
const { handleSubmit } = useForm({
  validationSchema: schema,
});

// Fields setup
const { value: email, errorMessage: emailError } = useField('email');
const { value: password, errorMessage: passwordError } = useField('password');

// Error messages
const errorMessage = ref('');

// Form submission handler
const handleFormSubmit = handleSubmit(async () => {
  errorMessage.value = '';

  try {
    const response = await axios.post('https://reqres.in/api/login', {
      email: email.value,
      password: password.value,
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
});

// Navigate to register page
const navigateToRegister = () => {
  router.push('/register');
};
</script>
