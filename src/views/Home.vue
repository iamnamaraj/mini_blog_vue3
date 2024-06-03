<template>
  <div class="home">
    <div v-if="error"> {{ error }} </div>
    <div v-if="posts.length">
      <PostList :posts="posts"/>
    </div>
    <div v-else> Loading data ...</div>
  </div>
</template>

<script>
import { ref } from 'vue'
import PostList from '../components/PostList.vue'
import getPosts from '../composables/getPosts'

export default {
  name: 'Home',
  components: { PostList},
  setup(){
    const {posts, error, load} = getPosts();
    load()
    return { posts, error }
  }
}
</script>
