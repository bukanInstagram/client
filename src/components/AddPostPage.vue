<template>
  <div>
   <div class="addpost">
        <br>
        <br>
        <div>
            <h1> Let's Influence the World!</h1>
        </div>
        <br>
        <div class="containAdd">
            <div class="addphoto">
                <img :src="imageLink" alt="" width="400">
            </div>
            <div class="formadd">
                <div class="ui small form">
                    <div class="fields">
                        <div class="field">
                            <label for="postTitle"><strong>Title</strong></label>
                            <input v-model="title" type="text" class="form-control" id="postTitle"
                                placeholder="post a title">
                        </div>
                        <div class="field">
                            <label for="postDescription"><strong>Description</strong></label>
                            <input v-model="description" type="text" class="form-control" id="postDescription"
                                placeholder="description">
                        </div>
                    </div>
                    <div class=" sixteen wide field">
                        <label for="articleTag"><strong>Tag</strong></label>
                        <select v-model="tag" class="ui search dropdown" id="articleTag">
                            <option value="" selected disabled hidden>choose tag here</option>
                            <option>sport</option>
                            <option>daily</option>
                            <option>politic</option>
                            <option>health</option>
                            <option>travel</option>
                            <option>automotive</option>
                            <option>electronic</option>
                            <option>hobbies</option>
                            <option>food</option>
                        </select>
                        </label>
                    </div>
                    <div class=" sixteen wide field">
                        <label for="addImage"><strong>Add Image</strong></label>
                        <input @change="previewFile" type="file" class="form-control-file ui secondary button"
                            id="addImage">
                        <br>
                        <br>
                        <button @click.prevent="uploadImage" class="ui small button">Upload Image</button>
                    </div>

                    <button class="ui secondary button" type="submit">Submit</button>
                </div>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Swal from "sweetalert2";
export default {
  data() {
    return {
      title: "",
      tag: "",
      description: "",
      formUploadImg: {
        img: ""
      },
      imageLink:
        "https://i2.wp.com/www.scribblesandcrumbs.com/wp-content/plugins/penci-portfolio//images/no-thumbnail.jpg?w=1170"
    };
  },
  methods: {
    previewFile(event) {
      this.formUploadImg.img = event.target.files[0];
    },
    submitPost() {
      axios({
        method: "post",
        url: "http://localhost:3000/posts",
        data: {
          title: this.title,
          tags: this.tag,
          description: this.description,
          img: this.imageLink
        },
        headers: {
          access_token: localStorage.getItem("access_token")
        }
      })
        .then(({ data }) => {
          Swal.fire({
            icon: "success",
            title: "Post Created"
          });
          this.title = "";
          this.tag = "";
          this.description = "";
          this.$emit("reFetch");
        })
        .catch(err => {
          Swal.fire({
            icon: "error",
            title: err.response.data.message.join("\n")
          });
        });
    },
    uploadImage() {
      let { img } = this.formUploadImg;
      let bodyFormData = new FormData();
      if (this.formUploadImg.img !== "") {
        Swal.fire({
          title: "wait a minute to upload data",
          allowOutsideClick: () => !Swal.isLoading()
        });
        Swal.showLoading("wait a minute ");
      } else {
        Swal.fire({
          icon: "error",
          title: "No Image Selected"
        });
      }
      bodyFormData.append("image", img);
      axios({
        method: "post",
        url: "http://localhost:3000/upload",
        data: bodyFormData
      })
        .then(({ data }) => {
          this.imageLink = data.link;
          Swal.close();
          Swal.fire({
            icon: "success",
            title: "Image Uploaded"
          });
        })
        .catch(err => {
          console.log(err.response.data.message);
        });
    }
  }
};
</script>

<style>
</style>