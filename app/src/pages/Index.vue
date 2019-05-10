<template>
  <q-page class="row justify-start items-start content-start bg-grey-4 q-pa-lg">
    <div class="q-display-2 q-pa-sm text-faded col-12">Dogdex.org</div>
    <div
      class="q-pt-lg"
      v-for="(dog, index) in dogs"
      :key="index"
    >
      <dogs :dog="dog" />
    </div>
  </q-page>
</template>

<style>
</style>

<script>
import dogs from '../components/dogs'

export default {
  name: 'PageIndex',
  components: { dogs },
  data () {
    return {
      dogs: []
    }
  },
  mounted () {
    this.getDogs()
  },
  methods: {
    getDogs () {
      this.$axios.get('/api/dogs')
        .then(res => {
          this.dogs = res.data
        })
    }
  }
}
</script>
