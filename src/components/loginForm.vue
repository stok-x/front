<template>
  <div class="bg-white rounded-5 shadow-5-strong p-5">
    <h2 class="title">Connexion</h2>
    <form id="loginForm" @submit.prevent="submit">
      <!-- Email input -->
      <div class="form-outline mb-4">
        <MDBInput label="Email" type="email" size="lg " v-model="state.email" required/>
          <span class="error-msg" v-if="v$.email.$error">L'email doit être renseigné !</span>
      </div>

      <!-- Password input -->
      <div class="form-outline mb-4">
        <div class="form-group">
          <MDBInput label="Mot de passe" type="password" size="lg" id="password" name="password" class="form-control"
                    v-model="state.password" required/>
          <span class="error-msg" v-if="v$.password.$error">Le mot de passe doit être renseigné !</span>
        </div>
      </div>

      <!-- 2 column grid layout for inline styling -->
      <div class="row mb-4">
        <div class="col d-flex justify-content-center">
          <!-- Checkbox -->
          <div class="form-check">
            <input class="form-check-input" type="checkbox" value="" id="remember-check" checked/>
            <label class="form-check-label" for="remember-check">
              Se souvenir de moi
            </label>
          </div>
        </div>

        <div class="col text-center">
          <!-- Simple link -->
          <router-link to="/reset-password">Mot de passe oublié?</router-link>
        </div>
      </div>
      <!-- Submit button -->
      <button type="submit" class="btn btn-block btn-submit">Se connecter</button>
    </form>
    <div class="col text-center">
      <!-- Simple link -->
      <span> Pas de compte ? <router-link to="/register">S'inscrire</router-link></span>
    </div>
  </div>
</template>

<script>
import {MDBInput} from 'mdb-vue-ui-kit';
import {computed, reactive} from "vue";
import {email, required} from "vuelidate/lib/validators";
import {useVuelidate} from "@vuelidate/core";

export default {
  name: "LoginForm",
  components: {
    MDBInput,
  },
  setup() {
    const state = reactive({
      email: '',
      password: ''
    })
    const rules = computed(() => {
      return {
        email: {required, email},
        password: {required}
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
};
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
  margin-bottom: 2vh;
}
.error-msg {
  color: #b71c1c;
}
</style>