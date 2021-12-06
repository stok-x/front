<template>
  <FormPage>
    <LoginForm></LoginForm>
  </FormPage>
</template>

<script>
import LoginForm from "../components/loginForm";
import FormPage from "./FormPage";

export default {
  name: "LoginPage",
  components: {FormPage, LoginForm}
}
</script>
