<template>
  <form @submit.prevent="handleSubmit">
    <label for="">Title:</label>
    <input type="text"  v-model="title" required>
    <label for="">Details:</label>
    <textarea  v-model="detail" required></textarea>
    <button>Update Project</button>
  </form>
</template>

<script>
export default {
    props:['id'],
    data(){
        return{
            title : this.title,
            detail :this.detail,
            uri: 'http://localhost:3000/projects/' + this.id
        }
    },
    mounted(){
        fetch(this.uri)
        .then(res => res.json())
        .then(data => {
            this.title = data.title,
            this.detail = data.detail
        })
    },
    methods: {
        handleSubmit(){
            fetch(this.uri, {
                method:'PATCH',
                headers:{ 'Content-type' : 'application/json'},
                body:JSON.stringify({ title:this.title, detail:this.detail}),
            })
            .then(() => {
                this.$router.push('/')
            })
            .catch(err => console.log(err))
        }
    }
}
</script>

<style>

</style>