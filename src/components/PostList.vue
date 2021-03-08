<template>
  <div class="post-list">
      <div v-for="post in posts" :key="post.id">
          <SinglePost :post="post" />
      </div>

  </div>
</template>

<script>
import { onMounted, onUnmounted, onUpdated } from 'vue'
import SinglePost from './SinglePost'
export default {
    props: ['posts'],
    components: { SinglePost },
    setup(props) { // Using props in the setup object
        //console.log(props.posts)
        onMounted(() => console.log('Component Mounted'))
        onUnmounted(() => console.log('Component Unmounted'))
        onUpdated(() => console.log('Component Updated'))
    }

}
</script>

<style>

</style>