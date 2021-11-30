<template>
         <h4>Edit Project</h4>
         <form @submit.prevent="">
            <label> Project Title </label>
            <input type="text" v-model="title">

            <label> Project Details </label>
            <textarea v-model="details"></textarea>

            <div class="btn-control">
                <button @click="updateProject">Update project</button>
            </div>
        </form>
</template>

<script>
export default {
    props:['id'],
    data(){
        return{
            title : '',
            details : ''
        }
    },
    mounted(){
        fetch("http://localhost:3000/projects/"+this.id)
        .then((res)=>{
            return res.json()
        })
        .then((datas)=>{
            this.title=datas.title;
            this.details=datas.details;
        })
        .catch((err)=>{
            console.log(err)
        })
    },
    methods:{
        updateProject(){
            fetch("http://localhost:3000/projects/"+this.id,{
                method:"PATCH",
                headers:{
                    "Content-Type" : "application/json"
                },
                body:JSON.stringify(
                    {
                        title : this.title,
                        details : this.details
                    }
                )
            })
            .then(()=>{
                this.$router.push("/")
            })
            .catch((err)=>{
            console.log(err)
            })
        }
    }
}
</script>

<style scoped>
    h4{
        color: indigo;
        text-align: center;
        margin-bottom: 5px;
    }
</style>