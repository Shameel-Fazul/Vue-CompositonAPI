<template>
  <div class="home">
    home
    <p>My name is {{ name }} and my age is {{ age }}</p> <!-- Vue automatically uses 'name.value' as the element value. In the template, we don't use the value property -->
    <button @click="handleClick">Click me</button>
    <button @click="age++">Increment age</button>
    <input type="text" v-model="name"> <!-- 2 Way Data Binding -->
    
    <br><br><br>
    <input type="text" v-model="search">
    <p>Search term - {{ search }}</p>
    <div v-for="jedi in matchingJedis" :key="jedi">{{ jedi }}</div>
    
    <br><br><br>
    <!-- PART 2 -->
    <div v-if="error">{{ error }}</div>
    <div v-if="posts.length">
      <PostList v-if="showPosts" :posts="posts"/>
    </div>
    <div v-else>Loading...</div>
    <br>
    <button @click="showPosts = !showPosts">toggle Posts</button>
    <button @click="posts.pop()">delete post</button> <!-- pop() remove an element from the posts array-->
  </div>
</template>

<script>
import PostList from '../components/PostList.vue'
import { computed, reactive, ref, watch, watchEffect } from 'vue'
import getPosts from '../composables/getPosts'

export default {
  name: 'Home',
  components: { PostList },
  setup() { // Vue using the Composition API

    // Creating reactive variables like the data() method in the options API
    // This is done using the template refs to make variables reactive
    const name = ref('Shameel')
    const age = ref(20)
    //const fullName = reactive('Shameel-Fazul') // reactive is similar to refs but you can't use primitive values. only objects/arrays reactive({ }) reactive([ ])

    //const p = ref(null) //Template reference - "null" is for the initial value for the <p> element before returning and getting the DOM value
    const search = ref('')
    const jedis = ref(['Anakin', 'Padme', 'Ahsoka', 'Obi Wan', 'Yoda', 'Mace Windu', 'Udamari'])
 
    // Computed Properties - Filtering data based on other data
    const matchingJedis = computed(() => {
      return jedis.value.filter((jedi) => jedi.includes(search.value))
    })

    const stopWatch = watch(search, () => { // Like the useEffect hook in React, runs everytime the search variable changes
      console.log('watch ran')
    })

    const stopWatchEffect = watchEffect(() => { // runs on initial load, and then watches and returns updated values
      console.log('watch effect ran', search.value)
    })


   const handleClick = () => {
     name.value = 'codename_shameel' // Updating data using the Composition API
     age.value = 19

     stopWatch() // Invoke to stop watching
     stopWatchEffect() // Invoke to stop watching
   }

   // PART 2

   const { posts, error, load } = getPosts() // from Composables / Composition Functions

   load()

   const showPosts = ref(true)

    return { name, age, handleClick, jedis, search, matchingJedis, posts, showPosts, error } // Value of DOM elements can be accessed after returning
  }
}
</script>
