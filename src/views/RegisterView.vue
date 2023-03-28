<script>
import { RouterLink } from "vue-router"
import axios from "axios"

export default {
    data(){
        return {
            name:"",
            email: "",
            password: "",
            error: "",
            success: "",
        }
    },
    methods: {
        async register() {
            try {
                const config = {
                    headers: {
                        "Content-type": "application/json"
                    }
                }

                const body = { email: this.email, password: this.password }

                const res = await axios.post("http://localhost:5000/auth/register", body, config)

                this.success = res.data.msg
                this.name:""
                this.email: ""
                this.password: ""

            } catch (error) {
                if(error.response.status === 403) {
                    this.error = error.response.data.message
                    setTimeout(() => {
                        this.error = ""
                    }, 5000);
                }
            }
        }
    }
}
</script>

<template>
    <main>
        <div class="login__Wrapper">
            <div class="login__Welcome">
                <h1>Verify</h1>
                <p>Register to create an account</p>
            </div>
            <form>
                <div class="error">
                    <p>{{ error }}</p>
                </div>
                <div class="success">
                    <p>{{ success }}</p>
                </div>
                <div class="login__InputDiv">
                    <input type="text" name="name" id="" required v-model="name">
                    <label for="">Full name</label>
                </div>
                <div class="login__InputDiv">
                    <input type="email" name="email" id="" required v-model="email">
                    <label for="">Email</label>
                </div>
                <div class="login__InputDiv">
                    <input type="password" name="password" id="" required v-model="password">
                    <label for="">Password</label>
                </div>
                <div class="login__Dialogue">
                    <p>By Registering you agreeing to our<RouterLink to="#"> terms and conditions</RouterLink></p>
                </div>
                <div class="login__Button">
                    <button type="button" v-on:click="register">Register</button>
                </div>
            </form>
            <div class="login__Exit">
                <p>Already have an account? <RouterLink to="/login">Login Now</RouterLink></p>
            </div>
        </div>
    </main>
</template>

<style lang="scss" scoped>
    main {
        position: relative;
        min-height: 100vh;
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        .login__Wrapper {
            min-width: 350px;
            box-shadow: 0 0 5px 3px rgba($color: #707070, $alpha: 0.15);
            padding: 60px;
            .login__Welcome{
                margin-bottom: 20px;
                text-align: center;
                h1{
                    font-weight: 800;
                    font-size: 30px;
                    color: rgb(64, 136, 231);
                    font-family: 'Comfortaa', cursive;
                }
                p{
                    // font-weight: 600;
                    font-style: italic;
                }
            }
            form {
                width: 100%;
                .error {
                    color: red;
                    margin-bottom: 10px;
                }
                .success {
                    color: green;
                    margin-bottom: 10px;
                }
                .login__InputDiv{
                    position: relative;
                    margin-bottom: 20px;
                    input {
                        width: 350px;
                        padding: 7px 20px;
                        font-size: 16px;
                        outline: none;
                        border-radius: 5px;
                        border: 1px solid #707070;
                        &:focus ~ label, &:valid ~ label {
                            top: -12px;
                            left: 5px;
                            padding: 0 3px;
                            font-size: 12px;
                            transition: all .2s linear;
                            background-color: #fff;
                        }
                    }
                    label {
                        position: absolute;
                        top: 6px;
                        left: 20px;
                        pointer-events: none;
                    }
                }
                .login__Dialogue {
                    display: flex;
                    justify-content: flex-end;
                    margin-bottom: 20px;
                    a{
                        font-size: 12px;
                        font-weight: 700;
                        text-decoration: none;
                        color: rgb(64, 136, 231);
                    }
                }
                .login__Button {
                    text-align: center;
                    margin-bottom: 20px;
                    button{
                        padding: 10px 25px;
                        font-weight: 700;
                        background-color: rgb(64, 136, 231);
                        color: #fff;
                        border: none;
                        border-radius: 5px;
                        cursor: pointer;
                    }
                }
            }
            .login__Exit {
                text-align: center;
                font-weight: 700;
                a{
                    font-style: italic;
                    text-decoration: none;
                        color: rgb(64, 136, 231);
                }
            }
        }
    }

    @media (max-width: 470px) {
        main .login__Wrapper{
            padding: 40px 20px;
            form .login__InputDiv input {
                width: 100%;
            }
        }
}
</style>