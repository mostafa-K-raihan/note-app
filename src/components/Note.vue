<template>
    <div class="note-container">
        <textarea v-model="msg" class="note-input" cols="30" rows="10"></textarea>
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
    width :;
}
</style>


