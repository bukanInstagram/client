<template>
  <div>
    <div id="login-register-page">
      <div>
        <img src alt />
      </div>
      <div class="form-structor">
        <div class="signup">
          <h2 class="form-title" id="signup">
            <span>or</span>Create Account
          </h2>
          <div class="form-holder">
            <input type="text" class="input" placeholder="Name" v-model="username" />
            <input type="email" class="input" placeholder="Email" v-model="email" />
            <input type="password" class="input" placeholder="Password" v-model="password" />
          </div>
          <button class="submit-btn" @click="signUp">Sign up</button>
        </div>
        <div class="login slide-up">
          <div class="center">
            <h2 class="form-title" id="login">
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
    <!-- END LOGIN REGISTER PAGE -->

    <!-- NAVBAR -->
    <div id="navbar">
      <header>
        <div class="logo">
          <img
            src="https://images-wixmp-fe53c9ff592a4da924211f23.wixmp.com/esh/icon_defaults/noun_366074.svg"
            style="width:40px; "
          />
          <h3>logo</h3>
        </div>
        <div id="profile">profile</div>
      </header>
    </div>
    <!-- END NAVBAR -->

    <!-- MAIN REGISTER PAGE -->
    <div id="main-page">
      <div class="home">
        <div class="ui equal width center aligned padded grid">
          <!-- HOME -->
          <div class="row">
            <div class="column">
              <div class="logo">
                <img src="./image/logolandscapewhite.png" alt />
              </div>
            </div>
            <div class="column">
              <div class="welcome">
                <h1>
                  Lorem ipsum dolor sit amet consectetur adipisicing elit. Libero architecto rerum,
                  nihil aliquam odit cupiditate nemo aut in velit modi ipsa ea blanditiis ex impedit
                  nobis quae, sint eaque sit.
                </h1>
              </div>
            </div>
          </div>
          <br />
          <br />
          <!-- END HOME -->

          <div class="row" style="background-color: #869D05;color: #FFFFFF;">
            <div class="column post"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

const axiosReq = axios.create({
  baseURL: "http://localhost:3000"
});

export default {
  data() {
    return {
      username: "",
      email: "",
      password: ""
    };
  },
  methods: {
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
          console.log(data);
        })
        .catch(err => console.log(err));
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
          console.log(data);
        })
        .catch(err => console.log(err));
    }
  }
};
</script>

<style>
</style>