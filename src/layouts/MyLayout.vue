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
        <q-input style="width:17rem" class="absolute-right q-pr-md" outlined bg-color="white" v-model="searchModel.string" label="Search" @keyup.enter="search()">
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
          <q-item clickable tag="a" target="_blank" href="https://newsapi.org/">
            <q-item-section avatar>
              <q-icon name="home" />
            </q-item-section>
            <q-item-section>
              <q-item-label>News Api</q-item-label>
              <q-item-label caption>Api used to get the news</q-item-label>
            </q-item-section>
        </q-item>
        <q-item-label header>
          <q-icon name="filter_list" style="color: #ccc; font-size: 1.6em;"/>
          Filtrar
        </q-item-label>
        <q-item clickable>
          <q-checkbox @click.native="change_checkbox()" keep-color v-model="checkbox[0]" label="Usa Today" color="primary" />
        </q-item>
        <q-item clickable>
          <q-checkbox @click.native="change_checkbox()" keep-color v-model="checkbox[1]" label="Cnn" color="positive" />
        </q-item>
        <q-item clickable>
          <q-checkbox @click.native="change_checkbox()" keep-color v-model="checkbox[2]" label="Bbc" color="warning" />
        </q-item>
        <q-item clickable>
          <q-checkbox @click.native="change_checkbox()" keep-color v-model="checkbox[3]" label="Wall Street" color="negative" />
        </q-item>
      </q-list>
    </q-drawer>
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import Vue from 'vue'
export default {
  name: 'MyLayout',
  data () {
    return {
      checkbox: [true, true, true, true],
      leftDrawerOpen: false,
      searchModel: { string: '', source: '' }
    }
  },
  created () {
    Vue.prototype.$ck = this.checkbox
    Vue.prototype.$search = this.searchModel
  }
  // methods: {
  //   change_checkbox () {
  //     this.$ck = this.checkbox
  //     console.log(this.$ck)
  //   },
  //   search () {
  //     this.$search = this.searchModel
  //     console.log(this.$search)
  //   }
  // }
}
</script>
