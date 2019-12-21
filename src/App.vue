<template>
  <div id="app" class="body-container">
    <BlogComponent/>
  </div>
</template>

<script>
import BlogComponent from './components/Blog.vue';

export default {
  name: 'app',
  components: {
    BlogComponent,
  }
}

</script>

<style lang="scss">
 @media( min-width: 1024px) {
  .body-container {
    max-width: 1040px;
    margin: 25px auto;
  }
 }
</style>
