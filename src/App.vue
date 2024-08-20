<template>
  <div id="app">
    <h1>Providers Firebase-Auth</h1>
    <br />
    <AuthContainer />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import AuthContainer from './components/AuthContainer.vue'

export default defineComponent({
  name: 'App',
  components: {
    AuthContainer
  }
})
</script>

<style>
@import './assets/styles/global.scss';
h1 {
  text-align: center;
  color: blueviolet;
}
</style>
