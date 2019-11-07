
<template>
  <div>
    <LoginPage v-if="!isLogin" @logged-in="logging"></LoginPage>
    <div v-else>
      <!-- <NavBar></NavBar> -->
      <span>LOGIN SUCCESS!</span>
      <!-- <MainPage v-if="isLogin"></MainPage> -->
    </div>
  </div>
</template>

<script>
import LoginPage from "./views/LoginPage";
// import NavBar from "./components/NavBar";
// import MainPage from "./views/MainPage";

export default {
  components: {
    LoginPage
    // NavBar
    // MainPage
  },
  data() {
    return {
      isLogin: false
    };
  },
  methods: {
    logging() {
      this.isLogin = true;
    }
  }
};
</script>

<style scoped>
</style>
