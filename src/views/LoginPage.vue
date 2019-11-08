<template>
  <div id="login-register-page">
    <div>
      <img src alt />
    </div>
    <div class="form-structor">
      <div class="signup" :class="{'slide-up': loginSite}">
        <h2 class="form-title" id="signup" @click="siteSwap">
          <span>or</span>Create Account
        </h2>
        <div class="form-holder">
          <input type="text" class="input" placeholder="Name" v-model="username" />
          <input type="email" class="input" placeholder="Email" v-model="email" />
          <input type="password" class="input" placeholder="Password" v-model="password" />
        </div>
        <button class="submit-btn" @click="signUp">Sign up</button>
      </div>
      <div class="login" :class="{'slide-up': !loginSite}">
        <div class="center">
          <h2 class="form-title" id="login" @click="siteSwap">
            <span>or</span>Log in
          </h2>
          <div class="form-holder">
            <input type="email" class="input" placeholder="Email" v-model="email" />
            <input type="password" class="input" placeholder="Password" v-model="password" />
          </div>
          <button class="submit-btn" @click="signIn">Log in</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import swal from "sweetalert2";

const axiosReq = axios.create({
  baseURL: "http://localhost:3000"
});

export default {
  data() {
    return {
      username: "",
      email: "",
      password: "",
      loginSite: false
    };
  },
  methods: {
    siteSwap() {
      this.loginSite = !this.loginSite;
    },
    signUp() {
      axiosReq({
        method: "post",
        url: "users/register",
        data: {
          username: this.username,
          email: this.email,
          password: this.password
        }
      })
        .then(({ data }) => {
          swal.fire("Success", "Register Success!");
          this.loginSite = !this.loginSite;
          this.email = "";
          this.username = "";
        })
        .catch(({ response }) => {
          swal.fire("Error", response.data.message.join(". "));
          console.log(response.data.message);
        })
        .finally(() => {
          this.password = "";
        });
    },
    signIn() {
      axiosReq({
        method: "post",
        url: "users/login",
        data: {
          email: this.email,
          password: this.password
        }
      })
        .then(({ data }) => {
          localStorage.setItem("access_token", data.access_token);
          swal.fire("Success", "Login Success!");
          this.$emit("logged-in");
          this.email = "";
        })
        .catch(({ response }) => {
          swal.fire("Error", response.data.message);
        })
        .finally(() => {
          this.password = "";
        });
    }
  },
  created() {
    if (localStorage.getItem("access_token")) this.$emit("logged-in");
  }
};
</script>

<style>
</style>