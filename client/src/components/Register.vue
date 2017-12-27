<template>
  <v-layout column>
    <v-flex xs6 offset-xs3>
      <panel title="Register">
        <form>
        <v-text-field name="email" label="Email" v-model="email">
        </v-text-field>

        <v-text-field name="password" label="Password" autocomplete="new-password" hint="At least 8 characters" v-model="password"
          min="8" :append-icon="e1 ? 'visibility' : 'visibility_off'" :append-icon-cb="() => (e1 = !e1)" :type="e1 ? 'password' : 'text'"
          counter>
        </v-text-field>
        <br>
        <v-alert class="ml-4" :value="error" transition="scale-transition" error>
          {{error}}
        </v-alert>
        <br>
        <v-btn dark class="cyan" @click="register">
          Register
        </v-btn>
        </form>
      </panel>
    </v-flex>
  </v-layout>
</template>

<script>
  import AuthenticationService from '@/services/AuthenticationService'
  import Panel from '@/components/Panel'

  export default {
    data () {
      return {
        email: '',
        password: '',
        e1: true,
        error: null
      }
    },
    components: {
      Panel
    },
    methods: {
      async register () {
        try {
          const response = await AuthenticationService.register({
            email: this.email,
            password: this.password
          })
          this.$store.dispatch('setToken', response.data.token)
          this.$store.dispatch('setUser', response.data.user)
        } catch (error) {
          this.error = error.response.data.error
        }
      }
    }
  }
</script>

<style scoped>
</style>