<template>
  <div class="container">

  <div class="blog-card-wrap">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
  <div class="search-wrap">
  <form>
    <input v-model="search" type="text" placeholder="Search" class="bar">
    <button @click.prevent="update()" type="submit" class="search-button"><i class="fa fa-search"></i></button>
  </form>
  </div>
    <div class="blog-cards">
      <BlogCard :post="post" v-for="(post, index) in Posts"  :key="index" />
    </div>
  </div>
  </div>
</template>

<script>
import BlogCard from "../components/BlogCard";


export default {
  name: "posts",
  components: { BlogCard },
  data() {
      return {
        search: "",
        copy: "",
      }},
  computed: {
    Posts() {

      if( this.copy === ""){
        return this.$store.state.blogPosts
      }

      return this.$store.state.blogPosts.filter(post=> post.blogTitle.toLowerCase().includes(this.copy.toLowerCase()) || this.copy.toLowerCase().includes(post.blogTitle.toLowerCase()) );
    },
  },
  methods: {
    update() {
      this.copy = this.search
    }
  },
  };

</script>

<style lang="scss" scoped>
.blog-cards {
  position: relative;
}
html, body {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  margin-top: 16px;
  margin-bottom: 16px;
}
.search-wrap{
  box-sizing: border-box;
  display: inline;
  .bar {
    padding: 10px;
    font-size: 17px;
    border: 1.5px solid grey;
    float: left;
    width: 80%;
    background: #f1f1f1;
    align-items: center;
    display: inline;
    margin-top: 23px;
    margin-bottom: 5%;
    margin-right: 1px;
  }
  .search-button {
    float: left;
    width: 10%;
    padding: 10px;
    background: #073B4C;
    color: white;
    font-size: 17px;
    border: 1px solid #073B4C;
    border-left: none;
    cursor: pointer;
    display: inline
  }
  button:hover {
    background: #118ab2;
  }
  ::after {
    content: "";
    clear: both;
    display: table;
}
}
div#app {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  

  .wrapper {
    display: flex;
    max-width: 444px;
    flex-wrap: wrap;
    padding-top: 12px;
  }

  .card {
    box-shadow: rgba(0, 0, 0, 0.117647) 0px 1px 6px, rgba(0, 0, 0, 0.117647) 0px 1px 4px;
    max-width: 124px;
    margin: 12px;
    transition: .15s all ease-in-out;
    &:hover {
      transform: scale(1.1);
    }
    a {
      text-decoration: none;
      padding: 12px;
      color: #03A9F4;
      font-size: 24px;
      display: flex;
      flex-direction: column;
      align-items: center;
      img {
        height: 100px;
      }
      small {
        font-size: 10px;
        padding: 4px;
      }
    }
  }
}
</style>