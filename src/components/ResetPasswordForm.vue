<template>
  <div class="bg-white rounded-5 shadow-5-strong p-5">
    <h2 class="title">Ré-initialisation du mot de passe</h2>
    <form id="loginForm" @submit.prevent="submit" v-if="resetPasswordSent === false">
      <!-- Email input -->
      <div class="form-outline mb-4">
        <MDBInput label="Email" type="email" size="lg " v-model="state.email" required/>
        <span class="error-msg" v-if="v$.email.$error">L'email doit être renseigné !</span>
      </div>
      <!-- Submit button -->
      <button type="submit" class="btn btn-block btn-submit">Envoyer un nouveau mot de passe </button>
      <div class="col text-center">
        <span><router-link to="/login">Retourner à la page de connexion</router-link></span>
      </div>
    </form>
    <div v-else class="row mb-4 text-center">
      <span>Un nouveau mot de passe vous a été envoyé ! </span>
      <span><router-link to="/login">Me connecter</router-link></span>
    </div>
  </div>
</template>

<script>
import {MDBInput} from 'mdb-vue-ui-kit';
import {computed, reactive} from "vue";
import {email, required} from "vuelidate/lib/validators";
import {useVuelidate} from "@vuelidate/core";

export default {
  name: "ResetPasswordPage",
  components: {
    MDBInput,
  },
  data() {
    return {
      resetPasswordSent: false
    }
  },
  setup() {
    const state = reactive({
      email: ''
    })
    const rules = computed(() => {
      return {
        email: {required, email}
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
        this.resetPasswordSent = true;
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