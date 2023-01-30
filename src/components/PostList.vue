<template>
  <div class="post" v-for="post in posts">
    <post-item :post="post"/>
  </div>
</template>

<script>
  import PostItem from '@/components/PostItem'
  export default {
    components: {PostItem},
    props: {
      posts: {
        type: Array,
        required: true
      }
    }
  }
</script>

<style>

  .post {
    padding: 15px;
    border: 1px solid darkgreen;
    margin-top: 15px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

</style>