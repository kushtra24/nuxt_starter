<template>
  <div class="container">
    <div class="card">
        <form action=""></form>
      <b-button variant="primary" @click="login()">Login</b-button>
    </div>
  </div>
</template>

<script>
export default {
    middleware: ['guest'],
    data() {
        return {
            form: {
                email: 'admin@admin.com',
                password: 'password'
            }
        }
    },

    methods: {
        login() {
            this.$auth.loginWith('laravelSanctum', {data: this.form})
        }
    }
}
</script>
