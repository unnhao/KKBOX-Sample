<template>
  <section>
    <div class="title">
      <h2 class="  font-weight-bold">熱門歌單</h2>
    </div>
    <div class="row">
      <div
        class="card mb-2 "
        style="width: 18rem;"
        v-for="item in hotList"
        :key="item.description"
        @click="goToYTPlayer(item.id, item.title)"
      >
        <img :src="item.images[0].url" class="card-img-top" />
        <div class="card-body p-2">
          <p class="card-text text-center ">
            {{ item.title }}
          </p>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  data() {
    return {
      hotList: ''
    };
  },
  methods: {
    goToYTPlayer(daylistID, daylistTitle) {
      this.$store.state.YTDayListID = daylistID;
      this.$store.state.YTDayListTitle = daylistTitle;
      this.$router.push({
        path: '/YTPlayer'
      });
    }
  },
  created() {
    this.$http
      .get(
        'https://api.kkbox.com//v1.1/new-hits-playlists?territory=TW',
        this.$store.state.config
      )
      .then(res => {
        this.hotList = res.data.data;
      });
  }
};
</script>
<style scoped>
section {
  width: 1120px;
  margin: 40px auto 50px auto;
}
.row {
  margin: 0 auto;
}
.link {
  text-decoration: none;
}
.card {
  max-width: 23%;
  margin-right: 2%;
  cursor: pointer;
  background: none;
  border: 5px solid transparent;
  opacity: 1;
  -webkit-transition: 0.3s ease-in-out;
  transition: 0.3s ease-in-out;
}
.card:hover {
  opacity: 0.5;
}
.card-body {
  background: #733195;
}
.card-text {
  font-weight: bold;
  font-size: 16px;

  color: white;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI',
    'Microsoft JhengHei', Roboto, 'Helvetica Neue', Arial, sans-serif;
}
hr {
  border-top: 1px solid black;
}
h2 {
  color: #e331a0;
}
</style>
