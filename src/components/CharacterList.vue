<template>
    <div>
      <div>
        <input v-model="filters.name" placeholder="Filter by name" />
        <select v-model="filters.status">
          <option value="">All</option>
          <option value="Alive">Alive</option>
          <option value="Dead">Dead</option>
          <option value="unknown">Unknown</option>
        </select>
        <button @click="applyFilters">Apply</button>
      </div>
      <div v-if="loading">Loading...</div>
      <div v-else>
        <div v-for="character in characters" :key="character.id">
          <CharacterCard :character="character" />
        </div>
        <div>
          <button @click="prevPage" :disabled="page === 1">Previous</button>
          <button @click="nextPage">Next</button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import CharacterCard from './CharacterCard.vue';
  
  export default {
    components: {
      CharacterCard,
    },
    data() {
      return {
        characters: [],
        loading: false,
        page: 1,
        filters: {
          name: '',
          status: '',
        },
      };
    },
    methods: {
      async fetchCharacters() {
        this.loading = true;
        const { name, status } = this.filters;
        const response = await axios.get(
          `https://rickandmortyapi.com/api/character/?page=${this.page}&name=${name}&status=${status}`
        );
        this.characters = response.data.results;
        this.loading = false;
      },
      applyFilters() {
        this.page = 1;
        this.fetchCharacters();
      },
      prevPage() {
        if (this.page > 1) {
          this.page -= 1;
          this.fetchCharacters();
        }
      },
      nextPage() {
        this.page += 1;
        this.fetchCharacters();
      },
    },
    mounted() {
      this.fetchCharacters();
    },
  };
  </script>
  