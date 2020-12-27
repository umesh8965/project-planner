<template>
  <div class="project" :class="{complete : project.complete}">
      <div class="action">
          <h3 @click="showDetail = !showDetail">{{project.title}}</h3>
          <div class="icons">
              <span class="material-icons tick" @click="toggleComplete">done</span>              
              <span class="material-icons" @click="deleteProject">delete</span>
              <router-link :to="{ name:'EditProject', params:{id : project.id}}">
                <span class="material-icons">edit</span>
              </router-link>
          </div>
      </div>
      <div v-if="showDetail" class="details">
          <p>{{project.detail}}</p>
      </div>
  </div>
</template>

<script>
export default {
    props:[
        "project"
    ],
    data(){
       return{
          showDetail: false,
          uri:"http://localhost:3000/projects/" + this.project.id
       } 
    },
    methods:{
        deleteProject(){
            fetch(this.uri, {method: "DELETE"})
            .then(() => this.$emit("delete", this.project.id))
            .catch(err => console.log(err))
        },
        toggleComplete(){
            fetch(this.uri, {
                method: 'PATCH',
                headers: { 'Content-type' : 'application/json'},
                body: JSON.stringify({ complete: !this.project.complete})
            })
            .then(() =>{
                this.$emit("complete",this.project.id)   
            })
            .catch((err) => console.log(err))
        }
    }
}
</script>

<style>
.project{
    margin: 20px auto;
    background-color: #fff;
    padding:10px 20px;
    border-radius: 5px;
    border-left:4px solid lightcoral;
    box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
}
.project h3{
    font-size: 14px;
}
.action{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.material-icons{
    font-size: 24px;
    margin-left: 10px;
    color: #bbb;
    cursor: pointer;
}
.material-icons:hover{
    color: #555;
}
.project.complete{
    border-left:4px solid mediumseagreen
}
.project.complete .tick{
    color:mediumseagreen
}
</style>