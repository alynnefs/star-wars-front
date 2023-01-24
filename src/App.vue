<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <WelcomeItem>
    <template #heading>Search people, films, planets or starships</template>
    <br />

    <input v-model="name" placeholder="search here" />
    
    <div>Selected: {{ selected }}</div>

    <select v-model="selected">
      <option disabled value="">Please select one</option>
      <option>People</option>
      <option>Films</option>
      <option>Planets</option>
      <option>Starships</option>
      <option>All</option>
    </select>

    <button @click="search">Search</button>


  </WelcomeItem>
</template>

<script>

export default {
  data() {
    return {
      selected: 'All',
      options: [
        { text: 'People', value: 'People' },
        { text: 'Films', value: 'Films' },
        { text: 'Planets', value: 'Planets' },
        { text: 'Starships', value: 'Starships' },
        { text: 'All', value: 'All' }
      ],
      name: ''
    }
  },
  methods: {
    search(event) {
      
      console.log(`Hello ${this.name}, ${this.selected}!`);
      fetch("http://127.0.0.1:5000/people/luke")
        .then(response => response.json())
        .then(data => console.log(data));
    }
  }
}

</script>