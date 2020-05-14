<template>
  <section class="mt-8 container mx-auto px-4">
    <div class="flex flex-wrap">
      <div class="w-1/2 mr-12 max-w-sm rounded shadow-xl overflow-hidden tam">
        <img
          class="w-full"
          :src="character.image" 
          alt="Sunset in the mountains"
        />
        <div class="px-6 py-4 text-center">
          <div class="font-bold text-xl mb-2">{{ character.name }}</div>
          <p class="text-gray-700 text-base">
            {{ character.species }}
          </p>
        </div>
        <div class="px-6 py-4 text-center">
          <span
            class="my-2 inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2"
            >Gender: {{ character.gender }} </span
          >
          <span
            class="my-2 inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2"
            >Origin: {{ character.origin.name }} </span
          >
          <span
            class="my-2 inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2"
            >Location: {{ character.location.name }} </span
          >
          <span
            class="my-2 inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700"
            >Status: {{ character.status }}</span
          >
        </div>
      </div>
      <div class="w-1/2 overflow-y-scroll overflow-hidden tam">
        <table class="table-fixed text-center">
          <thead>
            <tr>
              <th class="w-1/2 px-4 py-2">Episodio</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="characters in character.episode" :key="characters">
              <td class="border px-4 py-2">{{ characters }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </section>
</template>

<script>
import axios from 'axios'

export default {
  asyncData({ params }) {
    return {
      characterId: params.id
    }
  },

  data() {
    return {
      character: []
    }
  },

  async fetch() {    
    const id = this.$route.params.id 
    const url = `https://rickandmortyapi.com/api/character/${id}`
    await axios
      .get(url)
      .then(res => {
        this.character = res.data
        console.log(res)
      })
      .catch(err => {
        console.log(err)
      })
  }
}
</script>

<style scoped>
.tam{
  max-height: 700px;
}
</style>