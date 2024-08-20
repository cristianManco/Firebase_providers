<template>
  <div class="auth-container">
    <h2>Sign In</h2>
    <AuthButton
      v-for="provider in providers"
      :key="provider.name"
      :signIn="provider.signInMethod"
      :providerName="provider.name"
    />
    <br />
    <br />
    <EmailSignInForm
      :email="email"
      :password="password"
      @update:email="email = $event"
      @update:password="password = $event"
      @submit="signInWithEmail"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import EmailSignInForm from './EmailSignInForm.vue'
import {
  signInWithPopup,
  GoogleAuthProvider,
  FacebookAuthProvider,
  GithubAuthProvider,
  OAuthProvider,
  signInWithEmailAndPassword
} from 'firebase/auth'
import AuthButton from './authButton.vue'
import { auth } from '@/firebase.config'

export default defineComponent({
  name: 'AuthContainer',
  components: {
    AuthButton,
    EmailSignInForm
  },
  setup() {
    const email = ref('')
    const password = ref('')

    const signInWithGoogle = () => {
      const provider = new GoogleAuthProvider()
      signInWithPopup(auth, provider)
        .then((result) => {
          console.log('User signed in with Google', result.user)
          saveToken(result.user)
        })
        .catch((error) => {
          console.error('Google sign-in error', error)
        })
    }

    const signInWithFacebook = () => {
      const provider = new FacebookAuthProvider()
      signInWithPopup(auth, provider)
        .then((result) => {
          console.log('User signed in with Facebook', result.user)
          saveToken(result.user)
        })
        .catch((error) => {
          console.error('Facebook sign-in error', error)
        })
    }

    const signInWithGithub = () => {
      const provider = new GithubAuthProvider()
      signInWithPopup(auth, provider)
        .then((result) => {
          console.log('User signed in with GitHub', result.user)
          saveToken(result.user)
        })
        .catch((error) => {
          console.error('GitHub sign-in error', error)
        })
    }

    const signInWithMicrosoft = () => {
      const provider = new OAuthProvider('microsoft.com')
      signInWithPopup(auth, provider)
        .then((result) => {
          console.log('User signed in with Microsoft', result.user)
          saveToken(result.user)
        })
        .catch((error) => {
          console.error('Microsoft sign-in error', error)
        })
    }

    const signInWithEmail = () => {
      signInWithEmailAndPassword(auth, email.value, password.value)
        .then((userCredential) => {
          console.log('User signed in with Email', userCredential.user)
          saveToken(userCredential.user)
        })
        .catch((error) => {
          console.error('Email sign-in error', error)
        })
    }

    const saveToken = (user: any) => {
      user.getIdToken().then((token: string) => {
        localStorage.setItem('firebase_token', token)
      })
    }

    const providers = ref([
      { name: 'Google', signInMethod: signInWithGoogle },
      { name: 'Facebook', signInMethod: signInWithFacebook },
      { name: 'GitHub', signInMethod: signInWithGithub },
      { name: 'Microsoft', signInMethod: signInWithMicrosoft }
    ])

    return {
      email,
      password,
      providers,
      signInWithEmail
    }
  }
})
</script>

<style lang="scss" scoped>
.auth-container {
  width: 100%;
  max-width: 400px;
  margin: 2rem auto;
  padding: 2rem;
  background-color: #c9b5b5;
  border-radius: 15px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  text-align: center;
  filter: brightness(0.8);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: center;
  align-items: center;

  h2 {
    font-size: 2rem;
    color: #343a40;
    margin-bottom: 2rem;
    font-family: 'Poppins', sans-serif;
  }
}
</style>
