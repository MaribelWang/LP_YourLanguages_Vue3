# YourLanguages Landing Page

## Overview

The **YourLanguages Landing Page** is a responsive web application built with Vue 3 to provide a modern and engaging platform for language learners and tutors. The landing page includes functionalities for user registration, login, and navigation between different sections with a clean and visually appealing design.

---

## Features

- **Responsive Design**: Optimized for various screen sizes using Bootstrap.
- **User Authentication**: Registration and login forms with validation.
- **Vue Router Integration**: Smooth navigation between pages.
- **Advanced Form Validation**: Built with VeeValidate and Yup.
- **Page Transitions**: Elegant fade animations during navigation.
- **Reusable Components**: Modularized Navbar and Footer for easy scalability.

---

## Technologies Used

- **Frontend Framework**: Vue 3
- **CSS Framework**: Bootstrap 5
- **Form Validation**: VeeValidate and Yup
- **Routing**: Vue Router
- **HTTP Client**: Axios

---

## Pages

### 1. Home Page

- Displays a welcome message and information about the platform.
- Includes buttons for navigating to the Login and Registration pages.

### 2. Registration Page

- Allows users to create an account.
- Validates user inputs:
  - **Email**: Must be valid.
  - **Password**: Minimum 6 characters.
  - **Confirm Password**: Must match the password.
- Displays appropriate error messages for invalid inputs.

### 3. Login Page

- Enables existing users to log in.
- Validates user inputs for email and password.
- Redirects to the Home Page upon successful login.

---

## Installation

### Prerequisites

- Node.js and npm installed on your system.

### Steps

1. Clone the repository:

   ```bash
   git clone https://github.com/yourusername/LP_YourLanguages_Vue3.git
   ```

2. Navigate to the project directory:

   ```bash
   cd LP_YourLanguages_Vue3
   ```

3. Install dependencies:

   ```bash
   npm install
   ```

4. Start the development server:

   ```bash
   npm run dev
   ```

5. Open the app in your browser at `http://localhost:5173` (default Vite port).

---

## Folder Structure

```
LP_YourLanguages_Vue3
├── public           # Public assets
├── src
│   ├── assets       # Static images and CSS
│   ├── components   # Reusable components (Navbar, Footer)
│   ├── views        # Pages (Home, Login, Register)
│   ├── router       # Vue Router configuration
│   └── App.vue      # Root component
├── package.json     # Project dependencies
└── README.md        # Documentation
```

---

## API Endpoints

The app uses the [Reqres API](https://reqres.in/) for authentication:

- **Register**: `POST https://reqres.in/api/register`
- **Login**: `POST https://reqres.in/api/login`

## To test register and login, only use this mail and password

{
"email": "eve.holt@reqres.in",
"password": "pistol"
}

## Features in Detail

### Form Validation

- Built with **VeeValidate** and **Yup** for advanced client-side validation.
- Errors are displayed dynamically based on user interaction.

### Animations and Transitions

- Smooth page transitions using Vue's `<transition>` component.
- Button hover effects for better interactivity.

### Navigation Guards

- Protects restricted pages from unauthorized access by checking authentication status.

---

## Future Improvements

- Add real-time chat for users.
- Integrate a backend for user data persistence.
- Add multilingual support.

---

## Contributing

Contributions are welcome! Feel free to fork the repository and submit a pull request.

---

## License

This project is licensed under the MIT License. See the LICENSE file for more details.
