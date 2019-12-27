<template>
    <q-page>
        <!-- principal news -->
        <div class="container">
            <div class="row flex q-mt-md q-mx-xl justify-center content-start">
                <div style="width:25%; height:32rem " class="col-3 q-mt-lg">
                    <div class="full-height full-width">
                        <q-img class="full-height" src="../assets/Images/1.jpg">
                            <q-chip square size="lg" class="q-mt-md q-ml-sm text-weight-medium" style="bottom: 17%;"  icon="public" color="primary">times</q-chip>
                            <div class="text-weight-bold text-subtitle1 absolute-bottom" style=" max-height: 16%;">Uma pequena descrição a cerca da notícia principal de uma site</div>
                        </q-img>
                    </div>
                </div>
                <div style="width:25%; height:32rem " class="col-3 q-mt-lg">
                    <div class="full-height full-width">
                        <q-img class="full-height" src="../assets/Images/2.jpg">
                            <q-chip square size="lg" class="q-mt-md q-ml-sm text-weight-medium" style="bottom: 17%;"  icon="public" color="warning">reddit</q-chip>
                            <div class="text-weight-bold text-subtitle1 absolute-bottom" style=" max-height: 16%;">Uma pequena descrição a cerca da notícia principal de uma site</div>
                        </q-img>
                    </div>
                </div>
                <div style="width:25%; height:32rem " class="col-3 q-mt-lg">
                    <div class="full-height full-width">
                        <q-img class="full-height" src="../assets/Images/3.jpg">
                            <q-chip square size="lg" class="q-mt-md q-ml-sm text-weight-medium" style="bottom: 17%;"  icon="public" color="positive">terra</q-chip>
                            <div class="text-weight-bold text-subtitle1 absolute-bottom" style=" max-height: 16%;">Uma pequena descrição a cerca da notícia principal de uma site</div>
                        </q-img>
                    </div>
                </div>
                <div style="width:25%; height:32rem " class="col-3 q-mt-lg">
                    <div class="full-height full-width">
                        <q-img class="full-height" src="../assets/Images/4.jpg">
                            <q-chip square size="lg" class="q-mt-md q-ml-sm text-weight-medium" style="bottom: 17%;"  icon="public" color="negative">Folha de SP</q-chip>
                            <div class="text-weight-bold text-subtitle1 absolute-bottom" style=" max-height: 16%;">Uma pequena descrição a cerca da notícia principal de uma site</div>
                        </q-img>
                    </div>
                </div>
            </div>
        </div>
        <!-- all the other news  -->
        <div class="container wrap">
            <div class="flex q-mt-xl q-mx-xl justify-between content-start">
                <div style="width:24%; height:13rem" class="q-mt-lg">
                    <q-card class="my-card full-height full-width">
                        <q-img class="full-height" src="../assets/Images/1.jpg">
                            <q-chip square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="primary">times</q-chip>
                            <div style="max-height:30%" class="text-weight-bold text-subtitle2 absolute-bottom">Uma pequena descrição a cerca da notícia secundaria de uma site</div>
                        </q-img>
                    </q-card>
                </div>
                <div style="width:24%; height:13rem" class="q-mt-lg">
                    <q-card class="my-card full-height full-width">
                        <q-img class="full-height" src="../assets/Images/3.jpg">
                            <q-chip square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="warning">reddit</q-chip>
                            <div style="max-height:30%" class="text-weight-bold text-subtitle2 absolute-bottom">Uma pequena descrição a cerca da notícia secundaria de uma site</div>
                        </q-img>
                    </q-card>
                </div>
                <div style="width:24%; height:13rem" class="q-mt-lg">
                    <q-card class="my-card full-height full-width">
                        <q-img class="full-height" src="../assets/Images/2.jpg">
                            <q-chip square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="positive">terra</q-chip>
                            <div style="max-height:30%" class="text-weight-bold text-subtitle2 absolute-bottom">Uma pequena descrição a cerca da notícia secundaria de uma site</div>
                        </q-img>
                    </q-card>
                </div>
                <div style="width:24%; height:13rem" class="q-mt-lg">
                    <q-card class="my-card full-height full-width">
                        <q-img class="full-height" src="../assets/Images/4.jpg">
                            <q-chip square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="negative">Folha de SP</q-chip>
                            <div style="max-height:30%" class="text-weight-bold text-subtitle2 absolute-bottom">Uma pequena descrição a cerca da notícia secundaria de uma site</div>
                        </q-img>
                    </q-card>
                </div>
                <div style="width:24%; height:13rem" class="q-mt-lg">
                    <q-card class="my-card full-height full-width">
                        <q-img class="full-height" src="../assets/Images/1.jpg">
                            <q-chip square size="lg" class="q-mt-md q-ml-sm text-weight-medium"  style="bottom: 31%;" icon="public" color="negative">Folha de SP</q-chip>
                            <div style="max-height:30%" class="text-weight-bold text-subtitle2 absolute-bottom">Uma pequena descrição a cerca da notícia secundaria de uma site</div>
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
      terra: true,
      reddit: true,
      folha: true,
      leftDrawerOpen: false,
      searchModel: '',
      reddit_news: [],
      times_news: [],
      terra_news: [],
      folha_news: []
    }
  },
  created () {
    this.$axios.all([
      // getting the times json of the news
      this.$axios.get('https://api.nytimes.com/svc/news/v3/content/all/all.json?api-key=wEjtZ1kh7Fnh6bNd967TKsYcLEBSVHj4'),
      this.$axios.get('https://api.github.com/users/phantomjs', 'jsonp')
    ])
      .then(responseArr => {
        this.times_news = responseArr[0].data
        console.log('Times: ', this.times_news.__ob__.value.results)
        console.log('Date created: ', responseArr[1].data.created_at)
      })
  }
}
</script>
<style lang="scss" scoped>
</style>
