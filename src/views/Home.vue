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

export default {
  name: 'Home',
  components: {
  PostList
  },
  setup(){
    const posts = ref([])
    const error = ref(null)
    const post = ref(null)

    const load = async()=>{
      try {
        let data = await fetch('http://localhost:3000/posts')
        if(!data.ok){
          throw Error('No data available')
        }
        posts.value = await data.json()
      } catch (err) {
        error.value = err.message
      }
    }
    load()
    return { posts, error }
  }
}
</script>
