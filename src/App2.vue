<template>
    <div>
    <el-button type="text" @click="InputDialogVisible = true">click to open the Dialog</el-button>
        <el-button type="primary" @click="HelloFunc">My Button</el-button>

    <el-dialog
            title=""
            :visible.sync="dialogVisible"
            width="30%"
            :before-close="handleClose">

        <el-form :model="ruleForm" status-icon :rules="rules" ref="ruleForm" label-width="120px" class="demo-ruleForm">
            <el-form-item label="Login" prop="login">
                <el-input type="login" v-model="ruleForm.pass" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="Password" prop="pass">
                <el-input type="password" v-model="ruleForm.login" autocomplete="off"></el-input>
            </el-form-item>
        </el-form>

        <span slot="footer" class="dialog-footer">
        <el-button @click="InputDialogVisible = false">Ок</el-button>
        <el-button type="primary" @click="InputDialogVisible = false">Отмена</el-button>
      </span>
    </el-dialog>
    </div>
</template>

<style>
    .demo-input-label {
        display: inline-block;
        width: 130px;
    }
</style>

<script>
    export default {
        data() {

            return {
                InputDialogVisible: false,
                PostForm: {
                    pass: '',
                    login: ''
                },
            };
        },
        methods: {
            handleClose(done) {
                this.$confirm('Are you sure to close this dialog?')
                    .then(_ => {
                        done();
                    })
                    .catch(_ => {});
            },
            HelloFunc() {
                console.log('HelloWorld!');
            }
        }
    };
</script>