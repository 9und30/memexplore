<template>
  <h1 class="title">memexplore</h1>
  <div class="meme">
    <img :src="meme_img" alt="funny meme" class="meme-img">
    <a :href="meme_link" class="subreddit" target="_blank">r/{{meme_sub}}</a>
  </div>
  <button class="generate-btn" @click="generate_meme">another one</button>
</template>

<script>


export default {
  name: 'App',
  components: {

  },
  data() {
    return {
      meme_link: String,
      meme_img: String,
      meme_sub: String
      }
  },
  mounted() {
    this.generate_meme();
  },
  methods: {
    generate_meme() {
      this.axios.get('https://meme-api.herokuapp.com/gimme').then((response) => {
      this.meme = response.data;
      this.meme_link = response.data.postLink;
      this.meme_img = response.data.url;
      this.meme_sub = response.data.subreddit;
      });
    }
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Balsamiq+Sans:wght@400;700&display=swap');

  :root {
    --red: #b65656;
  }

  *, *::before, *::after {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: 'Balsamiq Sans', sans-serif;
    font-weight: 700;
    color: white;
  }

  body, html, #app {
    width: 100%;
    height: 100%;
  }

  #app {
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: #b65656;
  }

  .title {
    height: 7.5%;
    position: static;
    top: 5%;
    font-size: 3rem;
    text-align: center;
  }

  .meme {
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: center;
    height: 75%;
  }

  .meme-img {
    border-radius: 1rem;
    border: 1rem solid white;
    background-color: white;
    height: 85%;
    max-width: 100%;
    object-fit: scale-down;
  }

  .subreddit {
    border-radius: .25rem;
    background-color: white;
    padding: .25rem;
    color: var(--red);
    text-align: center;
    text-decoration: none;
    height: 5%;
  }

  .generate-btn {
    text-transform: uppercase;
    padding: .5rem 1rem;
    background-color: var(--red);
    border: 5px solid white;
    font-size: 1.5rem;
    color: white;
    position: absolute;
    bottom: 5%;
    height: 7.5%;
    text-align: center;
  }

  .generate-btn:hover {
    background-color: white;
    color: var(--red);
    cursor: pointer;
  }
</style>
