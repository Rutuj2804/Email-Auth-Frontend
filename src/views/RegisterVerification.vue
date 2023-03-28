<script>
import { RouterLink } from "vue-router"
import axios from "axios"

export default {
    data() {
        return {
            id: '',
            msg: "",
            isLoading: false
        }
    },
    async created() {
        this.id = this.$route.params.id;
        try { 
                this.isLoading = true
                const config = {
                    headers: {
                        "Content-type": "application/json"
                    }
                }

                const res = await axios.get(`http://localhost:5000/auth/verify/${this.id}`, config)
                this.msg = res.data.msg
                this.isLoading = false

            } catch (error) {
                if(error.response.status === 403) {
                    this.msg = error.response.data.message
                }
                this.isLoading = false
            }
    }
}
</script>

<template>
    <main>
        <div class="block">
            <h1>Registration Verification</h1>
            <p>
                {{this.isLoading ?  "Please wait, your email is under verification" : this.msg}}
            </p>
            <RouterLink to="/login">
                Proceed to Login
            </RouterLink>
        </div>
    </main>
</template>

<style scoped lang="scss">
    main {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 80vh;
        .block {
            box-shadow: 0 0 5px 3px rgba($color: #707070, $alpha: 0.15);
            padding: 60px;
            text-align: center;
            h1 {
                margin-bottom: 20px;
                    font-family: 'Comfortaa', cursive;
            }
            p{
                margin-bottom: 20px;
            }
        }
    }
</style>