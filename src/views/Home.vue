<template>
  <div class="home">
    <div class="recommend">
    <Recommend />
    </div>
    <Post v-if="!user" :post="welcomeScreen" />
    <Post :post="post" v-for="(post, index) in blogPostsFeed" :key="index" /> 
    <div class="blog-card-wrap">
      <div class="container">
        <h3>View More Recent posts</h3>
        <div class="blog-cards">
          <BlogCard :post="post" v-for="(post, index) in blogPostsCards" :key="index" />
        </div>
      </div>
    </div>
    <div v-if="!user" class="updates">
      <div class="container">
        <h2>Never miss a game. Register for your free account today!</h2>
        <router-link class="router-button" :to="{ name: 'Register' }">Register for GameHub<Arrow class="arrow arrow-light" /> </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import Post from "../components/Post";
import BlogCard from "../components/BlogCard";
import Arrow from "../assets/Icons/arrow-right-light.svg";
import Recommend from "../components/Recommend";
export default {
  name: "Home",
  components: { Post, BlogCard, Arrow, Recommend },
  data() {
    return {
      welcomeScreen: {
        title: "Welcome!",
        blogPost:
          "Register today to share your love for your favourtie games!",
        welcomeScreen: true,
        photo: "welcome2",
      },
    };
  },
  computed: {
    blogPostsFeed() {
      return this.$store.getters.blogPostsFeed;
    },
    blogPostsCards() {
      return this.$store.getters.blogPostsCards;
    },
    user() {
      return this.$store.state.user;
    },
  },
};
</script>

<style lang="scss" scoped>
.blog-card-wrap {
  h3 {
    font-weight: 300;
    font-size: 28px;
    margin-bottom: 32px;
  }
}

.recommend{
  padding-right: 8%;
  padding-left: 8%;
  padding-bottom: 3%;
  background-color: #EAF4F4;
}
.updates {
  .container {
    padding: 100px 25px;
    display: flex;
    flex-direction: column;
    align-items: center;
    @media (min-width: 800px) {
      padding: 125px 25px;
      flex-direction: row;
    }

    .router-button {
      display: flex;
      font-size: 20px;
      text-decoration: none;
      @media (min-width: 800px) {
        margin-left: auto;
      }
      background-color: #073B4C;
    }

    h2 {
      font-weight: 300;
      font-size: 32px;
      max-width: 425px;
      width: 100%;
      text-align: center;
      text-transform: uppercase;
      @media (min-width: 800px) {
        text-align: initial;
        font-size: 40px;
      }
    }
  }
}
</style>