<template>
   <div class="home">
       <FilteredNav @filter="filter=$event" :filter="filter"></FilteredNav>
       <div v-for="project in filterProjects" :key="project.id">
           <SingleProject :project="project" @delete="deleteProject" @complete="completeProject"></SingleProject>
       </div>
   </div>
</template>

<script>
import FilteredNav from '../components/FilteredNav'
import SingleProject from '../components/SingleProject'
export default {
  components: {
    FilteredNav, SingleProject },
    data(){
        return{
            projects : [], //local variable
            filter : "all"
        }
    },
    methods:{
        deleteProject(id){
            this.projects=this.projects.filter(el=>{
                return el.id!=id
            })
        },
        completeProject(id){
            let find = this.projects.find(el=>{
                return el.id === id;
            })
            find.isDone =!find.isDone
        }
    },
   mounted(){
        fetch('http://localhost:3000/projects')
        .then((response)=>{
            return response.json()
        })
        .then((datas)=>{
            this.projects=datas
        })
        .catch((err)=>{
            console.log(err.message())
        })
    },
    computed:{
        filterProjects(){
            if(this.filter==='complete'){
                return this.projects.filter(el=>{
                    return el.isDone;
                })
            }
             if(this.filter==='on going'){
                return this.projects.filter(el=>{
                    return !el.isDone;
                })
            }
            return this.projects
        }
    }
}
</script>

<style>

</style>