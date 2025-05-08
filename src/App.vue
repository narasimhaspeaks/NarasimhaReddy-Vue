<template>
  <div class="container">
    <MusicHitsHeader />
    <MusicHitsList :muiscHitsDetails="muiscHitsDetails" />
  </div>
</template>

<script>
import MusicHitsHeader from './components/MusicHitsHeader.vue';
import MusicHitsList from './components/MusicHitsList.vue';

export default {
  name: 'App',
  components: { MusicHitsHeader, MusicHitsList },
  data() {
    return {
      muiscHitsDetails: [] // To store fetched song data
    };
  },
  methods: {
    // Fetches music hits data from the backend
    async fetchMusicHits() {
      try {
        const res = await fetch('https://narasimha-node1.onrender.com/api'); // Backend API URL
        const data = await res.json();
        return data; // Assuming the backend returns an array of song objects
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    }
  },
  // When the component is created, fetch the music hits data
 async created() {
  const data = await this.fetchMusicHits();
  console.log("Fetched Data:", data);
  this.muiscHitsDetails = data;
}
}
</script>

<style scoped>
.container {
  display: grid;
  grid-template-rows: auto 1fr;
  gap: 1.5em;
  margin: 0 auto;
  padding: 1em;
  max-width: 1200px;
}
</style>
