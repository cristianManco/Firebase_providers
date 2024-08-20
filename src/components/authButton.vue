<template>
  <button class="auth-button" @click="signIn">{{ providerName }}</button>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'AuthButton',
  props: {
    signIn: {
      type: Function,
      required: true
    },
    providerName: {
      type: String,
      required: true
    }
  }
})
</script>

<style lang="scss">
.auth-button {
  background-color: #007bff;
  color: #fff;
  padding: 0.75rem 1.5rem;
  border: none;
  border-radius: 25px;
  font-family: 'Poppins', sans-serif;
  font-size: 1rem;
  cursor: pointer;
  margin: 0.5rem 0;
  width: 100%;
  display: block;
  text-align: center;

  &:hover {
    background-color: #0056b3;
  }
}
</style>
