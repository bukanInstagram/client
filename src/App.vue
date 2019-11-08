<template>
  <div>
    <LoginPage v-show="!isLogin" @logged-in="login"></LoginPage>
    <div v-show="isLogin">
      <Navbar></Navbar>
      <Main :posts="posts" v-show="content==='main'"></Main>
      <AddPostPage v-show="content==='addPost'"></AddPostPage>
      <PostPage
        v-show="content==='postPage'"
        @refetch="fetchData"
        @likeComment="likePost"
        @deletePost="deletePost"
      ></PostPage>
    </div>
  </div>
</template>

<script>
import Main from "./components/Main";
import LoginPage from "./Views/LoginPage";
import Navbar from "./components/Navbar";
import AddPostPage from "./components/AddPostPage";
import PostPage from "./components/PostPage";
import axios from "axios";
import Swal from "sweetalert2";
export default {
  components: {
    Navbar,
    LoginPage,
    Main,
    AddPostPage,
    PostPage
  },
  data() {
    return {
      isLogin: false,
      content: "main",
      posts: ""
    };
  },
  methods: {
    fetchData() {
      axios({
        method: "get",
        url: "http://localhost:3000/posts"
      })
        .then(({ data }) => {
          this.posts = data;
          console.log(this.posts);
        })
        .catch(err => {
          console.log(err.data.response.message);
        });
    },
    likePost(id) {
      axios({
        method: "patch",
        url: `http://localhost:3000/posts/${id}`,
        data: {},
        headers: {
          access_token: localStorage.getItem("access_token")
        }
      })
        .then(({ data }) => {
          Swal.fire({
            icon: "success",
            title: "Liked the post"
          });
          this.fetchData();
        })
        .catch(err => {
          Swal.fire({
            icon: "error",
            title: err.response.data.message
          });
        });
    },
    deletePost(id) {
      Swal.fire({
        title: "Are you sure?",
        text: "You won't be able to revert this!",
        icon: "warning",
        showCancelButton: true,
        confirmButtonColor: "#3085d6",
        cancelButtonColor: "#d33",
        confirmButtonText: "Yes, delete it!"
      }).then(result => {
        if (result.value) {
          axios({
            method: "delete",
            url: `http://localhost:3000/posts/${id}`,
            data: {},
            headers: {
              access_token: localStorage.getItem("access_token")
            }
          })
            .then(({ data }) => {
              Swal.fire("Deleted!", "Your Post has been deleted.", "success");
              this.fetchData();
            })
            .catch(err => {
              console.log(err.response.data.message);
            });
        }
      });
    },
    login() {
      this.isLogin = true;
    }
  },
  created() {
    this.fetchData();
  }
};
</script>

<style scoped>
</style>
