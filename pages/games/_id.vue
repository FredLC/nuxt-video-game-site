<template>
  <div class="container mx-auto">
    <div>{{ game.name }}</div>
    <img :src="game.cover.url.replace('t_thumb', 't_cover_big')" alt="cover" />
    <p>{{ game.summary }}</p>
    <div>{{ game.platforms }}</div>
    <p>{{ game.first_release_date }}</p>
    <p>{{ game.total_rating }}</p>
    <div>{{ game.screenshots }}</div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  asyncData({ params, error }) {
    const proxyurl = "https://cors-anywhere.herokuapp.com/";
    return axios
      .get(
        `${proxyurl}https://api-v3.igdb.com/games/${params.id}/?fields=name,cover.url,summary,platforms.name,first_release_date,websites,total_rating,screenshots.url,total_rating&expand=platforms,screenshots,cover`
      )
      .then(res => {
        return {
          game: res.data[0]
        };
      })
      .catch(e => {
        console.log(e);
      });
  },
  head() {
    return {
      title: this.game.name + " | Top Video Games"
    };
  }
};
</script>
