<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          @click="leftDrawerOpen = !leftDrawerOpen"
          icon="menu"
          aria-label="Menu"
        />
        <q-toolbar-title>
          Merge the news
        </q-toolbar-title>
        <div>Merge the news v0.01</div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-2"
    >
      <q-list>
        <q-item-label header>Filtrar</q-item-label>
        <q-item clickable>
          <q-checkbox keep-color v-model="globo" label="Globo" color="primary" />
        </q-item>
        <q-item clickable>
          <q-checkbox keep-color v-model="uol" label="Uol" color="warning" />
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
      uol: true,
      folha: true,
      leftDrawerOpen: false
    }
  }
}
</script>
