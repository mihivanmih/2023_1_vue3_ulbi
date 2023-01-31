<template>
  <div>
    <div>{{ post.id }}</div>
    <div><strong>Название: </strong> {{ post.title }}</div>
    <div><strong>Описание: </strong>{{ post.body }}</div>
  </div>
  <div class="post__btns">
    <my-button @click="$emit('remove', post)">удалить</my-button>
  </div>
</template>

<script>
//import MyButton from '@/components/UI/MyButton'
export default {
  // components: {
  //   MyButton
  // },
  props: {
    post: {
      type: Object,
      required: true
    }
  }
}
</script>

<style>
</style>