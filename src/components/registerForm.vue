<template>
  <div class="bg-white rounded-5 shadow-5-strong p-5">
    <h2 class="title">Inscription</h2>
    <form id="loginForm" @submit.prevent="submit">
      <!-- Username input -->
      <div class="form-outline mb-4">
        <MDBInput label="Username" type="text" size="lg " v-model="state.username" required/>
        <span class="error-msg" v-if="this.v$.username.$error">Le nom d'utilisateur doit faire au maximum 20 caractères !</span>
      </div>
      <!-- Email input -->
      <div class="form-outline mb-4">
        <MDBInput label="Email" type="email" size="lg " v-model="state.email" required/>
        <span class="error-msg" v-if="this.v$.email.$error">Email invalide !</span>
      </div>
      <!-- Password input -->
      <div class="form-outline mb-4">
        <div class="form-group">
          <MDBInput label="Mot de passe" type="text" size="lg " id="password" v-model="state.password"
                    name="password" required/>
          <span class="error-msg" v-if="this.v$.password.$error">Le mot de passe doit faire au moins 12 caractères et contenir au moins 1 chiffre, 1 majuscule, 1 minuscule et un caractère spécial !</span>
        </div>
      </div>
      <div class="form-group">
        <MDBInput label="Confirmer mot de passe" type="text" size="lg " id="confirmPassword" v-model="state.confirmPassword"
                  name="confirmPassword" required/>
        <span class="error-msg" v-if="this.v$.confirmPassword.$error">Les mots de passe ne sont pas identiques !</span>
        <span class="error-msg" v-if="this.v$.confirmPassword.$error">Les mots de passe ne sont pas identiques !</span>
      </div>

      <!-- Submit button -->
      <button type="submit" class="btn btn-block btn-submit">S'inscrire</button>
    </form>
    <div class="col text-center">
      <!-- Simple link -->
      <span> Déjà inscrit ? <router-link to="/login">Se connecter</router-link></span>
    </div>
  </div>
</template>

<script>
import {reactive, computed} from "vue";
import {required, email, minLength, maxLength, sameAs} from "vuelidate/lib/validators";
import {useVuelidate} from "@vuelidate/core";
import {MDBInput} from 'mdb-vue-ui-kit';

export default {
  name: "RegisterForm",
  components: {
    MDBInput,
  },
  setup() {
    const state = reactive({
      username: '',
      email: '',
      password: '',
      confirmPassword: ''
    })
    const rules = computed(() => {
      return {
        username: {required, max: maxLength(20) },
        email: {required, email},
        password: {
          required,
          valid: function (value) {
            const containsUppercase = /[A-Z]/.test(value);
            const containsLowercase = /[a-z]/.test(value);
            const containsNumber = /[0-9]/.test(value);
            const containsSpecial = /[#?!@$%^&*-]/.test(value);
            return (
              containsUppercase &&
              containsLowercase &&
              containsNumber &&
              containsSpecial
            );
          },
          minLength: minLength(12),
        },
        confirmPassword: {required, sameAs: sameAs('password') }
      }
    })
    const v$ = useVuelidate(rules, state)

    return {state, v$}
  },
  methods: {
    submit() {
      this.v$.$validate()
      if (!this.v$.$error) {
        console.log("SENT !")
      }
    }
  }
}
</script>

<style scoped>
.title {
  text-align: center;
  padding-bottom: 3vh;
}

.btn-submit {
  /* Chrome 10-25, Safari 5.1-6 */
  background: -webkit-linear-gradient(to right, rgba(252, 203, 144, 0.9), rgba(213, 126, 235, 0.9));
  /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  background: linear-gradient(to right, rgba(252, 203, 144, 0.9), rgba(213, 126, 235, 0.9));
  font-weight: bold;
  margin-top: 2vh;
  margin-bottom: 2vh;
}

.error-msg {
  color: #b71c1c;
}
</style>