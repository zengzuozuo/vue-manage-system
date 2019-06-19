<template>
    <div class="login-wrap">
        <header>
            <div class="flex-wrap">
                <div class="logo">
                    <h3>后台管理系统</h3>
                </div>
                <div class="link">
                    <a href="javascript:;">开发者中心</a>
                </div>
            </div>
        </header>
        <div class="main">
            <div class="confine">
                <div class="ms-login">
                    <div class="ms-title">商户后台 <span class="primary-ft-c">登录</span></div>
                    <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="0px" class="ms-content">
                        <el-form-item prop="username">
                            <el-input v-model="ruleForm.username" placeholder="username" autofocus></el-input>
                        </el-form-item>
                        <el-form-item prop="password">
                            <el-input type="password" placeholder="password" v-model="ruleForm.password" @keyup.enter.native="submitForm('ruleForm')"></el-input>
                        </el-form-item>
                        <div class="login-btn">
                            <el-button type="primary" @click="submitForm('ruleForm')">登录</el-button>
                        </div>
                        <div class="other">
                            <el-checkbox v-model="checked">保持登录状态</el-checkbox>
                        </div>
                    </el-form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data: function(){
            return {
                ruleForm: {
                    username: 'admin',
                    password: '123123'
                },
                rules: {
                    username: [
                        { required: true, message: '请输入用户名', trigger: 'blur' }
                    ],
                    password: [
                        { required: true, message: '请输入密码', trigger: 'blur' }
                    ]
                },
                checked: false
            }
        },
        methods: {
            submitForm(formName) {
                this.$refs[formName].validate((valid) => {
                    if (valid) {
                        localStorage.setItem('ms_username',this.ruleForm.username);
                        this.$router.push('/');
                    } else {
                        console.log('error submit!!');
                        return false;
                    }
                });
            }
        }
    }
</script>

<style scoped lang="less">
    @confineWidth: 1000px;
    .login-wrap{
        position: relative;
        width:100%;
        height:100%;
        header {
            background-color: #fff;
            .flex-wrap {
                display: flex;
                align-items: center;
                justify-content: space-between;
                height: 80px;
                max-width: @confineWidth;
                box-sizing: border-box;
                padding: 0 10px;
                margin: 0 auto;
                .logo {
                    color: #1890FF;
                    font-size: 20px;
                    h3 {
                        font-weight: 500;
                    }
                }
                .link {
                    a {
                        color: #323232;
                        font-size: 18px;
                        font-weight: 500;
                        &:hover {
                            text-decoration: underline;
                        }
                    }
                }
            }
        }
        .main {
            position: absolute;
            top: 80px;
            left: 0;
            width: 100%;
            height: calc(100% - 80px);
            background: url(../../../public/img/login_bg.png) no-repeat center;
            background-size: cover;
            .confine {
                position: relative;
                max-width: @confineWidth;
                height: 100%;
                margin: 0 auto;
                .ms-title{
                    width:100%;
                    line-height: 50px;
                    font-size:20px;
                    color: #000;
                    padding: 0 30px;
                }
                .other {
                    text-align: center;
                    margin: 10px 0;
                }
            }
        }
    }
    
    .ms-login{
        position: absolute;
        right: 10px;
        top:50%;
        width: 350px;
        margin:-190px 0 0 0;
        border-radius: 2px;
        background: #fff;
        overflow: hidden;
        padding: 10px 0;
    }
    .ms-content{
        padding: 10px 30px 0 30px;
    }
    .login-btn{
        text-align: center;
    }
    .login-btn button{
        width:100%;
        height:36px;
        margin-bottom: 10px;
    }
    .login-tips{
        font-size:12px;
        line-height:30px;
        color:#fff;
    }
</style>