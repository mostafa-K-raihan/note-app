<template>
    <div class="note-container">
        <div class="note-clicker" contenteditable="true" role="textbox">
            Take a note...
        </div>
        
    </div>
</template>
<script>
export default {
    name: "Note",
    data(){
        return {
            msg : '',
        }
    }
}
</script>
<style scoped>

.note-container {
    width : 540px;
    border: 1px solid gray;
    height: 46px;
    border-radius: 8px;
    box-shadow: 
    0 1px 2px 0 rgba(60,64,67, .3),
                0 2px 6px 2px rgba(60,64,67,.15)
    ;
    min-width: 360px;
    overflow: hidden;
    margin: 0;
}

.note-clicker {
    padding-top:12px;
    color: #80868b;
    line-height:1.5rem;
    font-size: 1.2em;
    padding : 12px 16px;
    letter-spacing: .00625em; 
}

.note-clicker:hover {
    cursor: auto;
}
</style>


