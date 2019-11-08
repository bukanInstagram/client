<template>
  <div id="navbar" style="background-color: #e3b04b;">
    <div class="ui secondary menu">
      <a class="active item">
        <img
          src="https://images-wixmp-fe53c9ff592a4da924211f23.wixmp.com/esh/icon_defaults/noun_366074.svg"
          style="width:40px; "
        />
      </a>
      <div class="right menu">
        <div class="item">
          <div class="ui icon input">
            <input type="text" placeholder="Search..." />
            <i class="search link icon"></i>
          </div>
        </div>
        <a class="ui item">
          <button class="ui secondary button">
            <i class="icon user"></i>
            Sign up
          </button>
        </a>
        <a class="ui item">
          <button class="ui secondary button">
            <i class="sign-in icon"></i>
            Log in
          </button>
        </a>
        <a class="ui item">
          <button class="ui secondary button">
            <i class="sign-out icon"></i>
            Logout
          </button>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style>
</style>