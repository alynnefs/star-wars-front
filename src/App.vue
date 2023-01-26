<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <WelcomeItem>
    <h1 class="text">Search people, films, planets or starships</h1>
    <br />


    <input v-model="name" placeholder="search here" class="filter text"/>

    <select v-model="selected" class="button-52 text">
      <option>people</option>
      <option>films</option>
      <option>planets</option>
      <option>starships</option>
      <option>all</option>
    </select>

    <center>
      <button @click="getItemsAndRecommedatios()" class="button-52 text" role="button">Search</button>
    </center>
    
    <!-- respose of get -->
    <br /><br /><br />
    <div v-for="element in items_rec">
      <h2 class="text">Item found</h2>

      <div class="card">
        <h2 v-if="element.item.name">
          Name:  {{ element.item.name }}
        </h2>
        <h2 v-else>
          Title: {{ element.item.title }}
        </h2>

        <div v-if="element.item.manufacturer">
          <h3>
          <!-- starships -->
          Manufacturer: {{ element.item.manufacturer }}
          <br />
          Crew: {{ element.item.crew}}
          <br />
          Passengers: {{ element.item.passengers }}
          <br />
          Consumables: {{ element.item.consumables }}
          <br />
          Starship Class: {{ element.item.starship_class }}
          </h3>
        </div>

        <!-- planets -->
        <div v-if="element.item.gravity">
          <h3>
          Diameter: {{ element.item.diameter }}
          <br />
          Climate: {{ element.item.climate }}
          <br />
          Gravity: {{ element.item.gravity }}
          <br />
          Terrain: {{ element.item.terrain }}
          <br />
          Population: {{ element.item.population }}
          </h3>
        </div>

        <!-- people -->
        <div v-if="element.item.height">
          <h3>
          Height: {{ element.item.height }}cm
          <br />
          Hair color: {{ element.item.hair_color }}
          <br />
          Eye color: {{ element.item.eye_color }}
          <br />
          Skin color: {{ element.item.skin_color }}
          <br />
          Birth year: {{ element.item.birth_year }}
          <br />
          Gender: {{ element.item.gender }}
          </h3>
        </div>

        <!-- film -->
        <div v-if="element.item.episode_id">
          <h3>
          Episode: {{ element.item.episode_id }}
          <br />
          Director: {{ element.item.director }}
          <br />
          Producer: {{ element.item.producer }}
          <br />
          Release date: {{ element.item.release_date }}
          </h3>
        </div>

      </div>
        
      <br />

      <!-- based on type-->
      <h3 class="text">Recommendations:</h3>

      <div v-for="rec in element.recommendations" class="card">
        <h3 v-if="rec.name">Name:  {{ rec.name }}</h3>
        <div v-else>Title: {{ rec.title }}</div>

        <!-- starships -->
        <div v-if="rec.manufacturer">
          Manufacturer: {{ rec.manufacturer }}
          <br />
          Crew: {{ rec.crew}}
          <br />
          Passengers: {{ rec.passengers }}
          <br />
          Consumables: {{ rec.consumables }}
          <br />
          Starship Class: {{ rec.starship_class }}
        </div>

        <!-- planets -->
        <div v-if="rec.gravity">
          Diameter: {{ rec.diameter }}
          <br />
          Climate: {{ rec.climate }}
          <br />
          Gravity: {{ rec.gravity }}
          <br />
          Terrain: {{ rec.terrain }}
          <br />
          Population: {{ rec.population }}
        </div>

        <!-- people -->
        <div v-if="rec.height">
          Height: {{ rec.height }}cm
          <br />
          Hair color: {{ rec.hair_color }}
          <br />
          Eye color: {{ rec.eye_color }}
          <br />
          Skin color: {{ rec.skin_color }}
          <br />
          Birth year: {{ rec.birth_year }}
          <br />
          Gender: {{ rec.gender }}
        </div>

        <!-- film -->
        <div v-if="rec.episode_id">
          Episode: {{ rec.episode_id }}
          <br />
          Director: {{ rec.director }}
          <br />
          Producer: {{ rec.producer }}
          <br />
          Release date: {{ rec.release_date }}
        </div>
        
      </div>
      <br />
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