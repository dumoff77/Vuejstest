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
                    PostForm.name = scope.row.name,
                    PostForm.number = scope.row.number,
                    PostForm.description = scope.row.description" type="text" size="small">Edit</el-button>
                </template>
            </el-table-column>
        </el-table>

        <el-button type="primary" @click="InputDialogVisible = true,
        PostForm.name = PostForm.number = PostForm.description = ''">Add new record</el-button>
        <el-dialog
                title=""
                :visible.sync="InputDialogVisible"
                width="30%"
                :before-close="handleClose">
            <el-form :model="PostForm" status-icon ref="ruleForm" label-width="120px" class="demo-ruleForm">
                <el-form-item label="Имя" prop="first_name">
                    <el-input type="login" v-model="PostForm.name" autocomplete="off"></el-input>
                </el-form-item>
                <el-form-item label="Телефон" prop="tel_number">
                    <el-input type="tel_number" v-model="PostForm.number" autocomplete="off"></el-input>
                </el-form-item>
                <el-form-item label="Описание" prop="desc">
                    <el-input type="desc" v-model="PostForm.description" autocomplete="off"></el-input>
                </el-form-item>
            </el-form>

            <span slot="footer" class="dialog-footer">
                <el-button @click="InputDialogVisible = false,
                UpdateHandbook()">Обновить</el-button>
                <el-button :visible.sync="InputButtonVisible" @click="InputDialogVisible = false,
                SetHandbook()">Сохранить</el-button>
                <el-button type="primary" @click="InputDialogVisible = false">Отмена</el-button>
            </span>
        </el-dialog>

        <el-dialog
                title="Вы уверены что хотите удалить запись"
                :visible.sync="DeleteDialogVisible"
                width="30%"
                :before-close="handleClose">
            <span slot="footer" class="dialog-footer">
                <el-button @click="deleteHandbook(), DeleteDialogVisible = false" type="success" size="medium">Delete</el-button>
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
                    name: '',
                    number: '',
                    description: ''
                },
                tableData: [
                    {
                    number: '0980446512',
                    name: 'Valera',
                    description: 'best friend'
                },
                    {
                    number: '0675487457',
                    name: 'Vasya',
                    description: 'classmate'
                }
                ]
            }
        },
        methods: {
            UpdateHandbook() {
                axios.put('/api/handbook/'+this.PostForm.name ,this.PostForm);
                this.tableData.pop(this.PostForm);
                this.tableData.push(this.PostForm);
            },
            SetHandbook() {
                axios.post('/api/handbook',this.PostForm);
                this.tableData.push(this.PostForm);
            },
            deleteHandbook() {
                axios.delete('/api/handbook/'+this.DeleteRecordBuffer.row.name);
                this.tableData.pop(this.DeleteRecordBuffer.row);
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