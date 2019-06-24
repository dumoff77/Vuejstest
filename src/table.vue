<template>
    <div>
        <el-table
                :data="tableData"
                style="width: 50%">
            <el-table-column
                    fixed
                    label="Имя"
                    width="150">
                <template slot-scope="scope">
                    {{ scope.row.name }}
                </template>
            </el-table-column>

            <el-table-column
                    label="Телефон"
                    width="120">
                <template slot-scope="scope">
                    {{ scope.row.number }}
                </template>
            </el-table-column>

            <el-table-column
                    label="описание"
                    width="120">
                <template slot-scope="scope">
                    {{ scope.row.description }}
                </template>
            </el-table-column>

            <el-table-column
                    label="Управление"
                    width="120">
                <template slot-scope="scope">
                    <el-button @click="deleteHandbook(scope.row.name)" type="text" size="small">Delete</el-button>
                    <el-button @click="handleClick" type="text" size="small">Edit</el-button>
                </template>
            </el-table-column>
        </el-table>

        <div class="demo-form-inline">
            <el-row>
                <el-input
                        size="medium"
                        placeholder="Please Input"
                        v-model="input2">
                </el-input>
                <el-input
                        size="medium"
                        placeholder="Please Input"
                        v-model="input3">
                </el-input>
                <el-input
                        placeholder="Please Input"
                        v-model="input4">
                </el-input>
                <el-button @click="setCurrent()">Clear selection</el-button>
            </el-row>


        </div>
    </div>

</template>


<script>
    import axios from 'axios';
    export default {
        name: "table",
        methods: {
            handleClick() {
                console.log('handleClick');
            },
            deleteHandbook(mydata) {
                axios.delete('/api/handbook/'+mydata);
                console.log(mydata)
            }
        },
        data() {
            return {
                tableData: [{
                    number: '0980446512',
                    name: 'Valera',
                    description: 'best friend'
                }, {
                    number: '0675487457',
                    name: 'Vasya',
                    description: 'classmate'
                }]
            }
        },
        mounted() {
            axios.get('/api/handbook').then(response => {
                this.tableData = response.data;
            })
        }
    }
</script>

<style scoped>

</style>