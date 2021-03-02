<template>
  <div class="home">
    home
    <p>My name is {{ name }} and my age is {{ age }}</p> <!-- Vue automatically uses 'name.value' as the element value. In the template, we don't use the value property -->
    <button @click="handleClick">Click me</button>
    <button @click="age++">Increment age</button>
    <input type="text" v-model="name"> <!-- 2 Way Data Binding -->

  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'Home',
  setup() { // Vue using the Composition API

    // Creating reactive variables like the data() method in the options API
    // This is done using the template refs to make variables reactive
    const name = ref('Shameel')
    const age = ref(20)

    //const p = ref(null) //Template reference - "null" is for the initial value for the <p> element before returning and getting the DOM value

   const handleClick = () => {
     name.value = 'codename_shameel' // Updating data using the Composition API
     age.value = 19
   }

    return { name, age, handleClick} // Value of DOM elements can be accessed after returning
  }
}
</script>
