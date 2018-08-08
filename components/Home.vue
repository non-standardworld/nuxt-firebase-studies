<template>
  <div class="home">
    <button @click="googleLogin">googleでログイン</button>
  </div>
</template>

<script>
import firebase from '@/plugins/firebase'
export default {
  name: 'home',
  methods: {
    googleLogin: function() {
      firebase.auth().signInWithRedirect(new firebase.auth.GoogleAuthProvider());
    }
  }
}
</script>
