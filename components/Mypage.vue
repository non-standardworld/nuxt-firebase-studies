<template>
<div id="mypage">
  <span>こんにちは, {{ user.displayName }}さん</span>
  <button @click="logout">ログアウト</button>
</div>
</template>

<script>
import firebase from '@/plugins/firebase'
export default {
  name: 'mypage',
  props: ['user'],
  methods: {
    logout: function() {
      firebase.auth().signOut();
    }
  }
}
</script>
