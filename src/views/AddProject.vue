<template>
    <h4>Add Project</h4>
   <form @submit.prevent="addProject">
       <label> Project Title </label>
       <input type="text" v-model="title">

       <label> Project Details </label>
       <textarea v-model="details"></textarea>

       <div class="btn-control">
           <button>Add project</button>
       </div>
   </form>

</template>

<script>
export default {
    data(){
        return{
            title : '',
            details : ''
        }
    },
    methods:{
        addProject(){
            console.log(this.title,this.detail);
            fetch("http://localhost:3000/projects",{
                method:"POST",
                headers:{
                    "Content-Type":"application/json"
                },
                body:JSON.stringify({
                    title : this.title,
                    details : this.details,
                    isDone: false
                })
            })
            .then(()=>{
                this.$router.push('/') //redirect
            })
            .catch((err)=>{
                console.log(err)
            })
        }
    }
}
</script>

<style>
    form{
        max-width: 500px;
        padding: 20px;
        text-align: left;
    }

    label{
        display: inline-block;
        color: rgb(7, 7, 97);
        font-size: 1.2em;
        margin-bottom: 10px;
    }

    input{
        display: block;
        width: 90%;
        border: none;
        outline: none;
        border-bottom: 2px solid indigo;
        opacity: 0.5;
        background: #fff;
        padding: 10px;
        margin: 10px 0;
        font-size: 1.1em;
    }

    textarea{
        display: block;
        width: 90%;
        border: none;
        outline: none;
        border-bottom: 2px solid indigo;
        background: #fff;
        opacity: 0.5;
        padding: 10px;
        margin: 10px 0;
        font-size: 1em;
    }

    .btn-control{
        text-align: center;
    }

    .btn-control button{
        padding: 10px;
        margin-top: 10px;
        outline: none;
        border: none;
        cursor: pointer;
        background: rgba(29, 3, 63, 0.993);
        color: #fff;
        border-radius: 10px;
    }

     h4{
        color: indigo;
        text-align: center;
        margin-bottom: 5px;
    }
</style>