<template>
  <div class="login-page h-full min-h-screen flex justify-center items-center">
    <v-sheet width="400" class="">
      <h2 class="text-3xl mb-8 text-center font-bold text-gray">Login</h2>
      <v-form fast-fail @submit.prevent="login">
        <v-text-field
          v-model="username"
          label="Username"
          :rules="usernameRules"
        ></v-text-field>

        <v-text-field
          v-model="password"
          label="Password "
          :rules="passwordRules"
        ></v-text-field>

        <v-btn type="submit" block class="mt-2">Submit</v-btn>
      </v-form>
      <p class="mt-[19px]">
        Don't have an account
        <span
          class="font-bold cursor-pointer text-brand"
          @click="$router.push('/register')"
          >Sign Up</span
        >
      </p>
    </v-sheet>
  </div>
</template>

<script>
import http from "../../../axios.config";
import { setToLocalStorage } from "../../../utils/localStorage";
import { useToast } from "vue-toastification";
export default {
  data: () => ({
    toast: useToast(),
    username: "",
    usernameRules: [
      (value) => {
        if (value?.length > 3) return true;

        return "First name must be at least 3 characters.";
      },
    ],
    password: "",
    passwordRules: [
      (value) => {
        if (/[^0-9]/.test(value)) return true;
        return "Last name can not contain digits.";
      },
    ],
  }),
  methods: {
    async login() {
      try {
        const res = await http.post("auth/login", {
          username: this.username,
          password: this.password,
        });
        if (res) {
          setToLocalStorage("access_token", res.data.access_token);
          this.toast.success("You  are welcome");
          this.$router.push("/");
        }
        if (this.passwordRules && this.usernameRules) return;
      } catch (err) {
        this.toast.error(err.response.data.message);
        console.log(err);
      }
    },
  },
};
</script>
