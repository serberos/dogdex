<template>
  <q-page class="row flex-center fit bg-primary">
    <div class="col-6 text-center">
      <div class="q-display-2 text-white">Cadastro Dogdex.org</div>
      <q-field
        class="q-pt-xl"
        label="Nome"
        orientation="vertical"
      >
        <q-input
          v-model="form.name"
          color="white"
          inverted-light
        />
      </q-field>
      <q-field
        class="q-pt-md"
        label="URL"
        orientation="vertical"
      >
        <q-input
          v-model="form.image"
          color="white"
          inverted-light
        />
      </q-field>
      <q-btn
        class="q-mt-xl"
        style="width: 150px; height: 40px;"
        label="Enviar"
        color="purple-9"
        @click="save"
      />
    </div>
  </q-page>
</template>

<script>
// import FormDog from '../components/form'

export default {
  name: 'New',
  data () {
    return {
      form: {
        name: '',
        image: ''
      }
    }
  },
  methods: {
    save () {
      const form = JSON.parse(JSON.stringify(this.form))
      this.$axios.post('/api/dogs', form)
        .then(() => {
          this.$q.notify({
            message: 'Cadastro efetuado com sucesso!',
            color: 'purple',
            timeout: 1000
          })
          this.$router.push('/')
        })
        .catch(err => {
          this.$q.notify({
            message: err,
            type: 'negative',
            timeout: 1000
          })
        })
    }
  }
}
</script>
