<template>
  <div id="app">
    <div class="container" v-if="currentCatPicture">
      <img
        class="cat-picture"
        :src="currentCatPicture.url"
        alt="creepy old cat painting"
      />
      <div class="quote">
        <p>{{ currentQuote.text }}</p>
        <p>{{ currentQuote.author }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
// TODO Stylize quote card - author name bold, quote in italics
// TODO Button to allow new image/quote pair
// TODO Big, fancy, gold frame?

export default {
  name: 'App',
  data() {
    return {
      currentCatPicture: '',
      currentQuote: '',
    };
  },
  async created() {
    const catPictures = await axios.get(
      'https://limitless-refuge-78150.herokuapp.com/'
    );
    const quotes = await axios.get('https://type.fit/api/quotes');
    this.currentCatPicture = catPictures.data[Math.floor(Math.random() * catPictures.data.length)];
    this.currentQuote = quotes.data[Math.floor(Math.random() * quotes.data.length)];
  },
};
</script>

<style lang="scss">
html, body {
  height: 100vh;
  width: 100vw;
  overflow: hidden;
}

#app {
  height: 100%;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.container {
  height: 100%;
  width: 80%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.quote {
  padding: 3%;
  margin: 5%;
  box-shadow: 5px 5px 11px 5px rgba(0,0,0,0.71);
  min-width: 15%;
}

.cat-picture {
  height: 70vmin;
  width: auto;
  box-shadow: 5px 5px 11px 5px rgba(0,0,0,0.71);
}
</style>
