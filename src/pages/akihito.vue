<template>
    <q-page>
        <!-- principal news -->
        <div class="q-mt-lg q-mx-xl">
          <q-carousel style="height:35rem" animated v-model="slide" arrows infinite autoplay>
            <q-carousel-slide v-for="top_new in most_relevant_news" v-bind:key="top_new.id" :name="most_relevant_news.indexOf(top_new)" :img-src="top_new.urlToImage" v-on:click="openUrl(top_new.url)">
              <div class="absolute-bottom">
                  <q-chip v-if="top_new.source.id == 'usa-today'" square size="xl" class="q-mb-md q-ml-md text-weight-medium"  icon="public" text-color="white" color="primary">Usa Today</q-chip>
                  <q-chip v-if="top_new.source.id == 'cnn'" square size="xl" class="q-mb-md q-ml-md text-weight-medium"  icon="public" text-color="white" color="positive">Cnn</q-chip>
                  <q-chip v-if="top_new.source.name == 'Bbc.com'" square size="xl" class="q-mb-md q-ml-md text-weight-medium"  icon="public" text-color="white" color="warning">Bbc</q-chip>
                  <q-chip v-if="top_new.source.id == 'the-wall-street-journal'" square size="xl" class="q-mb-md q-ml-md text-weight-medium"  icon="public" text-color="white" color="negative">Wall street</q-chip>
                  <q-chip v-if="top_new.source.id != 'the-wall-street-journal' && top_new.source.name != 'Bbc.com' && top_new.source.id != 'cnn' && top_new.source.id != 'usa-today'" square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="primary" text-color="white">{{top_new.source.name}}</q-chip>
                <div class="custom-caption white" style="font-size:1.7rem">{{top_new.title}}</div>
              </div>
            </q-carousel-slide>
          </q-carousel>
        </div>
        <!-- all the other news  -->
        <div class="container wrap">
            <div class="flex q-mt-xl q-mx-xl justify-between content-start">
                <div v-for="all_new in all_news" :key="all_new.id" style="width:24%; height:13rem" class="q-mt-lg">
                    <q-card v-on:click="openUrl(all_new.url)" target="_blank" v-if="all_new.urlToImage != null" class="my-card full-height full-width">
                      <q-img class="full-height full-width" :src="all_new.urlToImage">
                        <q-chip v-if="all_new.source.id == 'usa-today'" square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="primary">Usa Today</q-chip>
                        <q-chip v-if="all_new.source.id == 'cnn'" square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="positive">Cnn</q-chip>
                        <q-chip v-if="all_new.source.name == 'Bbc.com'" square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="warning">Bbc</q-chip>
                        <q-chip v-if="all_new.source.id == 'the-wall-street-journal'" square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="negative">Wall street</q-chip>
                        <div style="max-height:28%; min-height:28%" class="text-weight-bold text-subtitle2 absolute-bottom">{{all_new.title}}</div>
                       </q-img>
                    </q-card>
                    <q-card v-on:click="openUrl(all_new.url)" v-else class="my-card full-height full-width">
                        <q-img class="full-height full-width" src="../assets/Images/meta-logo.png">
                            <q-chip v-if="all_new.source.id == 'usa-today'" square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="primary">Usa Today</q-chip>
                            <q-chip v-if="all_new.source.id == 'cnn'" square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="positive">Cnn</q-chip>
                            <q-chip v-if="all_new.source.name == 'Bbc.com'" square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="warning">Bbc</q-chip>
                            <q-chip v-if="all_new.source.id == 'the-wall-street-journal'" square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="negative">Wall street</q-chip>
                            <div style="max-height:28%; min-height:28%" class="text-weight-bold text-subtitle2 absolute-bottom">{{all_new.title}}</div>
                        </q-img>
                    </q-card>
                </div>
            </div>
        </div>
    </q-page>
</template>
<script>
export default {
  data () {
    return {
      leftDrawerOpen: false,
      searchModel: '',
      all_news: [],
      most_relevant_news: [],
      slide: 1
    }
  },
  created () {
    this.$axios.all([
      // getting the Usa Today json of the news
      this.$axios.get('https://newsapi.org/v2/everything?language=en&domains=usatoday.com&apiKey=5415d503418f418697784db93216532d'),
      this.$axios.get('https://newsapi.org/v2/everything?sortBy=popularity&language=en&domains=cnn.com&apiKey=5415d503418f418697784db93216532d'),
      this.$axios.get('https://newsapi.org/v2/everything?language=en&domains=bbc.com&apiKey=5415d503418f418697784db93216532d'),
      this.$axios.get('https://newsapi.org/v2/everything?language=en&domains=wsj.com&apiKey=5415d503418f418697784db93216532d'),
      this.$axios.get('https://newsapi.org/v2/top-headlines?country=us&apiKey=5415d503418f418697784db93216532d')
    ])
      .then(responseArr => {
        for (let idx = 0; idx < 20; idx++) {
          for (let i = 0; i < 4; i++) {
            this.all_news.push(responseArr[i].data.articles[idx])
          }
        }
        for (let idx = 0; idx < 4; idx++) {
          this.most_relevant_news.push(responseArr[4].data.articles[idx])
        }
        console.log(responseArr[4].data)
      })
  },
  methods: {
    openUrl (url) {
      window.open(url, '_blank')
    }
  }
}
</script>
<style lang="scss" scoped>
  .custom-caption{
    text-align: center;
    padding: 12px;
    color: white;
    background-color: rgba(0, 0, 0, .3);
  }
</style>
