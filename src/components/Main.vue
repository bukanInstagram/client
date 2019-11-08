<template>
  <div id="main-page">
    <div class="home">
      <div class="ui equal width center aligned padded grid">
        <div class="row">
          <!-- TOP THREE POPULAR -->
          <div class="column">
            <div class="popular">
              <div class="ui card">
                <div class="content">
                  <div class="right floated meta">14h</div>
                  <img
                    class="ui avatar image"
                    src="https://semantic-ui.com/images/avatar/small/jenny.jpg"
                  /> Elliot
                </div>
                <div class="image">
                  <img src="../image/logo2.png" />
                </div>
                <div class="content">
                  <span class="right floated">
                    <i class="heart outline like icon"></i>
                    17 likes
                  </span>
                  <i class="comment icon"></i>
                  3 comments
                </div>
                <div class="extra content">
                  <div class="ui large transparent left icon input">
                    <i class="heart outline icon"></i>
                    <input type="text" placeholder="Add Comment..." />
                  </div>
                </div>
              </div>
            </div>
          </div>
          <!-- ENDTOP THREE POPULAR -->

          <!-- POST -->
          <div id="post">
            <section class="gridphoto">
              <div class="photo">
                <div v-for="post in posts" :key="post.id">
                  <!-- <div class="ui card" style="width: 300px; height: 300px; overflow: hidden;"> -->
                  <div class="ui card">
                    <div class="content">
                      <div class="right floated meta" style>14h</div>
                      <img
                        class="ui avatar image"
                        src="https://semantic-ui.com/images/avatar/small/jenny.jpg"
                      /> Elliot
                    </div>
                    <div class="image">
                      <img :src="post.img" />
                    </div>
                    <div class="content">
                      <span class="right floated">
                        <i class="heart outline like icon"></i>
                        {{post.likes.length}} likes
                      </span>
                      <i class="comment icon"></i>
                      {{post.comments.length}} comments
                    </div>
                    <div class="extra content">
                      <div class="ui large transparent left icon input">
                        <i class="heart outline icon"></i>
                        <input type="text" placeholder="Add Comment..." />
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </section>
          </div>
          <!-- END POST -->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["posts"]
};
</script>

<style >
</style>