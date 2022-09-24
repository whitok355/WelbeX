<template>
    <ul class="b-pagination">
        <li class="b-pagination-btn" @click="prevPage">next</li>
        <li class="b-pagination-number">{{pageNumber}}</li>
        <li class="b-pagination-btn" @click="nextPage">prev</li>
    </ul>
</template>
<script>
export default {
    name: 'pagination',
    props:{
        pageNumber:{
            type: Number,
            default: 1,
        }
    },
    methods:{
        prevPage(){
            this.$emit('prevPage')
        },
        nextPage(){
            this.$emit('nextPage')
        }
    }
}
</script>
<style scoped>
.b-pagination{
    list-style-type: none;
    display: flex;
}
.b-pagination-number{
    border: 1px solid black;
    border-radius: 50px;
    width: 20px;
    height: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-left: 20px;
    margin-right: 20px;   
}
.b-pagination-btn:hover{
    cursor: pointer;
}
</style>