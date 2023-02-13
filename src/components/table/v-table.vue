<template>
    <div class='v-table'>
        <div class="v-table_header">
            <p>Номер</p>
            <p>Имя</p>
            <p>Фамилия</p>
            <p>Курс</p>
            <p>Группа</p>
            <p>Средний балл</p>
        </div>
        <div class="table_body">
            <div class="body_row">
                <v-table-row
                    v-for="row in paginatedUsers"
                    :key="row.number"
                    :row_data="row"
                />
            </div>
        </div>
        <div class="v-table_pagination">
            <div class="page" v-for="page in pages" :key="page" @click="pageClick(page)">
                {{ page }}
            </div>
        </div>
    </div>
</template>
<script>
    import { METHODS } from 'http';
import vtablerow from './v-table-row'
    
    export default {
    name: "v-table",
    components:{
        vtablerow
    },
    props: {
    users_data: {
        type: Array,
        defalt: ()=>{
            return []
        }
    }
    },
    data() {
    return {
        usersPerPage: 5,
        pageNumber: 1
    }
    },
    computed: {
        pages(){
            return Math.ceil(this.users_data.length/5);
        },
        paginatedUsers(){
            let from= (this.pageNumber-1) * this.usersPerPage;
            let to = from + this.usersPerPage;
            return this.users_data.slice(from,to);
        }
    },
    methods:{
        pageClick(page){
            this.pageNumber = page;
        }
    }
}
</script>
 <style>
  .v-table{
    max-width: 900px;
    margin: 0 auto;
  }
  .v-table_header{
    display: flex;
    justify-content: space-around;
  }
  .v-table_header p{
    flex-basis: 25%;
    text-align: left;
  }
  .v-table_pagination{
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    margin-top: 30px;
  }
  .page{
    padding: 8px;
  }
 </style>