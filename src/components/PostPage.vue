<template>
  <div>
    <div id="comment-page">
      <!-- image -->
      <div class="containPostComment">
        <div class="ui yellow card" style="width: 600px;">
          <div class="content">
            <a class="header" href="#">{{selectedPosts.UserId.username}}</a>
            <div class="meta">
              <!-- <a>Last Seen 2 days ago</a> -->
            </div>
            <div
              @click="like(selectedPosts._id)"
              class="d-flex justify-content-end"
              style="cursor:pointer"
            >
              <div>
                <i class="thumbs up icon"></i>
                <!-- <span class="badge badge-dark">{{selectedPosts.likes.length}}</span> -->
              </div>
            </div>
          </div>
          <a class="image" href="#">
            <img :src="selectedPosts.img" />
          </a>
        </div>
      </div>
      <!-- end image -->
      <!-- =================== -->
      <div class="commentz">
        <div class="two column centered row">
          <div class="column">
            <div class="ui small comments">
              <h3 class="ui dividing header">Comments</h3>
              <div v-if="selectedPosts.comments.length === 0" class="comment">
                <div class="content">
                  <div class="metadata"></div>
                  <div class="text">
                    <strong>NO COMMENT</strong>
                  </div>
                  <div class="actions">
                    <a class="reply">Reply</a>
                  </div>
                </div>
              </div>
              <div class="comment">
                <div v-if="selectedPosts.comments.length > 0">
                  <div v-for="reply in selectedPosts.comments" :key="reply._id">
                    <a class="avatar">
                      <img src="https://semantic-ui.com/images/avatar/small/elliot.jpg" />
                    </a>
                    <div class="content">
                      <a class="author ml-1">{{username}}</a>
                      <div class="metadata">
                        <span class="date">Yesterday at 12:30AM</span>
                      </div>
                      <div class="text">
                        <p class="ml-1" v-html="reply.content"></p>
                      </div>
                      <div class="actions">
                        <a class="reply">Reply</a>
                      </div>
                    </div>
                  </div>
                </div>
                <form class="ui reply form">
                  <div class="form-group">
                    <quill-editor class="bg-white" v-model="content" ref="myQuillEditor"></quill-editor>
                  </div>
                  <div
                    @click="comment(selectedPosts._id)"
                    class="ui blue labeled submit icon button"
                  >
                    <i class="icon edit"></i> Add Reply
                  </div>
                </form>
              </div>
            </div>
          </div>
          <!-- ==================== -->
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import "quill/dist/quill.core.css";
import "quill/dist/quill.snow.css";
import "quill/dist/quill.bubble.css";
import { quillEditor } from "vue-quill-editor";
import axios from "axios";
import Swal from "sweetalert2";
export default {
  props: ["selectedPosts", "posts"],
  components: {
    quillEditor
  },
  data() {
    return {
      content: "",
      username: localStorage.getItem("user"),
      time: ""
    };
  },
  methods: {
    comment(id) {
      console.log("COMMENT");
      axios({
        method: "post",
        url: `http://34.87.109.94/comments/${id}`,
        data: {
          content: this.content
        },
        headers: {
          access_token: localStorage.getItem("access_token")
        }
      })
        .then(({ data }) => {
          this.time = new Date().toDateString();
          this.username = localStorage.getItem("user");
          Swal.fire({
            icon: "success",
            title: "Post Comment"
          });
          this.selectedPosts.comments.push({ content: this.content });
          this.$emit("refetch");
          this.content = "";
        })
        .catch(err => {
          Swal.fire({
            icon: "error",
            title: err.response.data.message.join("\n")
          });
        });
    },
    like(id) {
      console.log("MASUKK");
      this.$emit("likeComment", id);
    },
    deletePost(id) {
      this.$emit("deletePost", id);
    }
  }
};
</script>



<style>
</style>