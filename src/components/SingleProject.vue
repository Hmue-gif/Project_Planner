<template>
   <div class="project" :class="{doneProject:project.isDone}">
        <div>
            <h3 @click="showProject=!showProject"> {{project.title}} </h3>
            <p v-if="showProject"> {{project.details}} </p>
           
        </div>

        <div>
            <span class="material-icons del" @click="deleteProject">
            delete
            </span>
            <router-link :to="{name:'EditProject',params:{id:this.project.id}}">
                <span class="material-icons edit">
                    edit
                </span>
            </router-link>
            <span class="material-icons done" @click="completeProject">
            done
            </span>
        </div>
   </div>
</template>

<script>
export default{
    props:['project'],
    data(){
        return{
            showProject : false,
            api : "http://localhost:3000/projects/"
        }
    },
    methods:{
        deleteProject(){
            let deleteData = this.api+this.project.id;
            fetch(deleteData,{method:"DELETE"})
            .then(()=>{
                this.$emit("delete",this.project.id)
            })
        },
        completeProject(){
            let completeProject = this.api+this.project.id;
            fetch(completeProject,{
                method:"PATCH",
                headers:{
                    "Content-Type" : "application/json"
                },
                body:JSON.stringify(
                    {
                        isDone:!this.project.isDone
                    }
                )
            })
            .then(()=>{
                this.$emit("complete",this.project.id)
            })
            .catch((err)=>{
                console.log(err)
            })
        }
    }
}
</script>

<style>
    .project{
        padding: 20px;
        background: #f2f2f2;
        margin: 10px;
        display: flex;  
        justify-content: space-between;
        align-items: center;
        border-radius: 6px;
        border-left: 5px solid crimson;
    }

    .doneProject{
        border-left-color: greenyellow;
    }

    h3{
        color: indigo;
        cursor: pointer;
    }

    p{
        color: indigo;
        opacity: 0.8;
    }

    span{
        margin-left: 10px;
        cursor: pointer;
    }

    .del:hover{
        color: crimson;
        transform: scale(1.1);
        transition: 0.8s;
    }

    .edit:hover{
        color: yellow;
        transform: scale(1.1);
        transition: 0.8s;
    }

    .done:hover{
        color: greenyellow;
        transform: scale(1.1);
        transition: 0.8s;
    }

</style>
