<template>
    <div v-if="error"> {{ error }}</div>
    <div v-if="post" class="post">
        <h3>{{ post.title }}</h3>
        <p class="pre">{{ post.body }}</p>
    </div>
    <div v-else>
        <Spinner />
    </div>
</template>

<script>
import getPost from '../composables/getPost'
import Spinner from '../components/Spinner.vue'
import { useRoute } from 'vue-router'

export default {
    props: ['id'],
    components: { Spinner },

    setup(props){

        const route = useRoute()

        const { post,error,load } = getPost(route.params.id)

        // const { post,error,load } = getPost(props.id)

        load()

        return { post,error }
    }

}
</script>

<style>
    .post{
        max-width: 1200px;
        margin: 0 auto;
    }
    .post p{
        color: #444;
        line-height: 1.5rem;
        margin-top: 40px;
    }
</style>