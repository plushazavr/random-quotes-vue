<template>
  <div class="app">
    <h2 class="app__header">Quote of the Day</h2>
    <div class="container">
      <div class="quote-day" v-for="quote in quotes" :key="quote">
        <p class="quote-day__text">{{ quote.body }}</p>
        <p class="quote-day__author">{{ quote.author }}</p>

      </div>
      <button class="quote-day__button" @click="fetchQute()">Refresh</button>
      <button  @click="copyQute()">Copy</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

  export default {
  data() {
    return {
      quotes: [],
      text: 'helpMe',
    }
  },
  
  methods: {
    async fetchQute() {
      try {
        const response = await axios.get('https://favqs.com/api/qotd');        
        this.quotes = response.data; //помещыем в модель цитат цитату полученную с сервера
        delete this.quotes.qotd_date
      } catch(e) {
        console.log('Произошла ошибка. Повторите попытку позже')
      }
    },

    copyQute() {
      // navigator.clipboard.writeText(this.quotes.quote.body)
      navigator.clipboard.writeText('"'+ this.quotes.quote.body + '" ' + this.quotes.quote.author)
        .then(() => {
          console.log('Text copy')
        })
        .catch(err => {
          console.log('Something went wrong', err);
        });
    }
    
  },

  mounted() {
    this.fetchQute();
  }
  }
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
.app {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: linear-gradient(107.39deg, #FCA5F1 0%, #B5FFFF 99.76%);
}

.app__header {
  font-family: 'Italiana';
  font-style: normal;
  font-weight: 400;
  font-size: 104.808px;
  line-height: 123px;
  color: #000000;
}

.container {
  background-color: rgba(240, 236, 236, 0.39);
  border-radius: 30px;
  box-shadow: 9px 9px 9px rgba(0, 0, 0, 0.25);
  /* max-height: 250px;
  max-width: 500px; */
  width: 800px;
  height: 440px;
  padding: 50px 50px;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;

  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 400;
  font-size: 28px;
  line-height: 44px;
  color: #000000;
}

.quote-day {
  height: 250px;  
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.quote-day__text{
  margin: 0;
  padding: 0;
  overflow: auto;
}

.quote-day__text::-webkit-scrollbar {
  width: 10px;
  background-color: none;
}

.quote-day__text::-webkit-scrollbar-thumb {
  border-radius: 10px;
  background-color: #D7D5F9;
}

.quote-day__text {
  margin: 0;
  padding: 0;
}

.quote-day__author {
  margin: 0;
  padding: 0;
  font-weight: 700;
  text-align: right;
}

.quote-day__button {
  position: absolute;
  width: 368px;
  height: 86px;
  left: 216px;
  bottom: 27px;
  background: rgba(217, 217, 217, 0.39);
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 30px;
  border: none;
  cursor: pointer;

  font-family: 'Montserrat';
  font-style: normal;
  font-weight: 400;
  font-size: 36px;
  line-height: 44px;
  text-transform: uppercase;
  color: #000000;
}

.quote-day__button:hover {
  box-shadow: inset 0px 4px 4px rgba(0, 0, 0, 0.25);
}
</style>
