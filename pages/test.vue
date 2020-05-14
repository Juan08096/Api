<template>
  <section class="mt-8 container mx-auto px-4">
    <div>
      <table class="table-fixed">
        <thead>
          <tr>
            <th class="w-1/4 px-4 py-2">ID</th>
            <th class="w-1/4 px-4 py-2">Name</th>
            <th class="w-1/4 px-4 py-2">Status</th>
            <th class="w-1/4 px-4 py-2">Specie</th>
            <th class="w-1/4 px-4 py-2">Gender</th>
            <th class="w-1/4 px-4 py-2">Origin</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(tr, indextr) in list" :key="indextr.id" :data="tr">
            <td class="border px-4 py-2">{{ tr.id }}</td>
            <td class="border px-4 py-2">{{ tr.name }}</td>
            <td class="border px-4 py-2">{{ tr.status }}</td>
            <td class="border px-4 py-2">{{ tr.species }}</td>
            <td class="border px-4 py-2">{{ tr.gender }}</td>
            <td class="border px-4 py-2">{{ tr.origin.name }}</td>
            <td class="border px-4 py-2">
              <button icon="EyeIcon" @click.stop="handleClickUser(tr)">
                Ver Detalle
              </button>
            </td>
          </tr>
        </tbody>
      </table>
      <infinite-loading @infinite="infiniteScroll"></infinite-loading>
    </div>
  </section>
</template>

<script>
import axios from 'axios'
import InfiniteLoading from 'vue-infinite-loading'

export default {
  components: {
    InfiniteLoading
  },
  data() {
    return {
      list: [],
      page: 0
    }
  },

  created() {},

  destroyed() {},

  mounted() {},

  computed: {},

  methods: {
    infiniteScroll($state) {
      this.page++
      let url = 'https://rickandmortyapi.com/api/character/?page=' + this.page

      axios.get(url).then(response => {
        let posts = response.data.results
        console.log('holi')

        if (posts.length) {
          this.list = this.list.concat(posts)
          $state.loaded()
        } else {
          $state.complete()
        }
      })
    },
    handleClickUser(character) {
      this.$router.push({ name: 'id', params: { id: character.id } })
    }
  },

  watch: {}
}
</script>
