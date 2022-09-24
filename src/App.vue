<template>
  <div class="b-wrapper">
    <h1>Таблица</h1>
      <div class="b-container">
        <div class="b-filter">
          <fieldFilter class="b-filter-el" :params="paramsColumn" @setSelected='setSelected' id="column"/>
          <fieldFilter class="b-filter-el" :params="paramsCondition" @setSelected='setSelected' id="condition"/>
          <input v-model="filter.field" class="b-filter-el" plcaeholder="Введите значение">
          <btn class="b-filter-el" :text="'Фильтр'" @click='filtered'/>
          <btn class="b-filter-el" :text="'Сбросить'" @click='cleared'/>
        </div>
        <div class="b-table">
          <div class="b-top-row">
            <div class="b-column">Дата</div>
            <div class="b-column">Название</div>
            <div class="b-column">Количество</div>
            <div class="b-column">Расстояние</div>
          </div>
            <row v-for="(el,id) in paginated" :element="el" :key="id"/>
        </div>
        <div class="b-pagination-container">
          <pagination :pageNumber='pageNumber' @prevPage="prevPage" @nextPage="nextPage"/>
        </div>
      </div>
  </div>
</template>

<script>
import fieldFilter from './components/fieldFilter'
import btn from './components/btn'
import row from './components/row'
import pagination from './components/pagination'

