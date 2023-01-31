<template>

  <transition-group name="post-list">
    <div class="post" v-for="post in posts" :key="post.id" v-if="posts.length > 0">
      <post-item
          :post="post"
          :key="post.id"
          @remove="$emit('remove', post)"
      />
    </div>
    <div v-else>
      Список постов пуст
    </div>
  </transition-group>
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

.post-list {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.2s ease;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
.post-list-move {
  transition: transform 0.5s ease;
}


</style>