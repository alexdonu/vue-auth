<script lang="ts" setup>
import { ref } from 'vue'
import { getAuth, createUserWithEmailAndPassword } from 'firebase/auth'
import { useRouter } from 'vue-router'

const email = ref('')
const password = ref('')

const router = useRouter()

async function register() {
  createUserWithEmailAndPassword(getAuth(), email.value, password.value)
    .then((userCredential) => {
      const user = userCredential.user
      console.log('User registered:', user)
      router.push({ path: '/secret' })
    })
    .catch((error) => {
      const errorCode = error.code
      const errorMessage = error.message
      console.error('Error registering user:', errorCode, errorMessage)
    })
}
</script>

<template>
  <div>
    <label for="email">
      email:
      <input v-model="email" id="email" type="email" />
    </label>

    <br />

    <label for="password">
      Password:
      <input v-model="password" id="password" type="password" />
    </label>

    <br />

    <button @click="register">register</button>
  </div>
</template>
