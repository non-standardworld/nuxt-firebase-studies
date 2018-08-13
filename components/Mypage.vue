<template>
<div id="mypage">
  <span>こんにちは, {{ user.displayName }}さん</span>
  <p><button @click="logout">ログアウト</button></p>
  <h2>あなたのノート</h2>
  <p>{{ note_content }}</p>
  <div id='notesIndex' v-for="note in notes" :key="note.content">

    <p class="noteContent">{{ note.content }}</p>
  </div>
  <h2>入力されたノート</h2>
  <p><textarea v-model="note_content"></textarea></p>
    <p><button class="saveNoteBtn" @click="saveContent(note_content)">ノートを保存する</button></p>
</div>
</template>

<script>
import firebase from '@/plugins/firebase'
export default {
  name: 'mypage',
  props: ['user'],
  data (context) {
    // コンポーネントをロードする前に毎回呼び出されます
    return { note_content: 'hello', notes:[]}
  },
  created: function() {
    firebase
      .database()
      .ref('notes/' + this.user.uid)
      .once('value')
      .then(result => {
        if (result.val()) {
          this.notes = result.val();
        }
      })
  },
  methods: {
    logout: function() {
      firebase.auth().signOut();
    },
    saveContent: function(value) {
      // Get a key for a new Post.
      var newNoteKey = firebase.database().ref().child('notes').push().key;
      firebase
        .database()
        .ref('notes/' + this.user.uid　+ '/' + newNoteKey)
        .set({content:value});
    }
  }
}
</script>
