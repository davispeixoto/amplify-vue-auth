<template>
    <div>
        <h2>Sign In</h2>
        <div class="formcontainer">
            <input type="text" v-model="form.username" class="input" />
            <input type="password" v-model="form.password" class="input" />
            <button v-on:click="signIn" class="button">Sign In</button>
        </div>
    </div>
</template>

<script>
    import { Auth } from "aws-amplify"
    import { AmplifyEventBus } from "aws-amplify-vue"

    export default {
        name: "SignIn",
        data() {
            return {
                form: {
                    username: '',
                    password: '',
                }
            }
        },
        methods: {
            async signIn() {
                const { username, password } = this.form
                await Auth.signIn(username, password)
                AmplifyEventBus.$emit('authState', 'signedIn')
                this.$router.push('/profile')
            }
        }
    }
</script>

<style scoped>
    .formcontainer {
        display: flex;
        flex-direction: column;
        width: 500px;
        margin: 0 auto;
    }
    .input {
        margin-bottom: 7px;
        height: 38px;
        border: none;
        outline: none;
        border-bottom: 2px solid #ddd;
        font-size: 20px;
    }
    .button {
        height: 45px;
        border: none;
        outline: none;
        background-color: #dddddd;
        margin-top: 8px;
        cursor: pointer;
        font-size: 18px;
    }
    .button:hover {
        opacity: .7
    }
</style>
