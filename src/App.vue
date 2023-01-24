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
      <option>people</option>
      <option>films</option>
      <option>planets</option>
      <option>starships</option>
      <option>all</option>
    </select>

    <button @click="getItemsAndRecommedatios()">Search</button>
    
    <!-- respose of get -->
    <div v-for="item in items_rec.item"> <!--:key="p.name">-->
        <h2>{{ item.name }}</h2>
    </div>

  </WelcomeItem>
</template>

<script>
export default {
  data() {
    return {
      selected: 'all',
      options: [
        { text: 'people', value: 'people' },
        { text: 'films', value: 'films' },
        { text: 'planets', value: 'planets' },
        { text: 'starships', value: 'starships' },
        { text: 'all', value: 'all' }
      ],
      name: '',
      items_rec: []
    }
  },
  methods: {
  
    getItemsAndRecommedatios() {
      // TODO: remove url hard coded -->
      fetch(`http://127.0.0.1:5000/${this.selected}/${this.name}`)
        .then(response => response.json())
        .then(data => this.items_rec = data)
    }
  },
  click() {
    this.getItemsAndRecommedatios()
  }
}

</script>