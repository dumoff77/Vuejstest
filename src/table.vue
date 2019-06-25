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
                    <el-button @click="DeleteRecordBuffer = scope, DeleteDialogVisible = true" type="text" size="small">Delete</el-button>
                    <el-button @click="InputDialogVisible = true,
                    PostForm.first_name = scope.row.name,
                    PostForm.tel_number = scope.row.number,
                    PostForm.desc = scope.row.description" type="text" size="small">Edit</el-button>
                </template>
            </el-table-column>
        </el-table>

        <el-button type="primary" @click="InputDialogVisible = true,
        PostForm.first_name = PostForm.tel_number = PostForm.desc = ''">Add new record</el-button>
        <el-dialog
                title=""
                :visible.sync="InputDialogVisible"
                width="30%"
                :before-close="handleClose">
            <el-form :model="PostForm" status-icon ref="ruleForm" label-width="120px" class="demo-ruleForm">
                <el-form-item label="Имя" prop="first_name">
                    <el-input type="login" v-model="PostForm.first_name" autocomplete="off"></el-input>
                </el-form-item>
                <el-form-item label="Телефон" prop="tel_number">
                    <el-input type="tel_number" v-model="PostForm.tel_number" autocomplete="off"></el-input>
                </el-form-item>
                <el-form-item label="Описание" prop="desc">
                    <el-input type="desc" v-model="PostForm.desc" autocomplete="off"></el-input>
                </el-form-item>
            </el-form>

            <span slot="footer" class="dialog-footer">
                <el-button @click="InputDialogVisible = false,
                UpdateHandbook(PostForm.first_name,PostForm.tel_number,PostForm.desc)">Обновить</el-button>
                <el-button :visible.sync="InputButtonVisible" @click="InputDialogVisible = false,
                SetHandbook(PostForm.first_name,PostForm.tel_number,PostForm.desc)">Сохранить</el-button>
                <el-button type="primary" @click="InputDialogVisible = false">Отмена</el-button>
            </span>
        </el-dialog>

        <el-dialog
                title="Вы уверены что хотите удалить запись"
                :visible.sync="DeleteDialogVisible"
                width="30%"
                :before-close="handleClose">
            <span slot="footer" class="dialog-footer">
                <el-button @click="deleteHandbook(DeleteRecordBuffer.row.name), DeleteDialogVisible = false" type="success" size="medium">Delete</el-button>
                <el-button type="danger" size="medium" @click="DeleteDialogVisible = false">Отмена</el-button>
            </span>
        </el-dialog>
    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        name: "table",
        data() {
            return {
                DeleteRecordBuffer: '',
                InputButtonVisible: false,
                InputDialogVisible: false,
                DeleteDialogVisible: false,
                PostForm: {
                    first_name: '',
                    tel_number: '',
                    desc: ''
                },
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
        methods: {
            UpdatePage() {
                axios.get('/api/handbook').then(response => {
                    this.tableData = response.data;
                })
            },
            UpdateHandbook(first_name,tel_number,desc) {
                console.log(first_name,tel_number,desc)
                axios.put('/api/handbook/'+first_name,{ "name":first_name, "number":tel_number, "description":desc })
            },
            SetHandbook(first_name,tel_number,desc) {
                axios.post('/api/handbook',{ "name":first_name, "number":tel_number, "description":desc })
            },
            deleteHandbook(mydata) {
                axios.delete('/api/handbook/'+mydata);
            },
            handleClose(done) {
                this.$confirm('Are you sure to close this dialog?')
                    .then(_ => {
                        done();
                    })
                    .catch(_ => {});
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