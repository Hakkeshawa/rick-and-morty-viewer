<template>
    <div class="character-card">
        <img :src="character.image" :alt="character.name" />
        <h2>{{ character.name }} </h2>
        <p>Status: {{ character.status }}</p>
    <p>Species: {{ character.species }}</p>
  </div>
</template>
<script>
export default {
  props: {
    character: Object,
  },
};
</script>

<style scoped>
.character-card {
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 16px;
  text-align: center;
}
.character-card img {
  max-width: 100%;
  border-radius: 50%;
}
</style>