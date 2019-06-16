<template>
    <div>
    <!---
    <div class="showList" v-for="item in inOutList">

    </div>
    <span v-for="item in inOutList" v-bind:key="item.id">
        <p>{{ item.id }} {{ item.date }} {{ item.category }} {{ item.item }} {{ item.price }} {{ item.discription }}</p>
    </span> --->
        <template>
            <el-table
                    :data="inOutList"
                    style="width: 100%">
                <el-table-column
                        prop="date"
                        label="Date"
                        width="180"></el-table-column>
                <el-table-column
                        prop="category"
                        label="Category"
                        width="180"></el-table-column>
                <el-table-column
                        prop="item"
                        label="Item"
                        width="180"></el-table-column>
                <el-table-column
                    prop="price"
                    label="Price"
                    width="180"></el-table-column>
                <el-table-column
                    prop="discription"
                    label="Discription"
                    width="180"></el-table-column>
            </el-table>
        </template>
    <AddList />
    </div>
</template>

<script>
    import axios from 'axios'

    import AddList from './parts/AddList.vue'
    export default {
        name: "ListBoard",
        data() {
            return {
                inOutList: [],
                loading: true,
                errored: false,
            }
        },
        components:{
            AddList
        },
        mounted() {
            axios.get('http://localhost:4567/get_all')
                .then(
                    response=>{
                        this.inOutList = response.data
                        // this.data.inOutList = JSON.parse(this.getList)
                        // console.log(this.getList)
                    }
                ).catch(
                    error =>{
                        alert(error)
                        this.errored = true
                    }
            )
        }
    }
</script>

<style scoped>

</style>