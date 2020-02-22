<template>
  <div class="blog-form">
    <b-container>
      <b-row>
        <b-col md="6" cols="12" class="mx-auto my-5">
          <b-card>
            <b-card-title>Create Blog</b-card-title>
            <b-card-text>
              <b-form-file
                @change="handleUplaodImage($event)"
                placeholder="upload Blog Image"
                accept="image/jpeg, image/png, image/gif"
              ></b-form-file>
              <b-img
                class="my-2 blog-image"
                v-if="form.showBlogImage"
                :src="form.showBlogImage"
                alt="blogImage"
              ></b-img>
              <b-form-input
                class="mt-2"
                v-model="form.headline"
                placeholder="Blog Headline"
              ></b-form-input>
              <b-btn
                @click="handleCreateBlog"
                :disabled="isValid"
                variant="primary"
                class="mt-2"
                >Create Blog</b-btn
              >
            </b-card-text>
          </b-card>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>
<script>
export default {
  name: "CreateBlog",
  data() {
    return {
      form: {
        id: this.$uuid.v4(),
        headline: "",
        showBlogImage: "",
        comments: []
      },
      blogs: []
    };
  },
  methods: {
    handleUplaodImage(e) {
      const file = e.target.files[0];
      this.form.showBlogImage = URL.createObjectURL(file);
    },
    handleCreateBlog() {
      this.blogs = JSON.parse(localStorage.getItem("blogs")) || [];
      this.blogs.push(this.form);
      localStorage.setItem("blogs", JSON.stringify(this.blogs));
      this.$router.push("/");
    }
  },
  computed: {
    isValid() {
      const { headline, showBlogImage } = this.form;
      if (headline !== "" && showBlogImage !== "") {
        return false;
      } else {
        return true;
      }
    }
  }
};
</script>
<style>
.blog-image {
  height: 400px !important;
  width: 100% !important;
  box-shadow: 0 2px 10px #ccc;
}
</style>
