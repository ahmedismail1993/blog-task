<template>
  <main class="blogs mt-2">
    <b-container>
      <b-row>
        <b-col cols="12" class="my-3" v-if="blogs.length > 0">
          <b-nav-form>
            <b-form-input
              size="sm"
              class="mr-sm-2"
              placeholder="Search"
              v-model.trim="searchFilter"
            ></b-form-input>
          </b-nav-form>
        </b-col>
        <h2 v-if="blogs.length === 0">No Blogs please create</h2>

        <b-col
          class="mb-2"
          cols="12"
          v-for="(blog, index) in filterdBLogs"
          :key="index"
        >
          <router-link :to="{ name: 'blog', params: { id: blog.id } }">
            <CardBlog :blog="blog" />
          </router-link>
          <b-btn
            class="mt-1"
            variant="danger"
            @click="handleDeleteBlog(blog, index)"
            >delete</b-btn
          >
        </b-col>
      </b-row>
    </b-container>
  </main>
</template>

<script>
export default {
  name: "Blogs",
  components: {
    CardBlog: () => import("./CardBlog")
  },
  data() {
    return {
      blogs: JSON.parse(localStorage.getItem("blogs")) || [],
      searchFilter: ""
    };
  },
  computed: {
    filterdBLogs() {
      if (this.searchFilter !== "") {
        return this.blogs.filter(
          el => el.headline === this.searchFilter.toLowerCase()
        );
      } else {
        return this.blogs;
      }
    }
  },
  methods: {
    handleDeleteBlog(blog, index) {
      const blogs = this.blogs.filter(el => el.id !== blog.id);
      localStorage.clear("blogs");
      localStorage.setItem("blogs", JSON.stringify(blogs));
      this.$delete(this.blogs, index);
    }
  }
};
</script>

<style lang="scss">
article {
  img {
    height: 200px !important;
  }
}

a {
  text-decoration: none !important;
}
</style>
