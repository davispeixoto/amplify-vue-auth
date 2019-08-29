<template>
    <div class="auth">
        <sign-up :toggle="toggle" v-if="formState === 'signUp'"></sign-up>
        <sign-in v-if="formState === 'signIn'"></sign-in>
        <p v-on:click="toggle" class="toggle">
            {{
                formState === 'signUp' ?
                'Already sign up? Sign In' :
                'Need an account? Sign Up'
            }}
        </p>
    </div>
</template>

<script>
    import { AmplifyEventBus } from "aws-amplify-vue"
    import SignIn from "./SignIn"
    import SignUp from "./SignUp"

    export default {
        name: 'auth',
        data() {
            return {
                formState: 'signUp'
            }
        },
        methods: {
            toggle() {
                this.formState === 'signUp' ? this.formState = 'signIn' : this.formState = 'signUp'
            }
        },
        components: {
            SignIn,
            SignUp
        }
    }
</script>

<style>
    .auth {
        margin: 0 auto;
        width: 460px;
    }
    .toggle {
        cursor: pointer;
        font-size: 18px;
    }
</style>
