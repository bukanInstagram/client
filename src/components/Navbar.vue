<template>
  <div>
    <div id="navbar" style="background-color: #e3b04b; position:fixed; z-index: 1; width: 100%;">
      <div class="ui secondary menu">
        <a class="active item" @click="backHome">
          <img
            src="https://images-wixmp-fe53c9ff592a4da924211f23.wixmp.com/esh/icon_defaults/noun_366074.svg"
            style="width:40px; "
          />
        </a>
        <div class="right menu">
          <a class="ui item">
            <button class="ui secondary button" v-if="!isLogin" @click="showSignupForm">
              <i class="icon user"></i>
              Sign up
            </button>
          </a>
          <a class="ui item">
            <button class="ui secondary button" v-if="!isLogin" @click="showLoginForm">
              <i class="sign-in icon"></i>
              Log in
            </button>
          </a>
          <a class="ui item">
            <button class="ui secondary button" v-if="isLogin" @click="logout">
              <i class="sign-out icon"></i>
              Logout
            </button>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["isLogin"],
  methods: {
    logout() {
      this.$emit("logout");
    },
    backHome() {
      console.log("cehhh");
      this.$emit("back-home");
    }
  }
};
</script>

<style>
</style>