<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <form action="" @submit.prevent>
      <input type="text" name="chuckjokes" v-model="chucknorris">
      <input type="submit" value="chuck it" @click.prevent="postJoke()">
    </form>
    <ul>
      <li v-for="joke in chuckJokes" :key="joke.key">{{ joke.joke }}</li>
    </ul>
  </div>
</template>

<script>
import { db } from '../services/firebase'

export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js PWA',
      chucknorris: ''
    }
  },
  methods: {
    postJoke () {
      db.ref('chuckJokes').push({
        joke: this.chucknorris
      })
      this.chucknorris = ''
    }
  },
  firebase: {
    chuckJokes: db.ref('chuckJokes')
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #35495E;
}
</style>
