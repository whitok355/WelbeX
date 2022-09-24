<template>
    <div class="b-row">
        <div class="b-column">{{element.date}}</div>
        <div class="b-column">{{element.name}}</div>
        <div class="b-column">{{element.quantity}}</div>
        <div class="b-column">{{element.distance}}</div>
    </div>
</template>
<script>
export default {
    name: 'row',
    props:{
        element:{
            type: Object
        }
    }
}
</script>
<style scoped>
.b-row{
    display: flex;
    justify-content: space-between;
    margin-top: 20px;
}
</style>
