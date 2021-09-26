<template>
  <div class="d-flex container justify-content-center align-items-center ">
    <article
      v-if="active"
      v-show="active"
      class="card shadow p-3 w-75 text-center d-flex flex-row flex-column-sm"
    >
      <img :src="`${poster}`" :alt="`${title}`" />
      <div class="information">
        <h1 class="card-title">
          {{ title }}
        </h1>
        <p class="text-secondary card-text">plot: {{ plot }}</p>
        <span class="badge rounded-pill bg-warning text-dark"
          >year: {{ year }}</span
        >
        <div>
          <span class="badge rounded-pill bg-info text-dark"
            >genres: <span v-for="genere in genres" :key="genere">
             {{ genere }} &nbsp;

            </span> 
          </span>
        </div>
        <div class="">
          <p>
            actors:
            {{ actors }} 

          </p>
        </div>
        <router-link class="text-center btn btn-danger" to="/article"
          >back to home🏠</router-link
        >
      </div>
    </article>
    <div
      v-else
      class="d-flex container justify-content-center align-items-center "
    >
      <div class="spinner-border text-secondary" role="status">
        <span class="visually-hidden ">Loading...</span>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        active: false,
        detail: this.$route.fullPath,
        title: '',
        poster: '',
        year: '',
        actors: '',
        genres: '',
        plot: '',
      };
    },

    mounted() {
      //  http://moviesapi.ir/api/v1/movies/{movie_id}
      const DetailID = this.detail.replace('/detail/', '').trim();
      const url = `http://moviesapi.ir/api/v1/movies/${DetailID}`;

      fetch(url)
        .then((response) => response.json())
        .then((response) => {
          const { title, poster, year, actors, genres, plot } = response;
          this.title = title;
          this.poster = poster;
          this.year = year;
          this.actors = actors;

          this.genres = genres;
          this.plot = plot;
        });
      setTimeout(() => {
        this.active = !this.active;
      }, 2000);
      document.querySelector('title').textContent = `Detail`;

    },
  };
</script>
<style scoped>
  h1 {
    text-transform: uppercase;
    color: #666;
  }
  p {
    color: #222;
    font-weight: 700;
  }
  img {
    max-width: 100%;
    width: 20rem;
    height: 20rem;
    border-radius: 6px;
  }
</style>
