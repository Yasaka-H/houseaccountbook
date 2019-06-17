<template>
    <div>
        <div>
            <h3>Attention!!!</h3>
            <p>未完成です。入力フォームへの正しくない入力などを弾く機能は実装していません。優しく使ってあげてください</p>
            <ul>
                実装済み機能
                <li>初期、データベースをサーバーから取得、クライアントで表示</li>
                <li>データベースへの登録(自動でリストはリロードされません)</li>
                <li>リスト表示のリロード</li>
                <li>削除機能はボタンだけ実装で中身はありません</li>
            </ul>
        </div>
        <el-button type="primary" round @click="reloadList"> RELOAD</el-button>

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
                <el-table-column label="Delete" prop="id" width="80" >

                    <el-button type="danger" icon="el-icon-delete" circle @click.native.prevent="deleteList(id)"></el-button>
                </el-table-column>
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
                id: ''
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
                    }
                ).catch(
                    error =>{
                        alert(error)
                        this.errored = true
                    }
            )

        },
        methods: {
            reloadList() {
                axios.get('http://localhost:4567/get_all')
                    .then(
                        response=>{
                            this.inOutList = response.data
                        }
                    ).catch(
                    error =>{
                        alert(error)
                        this.errored = true
                    }
                )
            },
            deleteList: function(id) {
                alert(id)
                axios.delete('http://localhost:4567/delete?id=' + id)
                    .then(
                        response => {
                            alert('This delete is '+ response.data)
                        }
                    )
            }
        }
    }
</script>

<style scoped>

</style>