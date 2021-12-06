<template>
  <FormPage>
    <RegisterForm></RegisterForm>
  </FormPage>
</template>

<script>

import RegisterForm from "../components/registerForm";
import FormPage from "./FormPage";
export default {
  name: "RegisterPage",
  components: {FormPage, RegisterForm}
}
</script>