<template>
    <div class="filterNav">
        <button @click="filterBy('all')" :class="{activeNav:this.filter==='all'}">All</button>
        <button @click="filterBy('complete')" :class="{activeNav:this.filter==='complete'}">Complete</button>
        <button @click="filterBy('on going')" :class="{activeNav:this.filter==='on going'}">On going</button>
    </div>
</template>

<script>
export default {
    props:['filter'],
    methods:{
        filterBy(value){
            console.log(value);
            this.$emit('filter',value)
        }
    }
}
</script>

<style scoped>
    .filterNav button{
        border: none;
        outline: none;
        margin-left: 5px;
        padding: 5px;
        background: #fff;
        color: #aaa;
        cursor: pointer;
    }

    .activeNav{
       color: indigo !important;
       font-size: 1em;
    }
</style>