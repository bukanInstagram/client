<<<<<<< HEAD

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
=======
<template>
    <div>
        <LoginRegist v-show="!isLogin"
        ></LoginRegist>
        <div v-show="isLogin">
            <Navbar></Navbar>
            <Main v-show="content==='main'" ></Main>
            <AddPostPage v-show="content==='addPost'"></AddPostPage>
            <PostPage 
             :dummyData="posts[posts.length-1]" 
             v-show="content==='postPage'"
             @refetch="fetchData"
             @likeComment="likePost"
             @deletePost="deletePost"
             >
             </PostPage>
        </div>

    </div>

</template>

<script>
import Main from './components/Main'
import LoginRegist from './Views/LoginRegist'
import Navbar from './components/Navbar'
import AddPostPage from './components/AddPostPage'
import PostPage from './components/PostPage'
import axios from 'axios'
import Swal from 'sweetalert2'
export default {
  components :{
      Navbar,
      LoginRegist,
      Main,
      AddPostPage,
      PostPage
  },
  data() {
    return {
      isLogin : true,
      content : 'main',
      posts : ''
    };
  },
  methods : {
    fetchData(){
      axios({
        method : 'get',
        url : 'http://localhost:3000/posts'
      })
      .then(({data})=>{
        this.posts = data
      })
      .catch(err=>{
        console.log(err.data.response.message)
      })
    },
    likePost(id){
      axios({
        method : 'patch',
        url : `http://localhost:3000/posts/${id}`,
        data : {},
        headers : {
          access_token : localStorage.getItem('access_token')
        }
      })
      .then(({data})=>{
          Swal.fire({
            icon: 'success',
            title: 'Liked the post'
          })
        this.fetchData()
      })
      .catch(err=>{
          Swal.fire({
            icon: 'error',
            title: err.response.data.message
          })
      })
    },
    deletePost(id){
      Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, delete it!'
      }).then((result) => {
        if (result.value) {
          axios({
            method : 'delete',
            url : `http://localhost:3000/posts/${id}`,
            data : {},
            headers : {
              access_token : localStorage.getItem('access_token')
            }
          })
          .then(({data})=>{
            Swal.fire(
              'Deleted!',
              'Your Post has been deleted.',
              'success'
            )
            this.fetchData()
          })
          .catch(err=>{
            console.log(err.response.data.message)
          })

        }
      })

    }
  },
  created(){
    this.fetchData()
>>>>>>> addcomponents
  }
};
</script>

<<<<<<< HEAD
<style scoped>
</style>
=======
<style>
</style>
>>>>>>> addcomponents
