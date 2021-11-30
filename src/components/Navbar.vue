<template>
    <nav class="nav-bar">
       <router-link to="/">Project</router-link>
       <router-link to='/addprojects'>Add projects</router-link>
    </nav>
</template>

<script>
export default {

}
</script>

<style>
    .nav-bar{
        text-align: center;
        margin: 40px auto;
    }

    .nav-bar a{
        display: inline-block;
        text-decoration: none;
        margin: 0 20px;
        color: indigo;
        font-size: 18px;
    }

    a.router-link-active{
        border-bottom: 3px solid indigo;
        padding-bottom: 6px;
        transition: 0.5s;
    }
</style>