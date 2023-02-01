<template>
  <div>
    <div class="appButtons">

      <my-input type="text" v-model="searchQuery" placeholder="поиск" v-focus />
      <my-button @click="showDialog">
        Добавить пост
      </my-button>

      <my-select
          v-model="selectedSort"
          :options="sortOptions"
      />

    </div>

    <!--    <input type="text" v-model.trim.number="modificatorValue">-->
    <my-dialog v-model:show="dialogVisible">
      <post-form @create="createPost"/>
    </my-dialog>
    <post-list :posts="sortedAndSearchedPosts" @remove="removePost" v-if="!isPostLoading"/>
    <div v-else>Идет загрузка</div>
    <div class="observer" v-intersection="loadMorePosts" ref="observer"></div>

    <!--    <div class="page__wrapper">-->
    <!--      <div-->
    <!--          v-for="pageNumber in totalPage"-->
    <!--          class="page"-->
    <!--          :class="{'current-page': page === pageNumber}"-->
    <!--          @click="changePage(pageNumber)"-->
    <!--      >{{ pageNumber }}</div>-->
    <!--    </div>-->

  </div>
</template>

<script>
import PostForm from '@/components/PostForm'
import PostList from '@/components/PostList'
import { MyDialog, MySelect, MyInput } from '@/components/UI/index'
import axios from 'axios'

export default {
  components: {
    MySelect,
    MyDialog,
    PostForm,
    PostList,
    MyInput
  },
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostLoading: false,
      selectedSort: '',
      searchQuery: '',
      page: 1,
      limit: 10,
      totalPage: 0,
      sortOptions: [
        { value: 'title', name: "По названию"},
        { value: 'body', name: "По содержимому"}
      ]
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post)
      this.dialogVisible = false
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    showDialog() {
      this.dialogVisible = true
    },
    // changePage(pageNumber) {
    //   this.page = pageNumber
    // },
    async fetchPosts() {
      try {
        this.isPostLoading = true
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
          params: {
            _page: this.page,
            _limit: this.limit
          }
        })
        this.totalPage = Math.ceil(response.headers['x-total-count'] / this.limit)
        this.posts = response.data
      } catch (e) {
        console.log("error", e)
      } finally {
        this.isPostLoading = false
      }
    },
    async loadMorePosts() {
      try {
        this.page++
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
          params: {
            _page: this.page,
            _limit: this.limit
          }
        })
        this.totalPage = Math.ceil(response.headers['x-total-count'] / this.limit)
        this.posts = [...this.posts, ...response.data]
      } catch (e) {
        console.log("error", e)
      }
    }
  },
  mounted() {
    this.fetchPosts()
    // const options = {
    //   rootMargin: '0px',
    //   threshold: 1.0
    // }
    // const callback = (entries, observer) => {
    //   if(entries[0].isIntersecting) {
    //     this.loadMorePosts()
    //   }
    // }
    // const observer = new IntersectionObserver(callback, options)
    // observer.observe(this.$refs.observer)
  },
  computed: {
    sortedPost() {
      return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
      )
    },
    sortedAndSearchedPosts() {
      return this.sortedPost.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
    }
  },
  watch: {
    // selectedSort(newValue) {
    //   this.posts.sort((post1, post2) => {
    //     return post1[newValue]?.localeCompare(post2[newValue])
    //   })
    // },
    dialogVisible(newValue) {
      console.log(newValue)
    },
    // page() {
    //   this.fetchPosts()
    // }
  }
}
</script>

<style>
.page__wrapper {
  display: flex;
  margin-top: 15px;
}

.page {
  border: 1px solid #000;
  padding: 10px;
}

.current-page {
  border: 2px solid rgb(16, 71, 26);
}

.observer {
  height: 30px;
  background: teal;
}

</style>