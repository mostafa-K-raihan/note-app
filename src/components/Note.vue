<template>
<div>
<div class="note-parent">
    <input class="title" v-model="title" @click="firstTimeClick(title, 'Title')"/>
    <div class="note-container" ref="editableDiv" contenteditable="true" @input="update" @click="firstTimeClick(content, content)"></div>
    <div class="btn-save" type="button" v-if="btnShow" @click="saveNote">Save</div>
    
</div>
<div class="grid" ref="gallery">
    <div class="saved-note" v-for="(note,index) in notes" :key="index">
        <div class="delete" @click="deleteNote(index)">
            <div class="dots-caps"></div>
            <div class="dots" ></div>
        </div>
        <h1>{{note.title}}</h1>
        <h5>{{note.time}}</h5>
        <div>{{note.content}}</div>
    </div>
</div>
</div>
</template>
<script>
import Masonary from 'masonry-layout';
export default {
    name: "Note",
    data(){
        return {
            masonary : {},
            btnShow : false,
            title : 'Title',
            notes : [
                
            ],
        }
    },
    props : {
        content : String,
    },

    mounted() {
        this.$refs.editableDiv.innerText = this.content;

        this.masonary = new Masonary(this.$refs.gallery, {
            itemSelector : '.saved-note',
            columnWidth : 240,
            gutter : 16,
            fitWidth: true,
        });
        // console.log(masonary);
        this.notes = JSON.parse(localStorage.getItem("notes")) || [];
        this.nextTick();
    },

    methods:{
        deleteNote(idx){
            this.notes.splice(idx, 1);
            localStorage.setItem("notes", JSON.stringify(this.notes));

        },
        firstTimeClick(src, dest) {
            if(src === dest) {
                document.execCommand('selectAll', false, null);
            }
        },
        updateTitle(event) {
            // console.log(event.target.innerText);
            this.title = event.target.innerText;
        },
        nextTick() {
            this.$nextTick(()=>{
                this.masonary.reloadItems();
                this.masonary.layout();
            });
        },
        update(event){
            if(!this.btnShow) {
                this.btnShow = !this.btnShow;
            }
            this.$emit("update", event.target.innerText);
        },
        saveNote() {
            this.notes.push({title: this.title, time: new Date().toLocaleString(), content : this.content});
            localStorage.setItem("notes", JSON.stringify(this.notes));
            this.nextTick();
        }
    },


}
</script>
<style scoped>
.delete {
    float:right;
}
.dots {
    width:15px;
    height:20px;
    border-bottom-left-radius: 3px;
    border-bottom-right-radius: 3px;
    background:#000;
    border: 1px solid black;
    margin-left: 2px;

    
}

.dots:hover {
    transform : scale(1.1);
    transition: .3s transform ease-in;
    background: #ccc;
}
.dots-caps {
    width: 20px;
    height: 2px;
    background: #000;
    margin-bottom: 2px;
}

.dots-caps::before{
    width:10px;
    background: #000;
    height: 3px;
    content: "";
    display: block;
    position: absolute;
    margin-left: 5px;
    margin-top: -3px;
}

.title{
    /* user-select: all;
    -moz-user-select: all; */
    min-height: 46px;
    border-radius: 8px;
    box-shadow: 
    0 1px 2px 0 rgba(60,64,67, .3),
                0 2px 6px 2px rgba(60,64,67,.15)
    ;
    min-width: 360px;
    margin: 0;
    background: #ffe;

    color: #80868b;
    line-height:1.5rem;
    font-size: 1.5em;
    padding : 12px 16px;
    letter-spacing: .00625em;
    margin-bottom: 5px;

}
.note-container {
    position : relative;
    width : 510px;
    /* margin : 15px auto; */
    background: #fff;
    /* padding: 15px; */

    border: 1px solid gray;
    min-height: 46px;
    border-radius: 8px;
    box-shadow: 
    0 1px 2px 0 rgba(60,64,67, .3),
                0 2px 6px 2px rgba(60,64,67,.15)
    ;
    min-width: 360px;
    overflow: hidden;
    margin: 0;
    

    color: #80868b;
    line-height:1.5rem;
    font-size: 1.2em;
    padding : 12px 16px;
    letter-spacing: .00625em;
}
.note-parent {
    display: flex;
    flex-direction: column;
    /* background: #cde; */
    
}

.grid {
    /* -webkit-column-count: 3;
    -moz-column-count: 3;
    column-count: 3;

    -webkit-column-gap: 20px;
    -moz-column-count: 20px;
    column-gap: 20px; */
    /* max-height : 500px; */
    /* background: #234; */
    margin-top : 20px;
    width: 100%;
    /* border : 5px solid red; */
    
}
.btn-save {
    margin-top: 20px;
    justify-self: flex-end;
    align-self: flex-end;
    padding: 8px 20px;
    border-radius: 15px;
    cursor: pointer;
    color : aliceblue;
    background-color: #80868b;
    font-weight : bold;
    border: 1px solid #80868b;

    
}

.saved-note {
    background: #fff;
    border-radius: 5px;
    box-shadow: 0 2px 5px #ccc;
    padding : 10px;
    width: 240px;
    margin: 8px 0;
    
}

.btn-save:hover {
    background-color:darkgray;
    color: antiquewhite;
}
</style>


