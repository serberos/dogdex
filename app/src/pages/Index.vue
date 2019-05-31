<template>
  <q-page
    class="row bg-grey-4 q-pa-md"
    :class="dogs.length ? 'content-start' : 'justify-center items-center'"
  >
    <q-modal v-model="modalOpen">
      {{ dogDetail }}
    </q-modal>
    <div
      class="col-3"
      v-for="(dog, index) in dogs"
      :key="index"
    >
      <dogs
        :dog="dog"
        @detail="detail"
      />
    </div>
    <div v-if="!dogs.length">
      <img
        src="~assets/sad.svg"
        style="width: 30vw; max-width: 200px;"
      >
    </div>
  </q-page>
</template>

<script>
import dogs from '../components/dogs'

export default {
  name: 'Index',
  components: { dogs },
  props: ['search', 'filterSize'],
  data () {
    return {
      dogs: [],
      modalOpen: false,
      dogDetail: {}
    }
  },
  watch: {
    search (search) {
      let filter = search ? { params: { filter: { where: { name: { like: `%${search}%` } } } } } : ''
      this.getDogs(filter)
    },
    filterSize (filterSize) {
      let filter = filterSize ? { params: { filter: { where: { size: filterSize } } } } : ''
      this.getDogs(filter)
    }
  },
  mounted () {
    this.getDogs('')
  },
  methods: {
    getDogs (filter) {
      this.$q.loading.show()
      this.$axios.get('/api/dogs', filter)
        .then(res => {
          this.dogs = res.data
        })
        .catch(err => {
          console.log(err)
        })
        .finally(() => {
          setTimeout(() => {
            this.$q.loading.hide()
          }, 200)
        })
    },
    detail (dog) {
      this.$axios('api/Wiki/search', { dog })
        .then(res => {
          this.dogDetail = res.data
        })
        .catch(err => {
          console.log(err)
        })
        .finally(() => {
          this.modalOpen = true
        })
    }
  }
}
</script>
