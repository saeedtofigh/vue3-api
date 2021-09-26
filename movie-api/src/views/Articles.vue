<template>
  <div class="d-flex flex-row align-items-center justify-content-center my-4">
    <select v-model="page" @click="data" class="form-control  w-25 mx-3">
      <option v-for="p in pages" :key="p" :value="`${p}`">{{ p }}</option>
    </select>
    <p class="text-black bg-warning p-2 fw-bold">
      page {{ page }} as {{ pages.length }}
    </p>
  </div>
  <div class="articles">
    <div id="article" class="article mx-1">
      <article
        v-for="article in articles"
        :key="article.slug"
        class=" card shadow  p-1 d-flex flex-column align-items-center"
      >
        <div class="img-container">
          <img :src="`${article.poster}`" alt="" />
        </div>
        <h3>
          {{ article.title }}
        </h3>
        <p>country: {{ article.country }}</p>
        <router-link class="btn btn-info" :to="`/detail/${article.id}`"
          >+more
        </router-link>
      </article>
    </div>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        articles: [],
        page: 1,
        pages: [1, 2, 3, 4, 5, 6, 7, 8, 9],
      };
    },

    mounted() {
      document.querySelector('title').textContent = 'Movies';

      this.data();
    },
    methods: {
      data() {
        const axios = require('axios').default;
        const url = `http://moviesapi.ir/api/v1/movies?page=${this.page}`;
        axios
          .get(url)
          .then((response) => {
            this.articles = response.data.data;
          })
          .catch((err) => err);
      },
    },
  };
</script>
<style scoped>
  .articles {
    display: grid;
    place-items: center;
  }
  #article {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    grid-column-gap: 10rem;
    grid-row-gap: 1rem;
    width: 90%;
    place-items: center;
  }
  .img-container {
    width: 100%;
  }
  article {
    width: 25rem;
    height: 25rem;
    border-radius: 6px;
  }
  img {
    width: 100%;
    height: 15rem;
  }
</style>
