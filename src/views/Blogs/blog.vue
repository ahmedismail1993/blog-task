<template>
  <main class="blog">
    <b-container>
      <b-row>
        <b-col cols="12" class="mt-4">
          <CardBlog :blog="blog" :comments="comments" />
          <b-textarea
            no-resize
            class="mt-3"
            rows="10"
            placeholder="comments"
            v-model="form.comments"
          ></b-textarea>
          <b-btn
            @click="handleAddComment(blog)"
            :disabled="form.comments === ''"
            class="mt-2"
            variant="primary"
            >Add Comment</b-btn
          >
        </b-col>
      </b-row>
    </b-container>
  </main>
</template>

<script>
export default {
  name: "Blog",
  components: {
    CardBlog: () => import("./CardBlog")
  },
  data() {
    return {
      form: {
        comments: ""
      },

      comments: []
    };
  },
  methods: {
    handleAddComment() {
      this.comments.push(this.form.comments);
      this.form.comments = "";
    }
  },
  computed: {
    blog() {
      const blogs = JSON.parse(localStorage.getItem("blogs"));
      return blogs.filter(el => el.id === this.$route.params.id)[0];
    }
  }
};
</script>
