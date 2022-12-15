<template>
  <div class="app">
    <h2 class="app__header">Quote of the Day</h2>
    <div class="container">
      <div class="qod" v-for="quote in quotes" :key="quote">
        <p class="qod__text">{{quote.body}}</p>
        <p class="qod__author">{{quote.author}}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

  export default {
  data() {
    return {
      quotes: []
    }
  },

  methods: {

    async fetchPost() {
      try {
        const response = await axios.get('https://favqs.com/api/qotd');
        this.quotes = response.data; //помещыем в модель постов пост полученный с сервера
      } catch(e) {
        console.log('Произошла ошибка. Повторите попытку позже')
      }
    }
  },

  mounted() {
    this.fetchPost();
  }
  }
</script>

<style>
.app {
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.container {
  background-color: white;
  border: 1px solid red;
  /* max-height: 250px;
  max-width: 500px; */
  height: 250px;
  width: 500px;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;

}

.quote__text{
  margin: 0;
  padding: 0;
}
</style>
