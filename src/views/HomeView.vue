<template>
  <div>
    <h1>Rick and Morty Characters</h1>
    <CharacterList />
  </div>
</template>

<script>
import CharacterList from '@/components/CharacterList.vue';

export default {
  name: 'HomeView',
  components: {
    CharacterList,
  },
};
</script>
