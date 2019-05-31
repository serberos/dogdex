<template>
  <q-layout view="hHh LpR lfr">
    <q-layout-header>
      <q-toolbar color="primary">
        <q-btn
          flat
          dense
          round
          @click="leftDrawerOpen = !leftDrawerOpen"
          aria-label="Menu"
        >
          <q-icon name="menu" />
        </q-btn>
        <q-toolbar-title>Dogdex.org</q-toolbar-title>
        <q-btn
          v-if="filterSize"
          icon="fas fa-eraser"
          round
          flat
          @click="filterSize = ''"
        />
        <q-btn
          class="q-mr-md"
          icon="fas fa-filter"
          round
          flat
        >
          <q-popover
            anchor="bottom middle"
            self="top middle"
          >
            <q-list
              class="no-padding"
              separator
              link
            >
              <q-item
                v-for="(dog, index) in sizes"
                :key="index"
                @click.native="filterSize = dog.value"
              >
                <q-item-main :label="dog.label" />
              </q-item>
            </q-list>
          </q-popover>
        </q-btn>
        <q-search
          v-model="search"
          color="none"
          inverted
          autofocus
        />
      </q-toolbar>
    </q-layout-header>

    <q-layout-drawer
      v-model="leftDrawerOpen"
      content-class="bg-grey-2"
    >
      <q-list
        no-border
        link
        inset-delimiter
      >
        <q-item to="/">
          <q-item-main label="Dogdex" />
        </q-item>
        <q-item to="/sobre">
          <q-item-main label="About" />
        </q-item>
      </q-list>
    </q-layout-drawer>

    <q-page-container>
      <router-view
        :search="search"
        :filterSize="filterSize"
      />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: 'MyLayout',
  data () {
    return {
      leftDrawerOpen: this.$q.platform.is.desktop,
      search: '',
      sizes: [
        { label: 'Pequeno porte', value: 'p' },
        { label: 'Médio porte', value: 'm' },
        { label: 'Grande porte', value: 'g' }
      ],
      filterSize: ''
    }
  }
}
</script>
