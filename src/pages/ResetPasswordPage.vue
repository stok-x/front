<template>
  <FormPage>
    <ResetPasswordForm></ResetPasswordForm>
  </FormPage>
</template>

<script>
import FormPage from "./FormPage";
import ResetPasswordForm from "../components/ResetPasswordForm";

export default {
  name: "ResetPasswordPage",
  components: {ResetPasswordForm, FormPage}
}
</script>
