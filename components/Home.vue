<template>
    <button @click="googleLogin">googleでログイン</button>
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
