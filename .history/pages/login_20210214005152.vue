<template>
  <div class="container">
    <div class="card">

        <form class="form-signin" @submit.prevent="login()">
            <p class="error-message">{{  errorMessage }}</p>
            <h1 class="h3 mb-3 font-weight-normal">Please sign in</h1>
            <label for="inputEmail" class="sr-only">Email address</label>
            <input type="email" v-model="loginForm.email" @change="hideErrorMessage" id="inputEmail" class="form-control" placeholder="Email address" required="" autofocus="">
            <label for="inputPassword" class="sr-only">Password</label>
            <input type="password" v-model="loginForm.password" id="inputPassword" class="form-control" placeholder="Password" required="">
            <div class="checkbox mb-3">
                <label>
                <input type="checkbox" value="remember-me"> Remember me
                </label>
            </div>
            <button class="btn btn-lg btn-primary btn-block" type="submit">Sign in</button>
        </form>
    </div>
  </div>
</template>

<script>
export default {
    middleware: ['guest'],
    data() {
        return {
            loginForm: {
                email: '',
                password: ''
            },
            errorMessage: ''
        }
    },

    methods: {
        async login() {
            console.log('values', this.loginForm);
            try {
                await this.$auth.loginWith('laravelSanctum', {data: this.loginForm})
            } catch (err) {
                this.errorMessage = err.response.data.message;
            }
        },

        hideErrorMessage() {
            this.errorMessage = '';
        }
    }
}
</script>

<style scoped>
.form-signin {
    width: 100%;
    max-width: 330px;
    padding: 15px;
    margin: auto;
}
.error-message {
    color: red;
}
</style>