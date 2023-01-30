<template>
    <form @submit.prevent>
<!--      <input v-bind:value="post.title" @input="post.title = $event.target.value" class="input" type="text" placeholder="Название">-->
<!--      <input v-bind:value="post.body"  @input="post.body = $event.target.value" class="input" type="text" placeholder="Описание">-->

<!--      <my-input-->
<!--          v-model:value="post.title"-->
<!--          v-model:Myvalue="post.title"-->
<!--          placeholder="Название"-->
<!--      />     -->

      <my-input
          v-model="post.title"
          placeholder="Название"
      />
      <my-input v-model="post.body" placeholder="Описание" />
      <my-button @click="createPost">Создать</my-button>
    </form>
</template>

<script>
//import MyButton from '@/components/UI/MyButton'
export default {
  // components: {
  //   MyButton
  // },
  data() {
    return {
      post: {
        title: '',
        body: ''
      }
    }
  },
  methods: {
    createPost() {
      this.post.id = Date.now()
      this.$emit('create', this.post)
      this.post = {
        title: '',
        body: ''
      }

    }
  }
}
</script>

<style>

form {
  display: flex;
  flex-direction: column;
}

</style>