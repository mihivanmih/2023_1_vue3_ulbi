<template>
  <div>
<!--    <h1>{{ $store.state.post.limit }}</h1>-->
<!--    {{ $store.commit }}-->
<!--    <h1>{{ $store.getters.doubleLikes }}</h1>-->
<!--    PostPageWithStore-->

<!--    <my-button @click="$store.commit('incrementLikes')">+1</my-button>-->
<!--    <my-button @click="$store.commit('decrementLikes')">-1</my-button>-->

<!--    <h1>{{ $store.state.isAuth ? "Авторизован" : "Не авторизован" }}</h1>-->

      <div class="appButtons">

        <my-input
            type="text"
            :model-value="searchQuery"
            @update:model-value="setSearchQuery"
            placeholder="поиск"
            v-focus />
        <my-button @click="showDialog">
          Добавить пост
        </my-button>

        <my-select
            :model-value="selectedSort"
            @update:model-value="setSelectedSort"
            :options="sortOptions"
        />

      </div>

      <my-dialog v-model:show="dialogVisible">
        <post-form @create="createPost"/>
      </my-dialog>

      <post-list :posts="sortedAndSearchedPosts" @remove="removePost" v-if="!isPostLoading"/>

      <div v-else>Идет загрузка</div>
      <div class="observer" v-intersection="loadMorePostsPost" ref="observer"></div>


  </div>
</template>

<script>
import { mapState, mapGetters, mapActions, mapMutations} from 'vuex'
import PostForm from '@/components/PostForm'
import PostList from '@/components/PostList'
import { MyDialog, MySelect, MyInput } from '@/components/UI/index'

export default {
  components: {
    MySelect,
    MyDialog,
    PostForm,
    PostList,
    MyInput
  },
  name: "PostPageWithStore",
  methods: {
    ...mapMutations({
      setPage: 'post/setPage',
      setSearchQuery: 'post/setSearchQuery',
      setSelectedSort: 'post/setSelectedSort'
    }),
    ...mapActions({
      loadMorePostsPost: 'post/loadMorePosts',
      fetchPosts: 'post/fetchPosts',
    })
  },
  computed: {
    ...mapState({
      posts: state => state.post.posts,
      isPostLoading: state => state.post.isPostLoading,
      selectedSort: state => state.post.selectedSort,
      searchQuery: state => state.post.searchQuery,
      page: state => state.post.page,
      limit: state => state.post.limit,
      totalPage: state => state.post.totalPage,
      sortOptions: state => state.post.sortOptions
    }),
    ...mapGetters({
      sortedPost: 'post/sortedPost',
      sortedAndSearchedPosts: 'post/sortedAndSearchedPosts',
    })
  },
  mounted() {
    this.fetchPosts()
  }
}
</script>

<style scoped>

</style>