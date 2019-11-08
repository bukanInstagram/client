<template>
  <div id="main-page">
    <div class="ui equal width center aligned padded grid">
      <div class="home">
        <div class="logo" style="display: flex; flex-direction: column">
          <img src="../images/logolandscapewhite.png" alt />
          <div class="sharethis-inline-share-buttons"></div>
        </div>
        <div class="welcome">
          <div style="text-align: left; display: inline;">
            <h1 style="margin-bottom: 0;">
              Please, This is not instagram !
              <br />this's Your daily platform to "panjat sosial".
              The easiest way to share your life
              <br />Make it fun !
            </h1>
            <br />
            <div class="ui yellow buttons">
              <button class="ui button" @click="addPost">
                <i class="plus icon"></i>
                upload
              </button>
            </div>
          </div>
        </div>
      </div>

      <br />
      <br />
      <div class="row">
        <div class="column">
          <h1>Popular Posts</h1>
          <div class="popular">
            <div
              class="ui card"
              v-for="post in popularPost"
              :key="post.id"
              @click="postData(post)"
              style="cursor:pointer"
            >
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

        <div id="post">
          <section class="gridphoto">
            <div class="ui card" v-for="post in posts" :key="post.id" @click="postData(post)">
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
          </section>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

const axiosReq = axios.create({
  baseURL: "http://34.87.109.94"
});

export default {
  props: ["posts"],
  methods: {
    addPost() {
      if (localStorage.getItem("access_token")) {
        this.$emit("check-status", "ok");
      } else {
        this.$emit("check-status", "no");
      }
    },
    postData(data) {
      console.log(data);
      this.$emit("selectedPost", data);
    }
  },
  computed: {
    popularPost() {
      if (this.posts)
        return this.posts
          .sort((a, b) => a.likes.length - b.likes.length)
          .slice(0, 3);
    }
  }
};
</script>

<style >
</style>