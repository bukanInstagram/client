<template>
  <div id="main-page">
    <div class="ui equal width center aligned padded grid">
      <div class="home">
        <div class="logo">
          <img src="../image/logolandscapewhite.png" alt />
        </div>
        <div class="welcome" style="text-align: left; display: inline;">
          <h1 style="margin-bottom: 0;">
            Please, This is not instagram!
            <br />this's Your favourite platform to "panjat sosial".
            The easiest way to share your life
            <br />Make it fun !
          </h1>
          <br />
          <div class="ui yellow buttons">
            <button class="ui button">
              <i class="plus icon"></i>
              upload
            </button>
          </div>
        </div>
      </div>


      
      <div class="popular">
        <div class="ui card" v-for="post in popularPost" :key="post.id">
          <div class="content">
            <div class="right floated meta">14h</div>
            <div class="left floated">
              <img
                class="ui avatar image"
                src="https://semantic-ui.com/images/avatar/small/jenny.jpg"
              />
              {{post.UserId.username}}
            </div>
          </div>
          <div class="img-container">
            <img class="ui centered image" :src="post.img" />
          </div>
          <div class="content">
            <h3>{{post.title}}</h3>
            <span class="right floated">
              <i class="heart outline like icon"></i>
              {{post.likes.length}} likes
            </span>
            <span class="left floated">
              <i class="comment icon"></i>
              {{post.comments.length}} comments
            </span>
          </div>
        </div>
      </div>

      <div class="post">
        <div class="ui card" v-for="post in posts" :key="post.id">
          <div class="content">
            <div class="right floated meta">14h</div>
            <div class="left floated">
              <img
                class="ui avatar image"
                src="https://semantic-ui.com/images/avatar/small/jenny.jpg"
              />
              {{post.UserId.username}}
            </div>
          </div>
          <div class="img-container">
            <img class="ui centered image" :src="post.img" />
          </div>
          <div class="content">
            <h3>{{post.title}}</h3>
            <span class="right floated">
              <i class="heart outline like icon"></i>
              {{post.likes.length}} likes
            </span>
            <span class="left floated">
              <i class="comment icon"></i>
              {{post.comments.length}} comments
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["posts"],
  computed: {
    popularPost() {
      return this.posts
        .sort((a, b) => a.likes.length - b.likes.length)
        .slice(0, 3);
    }
  }
};
</script>

<style >
</style>