<template>
    <select v-model="selected" @change="setSelected">
        <option selected disabled>Выберите поле</option>
        <template v-for="(el, id) in params" :key="id">
         <option :value="el[1]" :id='el[1]'>{{el[0]}}</option>        
        </template>
    </select>
</template>
<script>
export default {
    name: 'fieldFilter',
    props:{
        params: {
            type: Array,
        }
    },
    data(){
        return{
            selected: null,
        }
    },
    methods:{
        setSelected(e){
            this.$emit('setSelected', this.selected, e.target.id)
        }
    },
}
</script>
<style></style>