<template>
    <q-page>
        <!-- principal news -->
        <div class="container">
            <div class="row flex q-mt-md q-mx-xl justify-center content-start">
                <div v-for="top_new in most_relevant_news" v-bind:key="top_new.id" style="width:25%; height:32rem " class="col-3 q-mt-lg">
                    <div class="full-height full-width">
                        <q-img class="full-height" :src="top_new.urlToImage">
                            <q-chip v-if="top_new.source.id == 'the-new-york-times'" square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 20%;" icon="public" color="primary">Times</q-chip>
                            <q-chip v-if="top_new.source.id == 'cnn'" square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 20%;" icon="public" color="positive">Cnn</q-chip>
                            <q-chip v-if="top_new.source.name == 'Bbc.com'" square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 20%;" icon="public" color="warning">Bbc</q-chip>
                            <q-chip v-if="top_new.source.id == 'the-wall-street-journal'" square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 20%;" icon="public" color="negative">Wall street</q-chip>
                            <div class="text-weight-bold text-subtitle1 absolute-bottom" style=" max-height:19%; min-height:19%">{{top_new.title}}</div>
                        </q-img>
                    </div>
                </div>
            </div>
        </div>

        <!-- all the other news  -->
        <div class="container wrap">
            <div class="flex q-mt-xl q-mx-xl justify-between content-start">
                <div v-for="all_new in all_news" :key="all_new.id" style="width:24%; height:13rem" class="q-mt-lg">
                    <q-card v-if="all_new.urlToImage != null" class="my-card full-height full-width">
                        <q-img class="full-height full-width" :src="all_new.urlToImage">
                            <q-chip v-if="all_new.source.id == 'the-new-york-times'" square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="primary">Times</q-chip>
                            <q-chip v-if="all_new.source.id == 'cnn'" square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="positive">Cnn</q-chip>
                            <q-chip v-if="all_new.source.name == 'Bbc.com'" square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="warning">Bbc</q-chip>
                            <q-chip v-if="all_new.source.id == 'the-wall-street-journal'" square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="negative">Wall street</q-chip>
                            <div style="max-height:28%; min-height:28%" class="text-weight-bold text-subtitle2 absolute-bottom">{{all_new.title}}</div>
                        </q-img>
                    </q-card>
                    <q-card v-else class="my-card full-height full-width">
                        <q-img class="full-height full-width" src="../assets/Images/meta-logo.png">
                            <q-chip v-if="all_new.source.id == 'the-new-york-times'" square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="primary">Times</q-chip>
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
      times_checkbox: true,
      bbc: true,
      cnn: true,
      wsj: true,
      leftDrawerOpen: false,
      searchModel: '',
      all_news: [],
      most_relevant_news: []
    }
  },
  created () {
    this.$axios.all([
      // getting the times json of the news
      this.$axios.get('https://newsapi.org/v2/everything?language=en&domains=nytimes.com&apiKey=5415d503418f418697784db93216532d'),
      this.$axios.get('https://newsapi.org/v2/everything?sortBy=popularity&language=en&domains=cnn.com&apiKey=5415d503418f418697784db93216532d'),
      this.$axios.get('https://newsapi.org/v2/everything?language=en&domains=bbc.com&apiKey=5415d503418f418697784db93216532d'),
      this.$axios.get('https://newsapi.org/v2/everything?language=en&domains=wsj.com&apiKey=5415d503418f418697784db93216532d'),
      this.$axios.get('https://newsapi.org/v2/top-headlines?country=us&apiKey=5415d503418f418697784db93216532d')
    ])
      .then(responseArr => {
        for (let idx = 0; idx < 20; idx++) {
          this.all_news.push(responseArr[0].data.articles[idx])
          this.all_news.push(responseArr[1].data.articles[idx])
          this.all_news.push(responseArr[2].data.articles[idx])
          this.all_news.push(responseArr[3].data.articles[idx])
        }
        for (let idx = 0; idx < 4; idx++) {
          this.most_relevant_news.push(responseArr[3].data.articles[idx])
        }
        console.log(this.most_relevant_news)
      })
  }
}
</script>
<style lang="scss" scoped>
</style>
