<template>
  <div id="app">
    
    <Note :content="msg" @update="msg=$event"/>
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
      msg:"Take a Note",
      title: "Title"
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

*{
  padding : 0;
  margin : 0;
  box-sizing: border-box;
}

html {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;

}

body {
  background: #eee;
  padding: 0 16px;
}
</style>
