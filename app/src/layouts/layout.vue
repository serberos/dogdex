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
      <router-view :search="search" />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: 'MyLayout',
  data () {
    return {
      leftDrawerOpen: this.$q.platform.is.desktop,
      search: ''
    }
  }
}
</script>
