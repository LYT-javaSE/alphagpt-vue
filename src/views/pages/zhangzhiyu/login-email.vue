<template>
    <div class="login-body">
        <h3 class="login-title">{{ $t('login.title') }}</h3>
        <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmitHandle()" status-icon>
            <el-form-item prop="email">
                <el-input v-model="dataForm.email" :placeholder="'请输入邮箱'">
                    <span slot="prefix" class="el-input__icon">
                      <svg class="icon-svg" aria-hidden="true"><use xlink:href="#icon-user"></use></svg>
                    </span>
                </el-input>
            </el-form-item>

            <el-form-item prop="code">
                <el-input class="code-input" v-model="dataForm.code" :placeholder="'请输入验证码'">
                    <span slot="prefix" class="el-input__icon">
                        <svg class="icon-svg" aria-hidden="true"><use xlink:href="#icon-user"></use></svg>
                    </span>
                </el-input>
                <el-button @click="sendMsg" type="primary" :disabled="isDisabled" class="send-button">{{buttonName}}</el-button>
            </el-form-item>

            <el-form-item>
                <el-button type="primary" @click="dataFormSubmitHandle()" class="w-percent-100">{{ $t('login.title') }}</el-button>
            </el-form-item>
        </el-form>
    </div>
</template>

<script>
    import Cookies from 'js-cookie'
    import debounce from 'lodash/debounce'
    import { isEmail } from '@/utils/validate'
    export default {
        data () {
            const validateConfirmPassword = (rule, value, callback) => {
                if (this.dataForm.password !== value) {
                    callback(new Error('确认密码与新密码不一致'))
                } else {
                    callback()
                }
            };
            const validateEmail = (rule, value, callback) => {
                if (!isEmail(value)) {
                    callback(new Error('邮箱格式错误'))
                } else {
                    callback()
                }
            };
            return {
                isDisabled: false,
                dataForm: {
                    email: '',
                    code: '',
                },
                buttonName: "获取验证码",
                time: 60,

            }
        },
        computed: {
            dataRule () {
                return {
                    email: [
                        { required: true, message: '邮箱不能为空', trigger: 'blur' },
                    ],
                    password: [
                        { required: true, message: this.$t('validate.required'), trigger: 'blur' }
                    ],
                    captcha: [
                        { required: true, message: this.$t('validate.required'), trigger: 'blur' }
                    ]
                }
            }
        },
        methods: {
            // 表单提交
            dataFormSubmitHandle: debounce(function () {
                this.$refs['dataForm'].validate((valid) => {
                    if (!valid) {
                        return false
                    }
                    this.$http.post('/login', this.dataForm).then(({ data: res }) => {
                        if (res.code !== 0) {
                            this.getCaptcha()
                            return this.$message.error(res.msg)
                        }
                        Cookies.set('token', res.data.token)
                        this.$router.replace({ name: 'home' })
                    }).catch(() => {})
                })
            }, 1000, { 'leading': true, 'trailing': false }),
            sendMsg() {
                this.$refs['dataForm'].validateField('email', error => {
                    if (!error) {
                        let me = this;
                        me.isDisabled = true;
                        let interval = window.setInterval(function() {
                            me.buttonName = '重新发送(' + me.time + ')';
                            --me.time;
                            if(me.time < 0) {
                                me.buttonName = "重新发送";
                                me.time = 60;
                                me.isDisabled = false;
                                window.clearInterval(interval);
                            }
                        }, 1000);
                    }
                })
            },
        }
    }
</script>

<style scoped>
    .code-input {
        position: relative;
        width: 56%;
        float: left;
    }
    .send-button {
        position: relative;
        width: 175px;
        float: left;
    }
</style>