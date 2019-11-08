<template>
  <div>
    <div class="column">

        <div class="logo">
            <img :src="imageLink" alt="" width="400">
        </div>
    </div>
        <!-- <div class="column"> -->
    <div class="welcome">
        <div class="p-3 rounded w-75" style="background-color: rgb(226, 226, 226);" >
            <form @submit.prevent="submitPost">
                <div class="form-group">
                  <label for="postTitle"><strong>Title</strong></label>
                  <input v-model="title" type="text" class="form-control" id="postTitle" placeholder="post a title">
                  <label for="postDescription"><strong>Description</strong></label>
                  <input v-model="description" type="text" class="form-control" id="postDescription" placeholder="description">
                </div>
                <div class="form-group">
                  <label for="articleTag"><strong>Tag</strong></label>
                  <select v-model="tag" class="form-control" id="articleTag">
                    <option value="" selected disabled hidden>Choose Tag Here</option>
                    <option>Sports</option>
                    <option>Daily-Lifes</option>
                    <option>Politics</option>
                    <option>Healths</option>
                    <option>Travels</option>
                    <option>Automotives</option>
                    <option>Electronics</option>
                    <option>Hobbies</option>
                    <option>Foods</option>
                  </select>
                </div>
                <div class="form-group">
                  <label for="addImage"><strong>Add Image</strong></label>
                  <input @change="previewFile" type="file" class="form-control-file" id="addImage">
                  <button @click.prevent="uploadImage" class="btn btn-info my-2">Upload Image</button>
                </div>

                <button class="btn btn-primary" type="submit">Post</button>
            </form>
        </div>
    </div>
        <!-- </div> -->
    
  </div>
</template>

<script>
import axios from'axios'
import Swal from 'sweetalert2'
export default {
    data() {
      return {
        title : '',
        tag : '',
        description: '',
        formUploadImg: {
        img: ''
        },
        imageLink : 'https://i2.wp.com/www.scribblesandcrumbs.com/wp-content/plugins/penci-portfolio//images/no-thumbnail.jpg?w=1170'
      }
    },
    methods :{
      previewFile (event) {
        this.formUploadImg.img = event.target.files[0]
      },
      submitPost(){
        axios({
            method : 'post',
            url :'http://localhost:3000/posts',
            data : {
                title : this.title,
                tags : this.tag,
                description : this.description,
                img : this.imageLink
            },
            headers : {
                access_token : localStorage.getItem('access_token')
            }
        })
        .then(({data})=>{
          Swal.fire({
            icon: 'success',
            title: 'Post Created'
          })
          this.title = ''
          this.tag = ''
          this.description = ''
          this.$emit('reFetch')
        })
        .catch(err=>{
          Swal.fire({
            icon: 'error',
            title: err.response.data.message.join('\n')
          })
        })
      },
      uploadImage(){
        let { img } = this.formUploadImg
        let bodyFormData = new FormData()
        if(this.formUploadImg.img !== ''){
          Swal.fire({
            title: 'wait a minute to upload data',
            allowOutsideClick: () => !Swal.isLoading()
          })
          Swal.showLoading('wait a minute ')
        }else{
          Swal.fire({
            icon: 'error',
            title: 'No Image Selected'
          })
        }
        bodyFormData.append('image', img)
        axios({
            method : 'post',
            url :'http://localhost:3000/upload',
            data :bodyFormData
        })
        .then(({data})=>{
          this.imageLink = data.link
          Swal.close()
          Swal.fire({
            icon: 'success',
            title: 'Image Uploaded'
          })
        })
        .catch(err=>{
          console.log(err.response.data.message)
        })
      }
    }
  }

</script>

<style>

</style>