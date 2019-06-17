<template>
    <div class="addList">
        <div style="margin: 10px;"></div>
        <el-form :label-position="labelPosition" label-width="100px" :model="params">
        <el-form-item label="date">
            <el-input placeholder="date" v-model="params.date"></el-input><br>
        </el-form-item>
            <el-form-item label="category">
                <el-input placeholder="category" v-model="params.category"></el-input><br>
            </el-form-item>
            <el-form-item label="item">
                <el-input placeholder="item" v-model="params.item"></el-input><br>
            </el-form-item>
            <el-form-item label="price">

                <el-input placeholder="price" v-model="params.price"></el-input><br>
            </el-form-item>
            <el-form-item label="memo">
                <el-input placeholder="description" v-model="params.discription"></el-input>
            </el-form-item>
        </el-form>
        <el-button type="primary" icon="el-icon-circle-plus-outline" round @click="addDB"> ADD</el-button>
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

                usp.append('date', this.params.date);
                usp.append('category', this.params.category);
                usp.append('item', this.params.item);
                usp.append('price', this.params.price);
                usp.append('discription', this.params.discription);
                axios.post('http://localhost:4567/post', usp)
                    .then(
                        response => {
                            alert('test : ' + response.data)
                        }
                    )
                this.params.date = '';
                this.params.category = '';
                this.params.item = '';
                this.params.price = '';
                this.params.discription = '';

            }
        }

    }
</script>

<style scoped>
.el-input {
    width: 400px;
}
</style>