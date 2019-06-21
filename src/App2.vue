<template>
    <div>
    <el-button type="text" @click="dialogVisible = true">click to open the Dialog</el-button>

    <el-dialog
            title=""
            :visible.sync="dialogVisible"
            width="30%"
            :before-close="handleClose">
        <div>
            <div class="demo-input-label">
                <span>Login: </span>
            </div>
            <div class="demo-input-label">
                <el-input placeholder="login" v-model="login"></el-input>
            </div>
        </div>


        <div>
            <div class="demo-input-label">
                <span>Pass: </span>
            </div>
            <div class="demo-input-label">
                <el-input placeholder="password" v-model="pass"></el-input>
            </div>
        </div>

        <span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">Ок</el-button>
        <el-button type="primary" @click="dialogVisible = false">Отмена</el-button>
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
                dialogVisible: false,
                login: '',
                pass: ''
            };
        },
        methods: {
            handleClose(done) {
                this.$confirm('Are you sure to close this dialog?')
                    .then(_ => {
                        done();
                    })
                    .catch(_ => {});
            }
        }
    };
</script>