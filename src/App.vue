<template>
  <div id="app">
    
    <Note/>
  </div>
</template>

<script>
import Note from './components/Note.vue'

export default {
  name: 'app',
  components: {
    Note
  },
  data() {
    return{
      noteCounter : 0,
    }
  },
  methods:{
    addNote() {
      this.noteCounter ++;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
  display:flex;
  align-items: center;
  justify-content: center;

}
</style>
