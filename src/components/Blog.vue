<template>
  <div class="body">
    <div class="container">
      <div class="blog-posts">
        <div class="blog-content" v-for="index in this.blogPosts.slice(0, this.blogLimit)" :key="index.id">
            <div class="text-center">
              <img class="blog-image img-fluid" src="https://www.fillmurray.com/250/155" alt="blog post image" />
            </div>
            <div class="blog-info">
              <h5 class="blog-category">Category</h5>
              <h6 class="blog-date"> &#x2f;&#x2f; {{date}}</h6>
            </div>
            <h3 class="blog-title">{{index.title}}</h3>
            <a href="#" class="blog-link">Read More</a>
        </div>
      </div>
      <div class="view-more">
        <p v-on:click="viewMore()">&#x2f;&#x2f; load more articles</p>
        <p v-if="this.blogLimit >= 8"  v-on:click="viewLess()">&#x2f;&#x2f; load less articles</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import moment from 'moment';

export default {
  name: 'BlogComponent',
  props: [],

  data() {
    return {
      date: this.datePosted(),
      blogPosts: [],
      limit: 4
    }
  },
  computed: {
    blogLimit() {
      return this.limit;
    }
  },

  async created() {
    let result = await this.getBlogPosts();
    this.blogPosts = result.data;
  },

  methods : {
    datePosted () {
      let date = moment().format('DD MMMM YYYY');
      return date;
    },
    async getBlogPosts () {
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts');
        return response;

      } catch (err) {
        console.error(err);
      }
    },
    viewMore() {
      this.limit = this.limit + 4;
    },
    viewLess() {
      this.limit = this.limit - 4;
    }
  }

};

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

  @import '../css/variables';

  .container {
    padding: 10px;
  }

  .blog-posts {
    display: inline-grid;
    grid-template-columns: 1fr;
  }

  .blog-content {
    margin-bottom: 30px;

    .blog-image {
      width: 100%;
      height: auto;
    }

    .blog-info {
      display: block;
      margin-top: 20px;
      margin-bottom: 15px;

        .blog-category, .blog-date {
          display: inline;
        }
        .blog-date {
          font-weight: 700;
          text-transform: uppercase;
        }
    }

    .blog-category {
      color: $color-green-fade;
      text-transform: uppercase;
    }

    .blog-title {
      text-transform: capitalize;
      margin-bottom: 25px;
    }

    .blog-link {
      border: 2px solid $primary-color;
      padding: 5px 10px;
      color: $primary-color;
      font-weight: 700;
      text-transform: lowercase;
      font-size: 14px;
        &:hover {
          text-decoration: none;
        }
    }
  }

  .view-more {
    display: block;
    margin: 20px 0;
      p {
        display: inline;
        margin-right: 10px;
      }
  }


  @media( min-width: 1025px) {
    .body {
      background-image: url('../assets/background-img.png');
      background-size: 555px;
      background-repeat: no-repeat;
      background-position: 30px 120px;
    }
    .container {
      padding: 6% 15%;
    }
    .blog-posts {
      grid-template-columns: 1fr 1fr;
      grid-template-columns: 1fr 1fr;
    }

    .blog-content {
      margin: 10px;
    }
  }



</style>
