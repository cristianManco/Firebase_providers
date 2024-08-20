<template>
  <form @submit.prevent="submitForm" class="email-form">
    <input type="email" v-model="localEmail" placeholder="Correo electrónico" required />
    <input type="password" v-model="localPassword" placeholder="Contraseña" required />
    <br />
    <br />
    <button type="submit" class="btnsubmit">Iniciar sesión</button>
  </form>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from 'vue'

export default defineComponent({
  name: 'EmailSignInForm',
  props: {
    email: {
      type: String,
      required: true
    },
    password: {
      type: String,
      required: true
    }
  },
  emits: ['update:email', 'update:password', 'submit'],
  setup(props, { emit }) {
    const localEmail = ref(props.email)
    const localPassword = ref(props.password)

    const submitForm = () => {
      emit('submit', { email: localEmail.value, password: localPassword.value })
    }

    watch(
      () => props.email,
      (newVal) => {
        localEmail.value = newVal
      }
    )

    watch(
      () => props.password,
      (newVal) => {
        localPassword.value = newVal
      }
    )

    return {
      localEmail,
      localPassword,
      submitForm
    }
  }
})
</script>

<style lang="scss">
/* EmailSignInForm.vue */
.email-signin-form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.form-group {
  margin-bottom: 20px;
  width: 100%;
}

input[type='email'],
input[type='password'] {
  width: 100%;
  padding: 12px;
  border-radius: 5px;
  border: 1px solid #ddd;
  box-sizing: border-box;
  font-size: 16px;
}

input[type='email']:focus,
input[type='password']:focus {
  border-color: #007bff;
  outline: none;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}

.btnsubmit {
  background-color: #28a745;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  transition: all 0.3s ease;
}

.btnsubmit:hover {
  background-color: #218838;
}

.btnsubmit:active {
  background-color: #1e7e34;
}
</style>
