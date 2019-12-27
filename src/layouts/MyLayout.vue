<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="bg-blue-grey-10 no-wrap row">
      <q-toolbar class="q-pa-sm">
        <q-btn
          flat
          dense
          round
          @click="leftDrawerOpen = !leftDrawerOpen"
          icon="menu"
          aria-label="Menu"
          style="font-size: 1.6em;"
        />
        <q-toolbar-title class=" absolute-center text-h5" >
          Merge the news
        </q-toolbar-title>
        <q-input style="width:17rem" class="absolute-right q-pr-md" outlined bg-color="white" v-model="searchModel" label="Search">
          <template v-slot:prepend>
            <q-icon name="search" />
          </template>
        </q-input>
      </q-toolbar>
    </q-header>
    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-2"
    >
      <q-list>
        <q-item-label header>
          <q-icon name="settings_applications" style="color: #ccc; font-size: 1.6em;"/>
          Opções
        </q-item-label>
        <q-item clickable tag="a" target="_blank" href="https://github.com/Vakihito/get-news">
          <q-item-section avatar>
            <q-icon name="code" />
          </q-item-section>
          <q-item-section>
            <q-item-label>Github</q-item-label>
            <q-item-label caption>github.com/Vakihito/get-news</q-item-label>
          </q-item-section>
        </q-item>
          <q-item clickable tag="a" href="http://localhost:8080/#/aki">
            <q-item-section avatar>
              <q-icon name="home" />
            </q-item-section>
            <q-item-section>
              <q-item-label>Home</q-item-label>
              <q-item-label caption>Página inicial</q-item-label>
            </q-item-section>
        </q-item>
        <q-item-label header>
          <q-icon name="filter_list" style="color: #ccc; font-size: 1.6em;"/>
          Filtrar
        </q-item-label>
        <q-item clickable >
          <q-checkbox keep-color v-model="globo" label="Globo" color="primary" />
        </q-item>
        <q-item clickable>
          <q-checkbox keep-color v-model="reddit" label="reddit" color="warning" />
        </q-item>
        <q-item clickable>
          <q-checkbox keep-color v-model="terra" label="Terra" color="positive" />
        </q-item>
        <q-item clickable>
          <q-checkbox keep-color v-model="folha" label="Folha de SP" color="negative" />
        </q-item>
      </q-list>
    </q-drawer>
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: 'MyLayout',

  data () {
    return {
      globo: true,
      terra: true,
      reddit: true,
      folha: true,
      leftDrawerOpen: false,
      searchModel: ''
    }
  }
}
</script>
