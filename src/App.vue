<template>
   <div class="background">
    <img src="https://i.ibb.co/F88mT9d/image.png" />
  </div>
  <div class="content">
    <h1>Sign Up</h1>
    <form @submit.prevent="handleSubmit">
      <div class="tampilan">
      <div>
        <label for="username">Username:</label>
        <input type="text" id="username" v-model="username" @input="updateUsername">
        <p :class="{ 'error': usernameError }">Username dimasukan: {{ username }}</p>
        <span :class="usernameValidationIconClass"></span>
      </div>
      <div>
        <label for="password">Password:</label>
        <input type="password" id="password" v-model="password" @input="updatePassword">
        <p :class="{ 'error': !isPasswordValid }">{{ passwordErrorMsg }}</p>
        <span :class="passwordValidationIconClass"></span>
      </div>
    </div>
      <button type="submit">Sign Up</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const username = ref('');
const password = ref('');
const usernameError = ref(false);
const isPasswordValid = ref(true);
const passwordErrorMsg = ref('');

const handleSubmit = () => {
  if (!username.value) {
    usernameError.value = true;
  } else {
    alert('Form submitted!');
    username.value = '';
    password.value = '';
    usernameError.value = false;
  }
};

const updateUsername = (event) => {
  console.log('Username updated:', event.target.value);
};

const updatePassword = (event) => {
  const passwordValue = event.target.value;
  isPasswordValid.value = validatePassword(passwordValue);
  passwordErrorMsg.value = isPasswordValid.value ? '' : 'Password harus memiliki simbol, huruf kapital, dan angka';
};

const validatePassword = (password) => {
  const symbolRegex = /[-!$%^&*()_+|~=`{}\[\]:";'<>?,.\/]/;
  const capitalLetterRegex = /[A-Z]/;
  const numberRegex = /[0-9]/;

  return symbolRegex.test(password) && capitalLetterRegex.test(password) && numberRegex.test(password);
};

const usernameValidationIconClass = () => {
  return username.value && !usernameError.value ? 'valid-check' : 'invalid-check';
};

const passwordValidationIconClass = () => {
  return isPasswordValid.value ? 'valid-check' : 'invalid-check';
};
</script>

<style>
.error {
  color: red;
  text-align: left;
  margin-right: 10px;
}

.valid-check::before {
  content: '✓';
  color: green;
  margin-right: 5px;
}

.invalid-check::before {
  content: '✕';
  color: red;
  margin-right: 5px;
}
.tampilan, input{
  display: grid;
  margin-bottom: 10px;
  margin-top: 10px;
}
h1{
  margin-left: 70px;
  padding-top: 10%;
  position: fixed;
  font-weight: bold;
  text-shadow: 0 0 10px black;

}
.tampilan{
  margin-left: 70px;
  margin-top: 100px;
}

button{
  margin-left: 120px;
  font-size: 20px;
  border-radius: 10px;
  padding: 5px 5px;
}

.content{
  border: 1px solid black;
  width: 300px;
  height: 350px;
  max-width: 100%;
  margin-left: -50%;
  background-color: transparent;
  backdrop-filter: blur(5px);
}

.background img{
  position: fixed;
  top: 0;
  left: 0;
  min-height: 90%;
  min-width: 1500px;
  width: 100%;
  height: 100%;
  overflow: hidden;
  z-index: -2;
  object-fit: cover;
  -webkit-background-size:cover; -moz-background-size:cover; -o-background-size:cover; background-size: cover;
  filter: brightness(0.8);
}
</style>