export default {
  name: 'App',
  components: { fieldFilter, btn, row, pagination },
  data(){
    return{
      filter: {
        column: null,
        condition: null,
        field: null,
      },
      dataBase: [
        {date: '23.11.2021', name: 'Иван', quantity: 2, distance: 1000},
        {date: '12.15.2011', name: 'Алена', quantity: 3, distance: 2000},
        {date: '11.17.2012', name: 'Светлана', quantity: 4, distance: 3000},
        {date: '10.18.2014', name: 'Игорь', quantity: 5, distance: 4000},
        {date: '04.11.2016', name: 'Алексей', quantity: 1, distance: 5000},
        {date: '02.12.2017', name: 'Андрей', quantity: 8, distance: 6000},
        {date: '10.23.2022', name: 'Сергей', quantity: 9, distance: 6600},
        {date: '19.26.2018', name: 'Иосиф', quantity: 6, distance: 1700},
        {date: '09.28.2019', name: 'Багдан', quantity: 8, distance: 1080},
        {date: '23.11.2021', name: 'Иван', quantity: 2, distance: 14000},
        {date: '12.15.2011', name: 'Алена', quantity: 3, distance: 23500},
        {date: '11.17.2012', name: 'Светлана', quantity: 4, distance: 56700},
        {date: '10.18.2014', name: 'Игорь', quantity: 5, distance: 78900},
        {date: '04.11.2016', name: 'Алексей', quantity: 1, distance: 800},
        {date: '02.12.2017', name: 'Андрей', quantity: 8, distance: 6123000},
        {date: '10.23.2022', name: 'Сергей', quantity: 9, distance: 623600},
        {date: '19.26.2018', name: 'Иосиф', quantity: 6, distance: 1704530},
        {date: '09.28.2019', name: 'Багдан', quantity: 8, distance: 105480},
        {date: '23.11.2021', name: 'Иван', quantity: 2, distance: 106500},
        {date: '12.15.2011', name: 'Алена', quantity: 3, distance: 2056400},
        {date: '11.17.2012', name: 'Светлана', quantity: 4, distance: 3023400},
        {date: '10.18.2014', name: 'Игорь', quantity: 5, distance: 402300},
        {date: '04.11.2016', name: 'Алексей', quantity: 1, distance: 500450},
        {date: '02.12.2017', name: 'Андрей', quantity: 8, distance: 604500},
        {date: '10.23.2022', name: 'Сергей', quantity: 9, distance: 665600},
        {date: '19.26.2018', name: 'Иосиф', quantity: 6, distance: 176700},
        {date: '09.28.2019', name: 'Багдан', quantity: 8, distance: 10880},
        {date: '23.11.2021', name: 'Иван', quantity: 2, distance: 10090},
        {date: '12.15.2011', name: 'Алена', quantity: 3, distance: 20030},
        {date: '11.17.2012', name: 'Светлана', quantity: 4, distance: 30020},
        {date: '10.18.2014', name: 'Игорь', quantity: 5, distance: 4012300},
        {date: '04.11.2016', name: 'Алексей', quantity: 1, distance: 532400},
        {date: '02.12.2017', name: 'Андрей', quantity: 8, distance: 60040},
        {date: '10.23.2022', name: 'Сергей', quantity: 9, distance: 6654300},
        {date: '19.26.2018', name: 'Иосиф', quantity: 6, distance: 1703230},
        {date: '09.28.2019', name: 'Багдан', quantity: 8, distance: 10123840},
        {date: '23.11.2021', name: 'Иван', quantity: 2, distance: 1001230},
        {date: '12.15.2011', name: 'Алена', quantity: 3, distance: 200340},
        {date: '11.17.2012', name: 'Светлана', quantity: 4, distance: 300540},
        {date: '10.18.2014', name: 'Игорь', quantity: 5, distance: 4008900},
        {date: '04.11.2016', name: 'Алексей', quantity: 1, distance: 50600},
        {date: '02.12.2017', name: 'Андрей', quantity: 8, distance: 60030},
        {date: '10.23.2022', name: 'Сергей', quantity: 9, distance: 6623400},
        {date: '19.26.2018', name: 'Иосиф', quantity: 6, distance: 1704640},
        {date: '09.28.2019', name: 'Багдан', quantity: 8, distance: 1023480},
        {date: '23.11.2021', name: 'Иван', quantity: 2, distance: 1002340},
        {date: '12.15.2011', name: 'Алена', quantity: 3, distance: 2000123},
        {date: '11.17.2012', name: 'Светлана', quantity: 4, distance: 3043500},
        {date: '10.18.2014', name: 'Игорь', quantity: 5, distance: 4000567},
        {date: '04.11.2016', name: 'Алексей', quantity: 1, distance: 596000},
        {date: '02.12.2017', name: 'Андрей', quantity: 8, distance: 602300},
        {date: '10.23.2022', name: 'Сергей', quantity: 9, distance: 6602340},
        {date: '19.26.2018', name: 'Иосиф', quantity: 6, distance: 17067540},
        {date: '09.28.2019', name: 'Багдан', quantity: 8, distance: 1087680},
      ],
      filterData: [],
      pageNumber: 1,
      size: 10,
      paramsColumn: [['Название', 'name'], ['Количество', 'quantity'], ['Расстояние', 'distance']],
      paramsCondition: [['Равно', 'equally'], ['Содержит', 'contains'], ['Больше', 'more'], ['Меньше', 'less']],
      reloade: true,
    }
  },
  mounted(){
    this.filterData = this.dataBase;
  },
  methods:{
    nextPage(){
      if(this.pageNumber < this.pageCount){
         this.pageNumber++;
        }
    },
    prevPage(){
      if(this.pageNumber >= 2){
        this.pageNumber--;
      }
    },
    setSelected(selected, param){
      this.filter[param] = selected;
    },
    filtered(){
      if(this.filter.condition === 'equally'){
        const regExp = new RegExp(`^${this.filter.field}`, 'i');
        this.filterData = this.dataBase.filter(el => regExp.test(el[this.filter.column]))
      }
      if(this.filter.condition === 'contains'){
        const regExp = new RegExp(`${this.filter.field}+`, 'i')
        this.filterData = this.dataBase.filter(el => regExp.test(el[this.filter.column]))
      }
      if(this.filter.condition === 'more'){
        this.filterData = this.dataBase.filter(el => el[this.filter.column] > this.filter.field);
      }
      if(this.filter.condition === 'less'){
        this.filterData = this.dataBase.filter(el => el[this.filter.column] < this.filter.field);
      }
    },
    cleared(){
      this.filterData = this.dataBase;
      for(let i in this.filter){
        this.filter[i] = null
      }
    }
  },

  computed:{
    pageCount(){
      return Math.ceil(this.dataBase.length / this.size)
    },
    paginated(){
      const start = this.pageNumber === 1 ? 1: this.pageNumber * this.size;
      const end = start + this.size;
      return this.filterData.slice(start, end)
    },
  }
}
</script>

<style>
.b-wrapper{
  height: 100vh;
  background: grey;
  padding: 30px;
}
.b-container{
  padding: 20px 50px;
  border: 1px solid black;
  margin: 0 auto;
}
h1{
  text-align: center;
}
.b-filter{
  text-align: center;
}
.b-filter-el{
  margin-right: 30px;
}
.b-top-row{
  margin-top: 40px;
  display: flex;
  justify-content: space-between;
  font-size: 1.5em;
  text-transform: uppercase;
}
.b-column{
  width: 150px;
  text-align: center;
}
.b-pagination-container{
  display: flex;
  justify-content: center;
}
</style>
