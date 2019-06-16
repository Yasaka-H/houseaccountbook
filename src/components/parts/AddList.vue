<template>
    <div class="addList">
        <div style="margin: 10px;"></div>
        <el-form :label-position="labelPosition" label-width="100px" :model="params">
        <el-form-item label="日付">
            <el-input placeholder="date" v-model="params.date"></el-input><br>
        </el-form-item>
            <el-form-item label="費目">
                <el-input placeholder="category" v-model="params.category"></el-input><br>
            </el-form-item>
            <el-form-item label="買ったもの">
                <el-input placeholder="item" v-model="params.item"></el-input><br>
            </el-form-item>
            <el-form-item label="値段">

                <el-input placeholder="price" v-model="params.price"></el-input><br>
            </el-form-item>
            <el-form-item label="メモ">
                <el-input placeholder="discription" v-model="params.discription"></el-input>
            </el-form-item>
        </el-form>
        <el-button type="primary" icon="el-icon-circle-plus-outline" round @click="addDB"> 追加</el-button>
    </div>
</template>

<script>
    import axios from 'axios'
    export default {
        name: "AddList",
        data() {
            return {
                labelPosition: 'right',
                params: {
                    date: '',
                    category: '',
                    item: '',
                    price: '',
                    discription: ''
                }
            }
        },
        methods: {
            addDB() {
                let usp = new URLSearchParams();

                usp.append('params', this.params);
                axios.post('http://localhost:4567/post', usp)
                    .then(
                        response => {
                            alert('test : ' + response.data)
                        }
                    )

            //     axios.post('http://localhost:4567/post', {
            //         date: this.params.date,
            //         category: this.params.category,
            //         item: this.params.item,
            //
                //  price: this.params.price,
            //         discription: this.params.discription
            // })

            }
        }

    }
</script>

<style scoped>
.el-input {
    width: 400px;
}
</style>