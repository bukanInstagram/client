
<template>
  <div>
    <Main></Main>
  </div>
</template>

<script>
import Main from "./components/Main";
export default {
  components: {
    Main
  },
  data() {
    return {
      username: "",
      email: "",
      password: ""
    };
  }
};
</script>

<style scoped>
</style>
