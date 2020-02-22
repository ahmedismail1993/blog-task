<template>
  <section class="card-wrapper">
    <b-row>
      <b-col md="2 mx-2">
        <b-img
          class="card-wrapper__image"
          :src="blog.showBlogImage"
          style="max-width: 10rem;"
          alt="image"
        ></b-img>
      </b-col>
      <b-col md="9">
        <h3 class="card-wrapper__headeline">{{ blog.headline }}</h3>
        <ul v-if="comments.length > 0">
          <li v-for="(comment, index) in comments" :key="index">
            {{ comment }}
          </li>
        </ul>
      </b-col>
    </b-row>
  </section>
</template>

<script>
export default {
  nmae: "CardBlog",
  props: {
    blog: {
      type: Object,
      default: () => {}
    },
    comments: {
      type: Array,
      default: () => []
    }
  }
};
</script>

<style lang="scss">
.card-wrapper {
  box-shadow: 0 1px 10px #ccc;
  padding: 15px;
  border-radius: 10px;
  &__image {
    border-radius: 10px;
  }
  &__headeline {
    text-transform: capitalize;
    margin-left: 20px;
    color: #444;
    font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  }
}
ul {
  list-style: none;
}
</style>
