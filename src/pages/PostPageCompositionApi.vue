<template>
  <div>
      <div class="appButtons">
<!--        <h1>{{ likes }}</h1>-->
<!--        <my-button @click="addLike">+ 1</my-button>-->

        <my-input
            type="text"
            v-model="searchQuery"
            placeholder="поиск"
            v-focus />

        <my-select
            v-model="selectedSort"
            :options="sortOptions"
        />

      </div>

      <post-list :posts="sortedAndSearchedPosts" v-if="!isPostLoading"/>

      <div v-else>Идет загрузка</div>
<!--      <div class="observer" v-intersection="loadMorePostsPost" ref="observer"> -->

</div>

</template>

<script>
import PostForm from '@/components/PostForm'
import PostList from '@/components/PostList'
import { MyDialog, MySelect, MyInput } from '@/components/UI/index'
import { usePosts } from '@/hooks/usePosts'
import useSortedPosts from '@/hooks/useSortedPost'
import useSortedAndPosts from '@/hooks/useSortedAndSearch'

export default {
  components: {
    MySelect,
    MyDialog,
    PostForm,
    PostList,
    MyInput
  },
  name: "PostPageCompositionApi",
  data() {
    return {
      dialogVisible: false,
      sortOptions: [
        { value: 'title', name: "По названию"},
        { value: 'body', name: "По содержимому"}
      ]
    }
  },
  setup(props) {
   const {posts, isPostLoading, totalPage} = usePosts(10)
   const {sortedPosts, selectedSort} = useSortedPosts(posts)
   const {searchQuery, sortedAndSearchedPosts} = useSortedAndPosts(sortedPosts)


    return {
      posts,
      totalPage,
      isPostLoading,
      sortedPosts,
      selectedSort,
      searchQuery,
      sortedAndSearchedPosts
    }

    // const likes = ref(20)
    //
    // const addLike = () => {
    //   likes.value += 1
    // }
    //
    // return {
    //   likes,
    //   addLike
    // }
  }
}
</script>

<style scoped>

</style>