<template>
  <div class="container-fluid d-flex justify-content-center align-items-center vh-100">
    <div class="row w-100">
      <div class="col-md-6 d-flex flex-column justify-content-center text-center">
        <h1 class="fw-bold">Welcome back to where you strive yourself!</h1>
      </div>
      <div class="col-md-6 d-flex flex-column justify-content-center">
        <div class="card p-4 shadow-lg">
          <h3 class="text-primary text-center fw-bold">Create Account</h3>
          <form @submit.prevent="handleFormSubmit">
            <div class="mb-3">
              <input
                v-model="values.email"
                type="email"
                class="form-control"
                placeholder="Email"
              />
              <span v-if="errors.email" class="text-danger">{{ errors.email }}</span>
            </div>
            <div class="mb-3">
              <input
                v-model="values.firstName"
                type="text"
                class="form-control"
                placeholder="First Name"
              />
              <span v-if="errors.firstName" class="text-danger">{{ errors.firstName }}</span>
            </div>
            <div class="mb-3">
              <input
                v-model="values.lastName"
                type="text"
                class="form-control"
                placeholder="Last Name"
              />
              <span v-if="errors.lastName" class="text-danger">{{ errors.lastName }}</span>
            </div>
            <div class="mb-3">
              <input
                v-model="values.password"
                type="password"
                class="form-control"
                placeholder="Password"
              />
              <span v-if="errors.password" class="text-danger">{{ errors.password }}</span>
            </div>
            <div class="mb-3">
              <input
                v-model="values.confirmPassword"
                type="password"
                class="form-control"
                placeholder="Confirm Password"
              />
              <span v-if="errors.confirmPassword" class="text-danger">
                {{ errors.confirmPassword }}
              </span>
            </div>
            <p v-if="errorMessage" class="text-danger text-center">{{ errorMessage }}</p>
            <p v-if="successMessage" class="text-success text-center">{{ successMessage }}</p>
            <button type="submit" class="btn btn-primary w-100">Sign up</button>
            <button
              type="button"
              class="btn btn-light w-100 mt-2"
              @click.prevent="navigateToLogin"
            >
              Already have an account
            </button>
          </form>
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


const router = useRouter();


const schema = yup.object({
  email: yup.string().email('Please enter a valid email').required('Email is required'),
  firstName: yup.string().required('First Name is required'),
  lastName: yup.string().required('Last Name is required'),
  password: yup
    .string()
    .min(6, 'Password must be at least 6 characters')
    .required('Password is required'),
  confirmPassword: yup
    .string()
    .oneOf([yup.ref('password')], 'Passwords must match')
    .required('Confirm Password is required'),
});


const { handleSubmit, values, errors } = useForm({
  validationSchema: schema,
});

const errorMessage = ref('');
const successMessage = ref('');
const loading = ref(false);


const handleFormSubmit = handleSubmit(async () => {
  errorMessage.value = '';
  successMessage.value = '';
  loading.value = true;

  try {
    const response = await axios.post('https://reqres.in/api/register', {
      email: values.email,
      password: values.password,
    });

    if (response.data.token) {
      successMessage.value = 'Registration successful! Redirecting...';
      localStorage.setItem('token', response.data.token);

      setTimeout(() => {
        router.push('/');
      }, 2000);
    }
  } catch (error) {
    errorMessage.value = 'Registration failed. Please try again.';
  } finally {
    loading.value = false;
  }
});

const navigateToLogin = () => {
  router.push('/login');
};
</script>
