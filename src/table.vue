<template>
    <el-table
            :data="tableData"
            style="width: 50%">
        <el-table-column
                fixed
                prop="name"
                label="Имя"
                width="150">
        </el-table-column>

        <el-table-column
                prop="number"
                label="Телефон"
                width="120">
        </el-table-column>

        <el-table-column
                prop="description"
                label="описание"
                width="120">
        </el-table-column>

        <el-table-column
                label="Управление"
                width="120">
            <template slot-scope="scope">
                <el-button @click="handleClick" type="text" size="small">Delete</el-button>
                <el-button type="text" size="small">Edit</el-button>
            </template>
        </el-table-column>
    </el-table>
</template>

<script>
    export default {
        name: "table",
        methods: {
            handleClick() {
                console.log('click');
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
        }
    }
</script>

<style scoped>

</style>