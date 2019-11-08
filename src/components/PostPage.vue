<template>
    <div class="col p-3" style="height: 30vh; background-color: rgb(226, 226, 226);" >
      
        {{dummyData}}

        <div>
                  <button @click="like(dummyData._id)" class="btn btn-primary">click to like</button>
                  <button @click="deletePost(dummyData._id)" class="btn btn-danger">click to delete</button>
        </div>


        <form @submit.prevent="comment">
          <div class="form-group">
              <quill-editor class="bg-white" v-model="content"
                ref="myQuillEditor"
                >
              </quill-editor>
          </div>
          <button class="btn btn-primary" type="submit">Comment</button>
        </form>

    </div>
</template>


<script>
import 'quill/dist/quill.core.css'
import 'quill/dist/quill.snow.css'
import 'quill/dist/quill.bubble.css'
import { quillEditor } from 'vue-quill-editor'
import axios from'axios'
import Swal from 'sweetalert2'
  export default {
    props : ['dummyData'],
    components: {
        quillEditor
  },
    data() {
      return {
        content: '',
      }
    },
    methods :{
      comment(){
        axios({
          method : 'post',
          url : `http://localhost:3000/comments/${this.dummyData._id}`,
          data : {
            content : this.content
          },
          headers:{
            access_token : localStorage.getItem('access_token')
          }
        })
        .then(({data})=>{
          this.content = ''
          this.$emit('refetch')
        })
        .catch(err=>{
          Swal.fire({
            icon: 'error',
            title: err.response.data.message
          })
        })
      },
      like(id){
        this.$emit('likeComment', id)
      },
      deletePost(id){
        this.$emit('deletePost', id)
      }
    }
  }
</script>



<style>

</style>