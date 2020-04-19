<template>
  <body>
    <h1>Select Breaking Bad Characters</h1>
  <div id="app">
    <character-filter-form class="characters" :characters="characters" />
    <character-detail />
  </div>

  <div >
    <h2 class="quoteTitle">Quote Of The Day</h2>

    <quote-detail />
    <quote-form class="quote" :quotes="quotes" />
  </div>
  <div class="">
  </div>
</body>

</template>

<script>
import { eventBus } from './main.js'
import CharacterListForm from './components/CharacterListForm.vue'
import CharacterDetail from './components/CharacterDetail.vue'
import QuoteForm from './components/QuoteForm.vue'
import QuoteDetail from './components/QuoteDetail.vue'

export default {
  name: 'app',
  data(){
    return {
      characters: [],
      quotes: []
    };
  },
  mounted(){
    fetch('https://www.breakingbadapi.com/api/characters')
    .then(res => res.json())
    .then(characters => this.characters = characters)

    fetch('https://breaking-bad-quotes.herokuapp.com/v1/quotes/53')
    .then(res => res.json())
    .then(quotes => this.quotes = quotes)

    eventBus.$on('quote-selected', (quote) => {
      this.selectedQuote = quote;
    })

    eventBus.$on('character-selected', (character) => {
      this.selectedCharacter = character;
    })
  },
  components: {
    "character-filter-form": CharacterListForm,
    "character-detail": CharacterDetail,
    "quote-form": QuoteForm,
    "quote-detail": QuoteDetail,
  },
}
</script>

<style>
div {

}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  flex-direction: column;
}

body {
  background-color: black;
  padding: 10px;;
}

h1  {
  color: white;
  display: flex;
  justify-content: center;
  font-size: 80px;
}

.quoteTitle {
  padding-top: 20rem;
  color: white;
  display: flex;
  justify-content: center;
  font-size: 80px;
}
h3 {
  color: white;
  display: flex;
  justify-content: center;
  font-size: 2rem;
}

.quote {
  display: flex;
  justify-content: center;
}

.characters {
  display: flex;
  justify-content: center;
}
</style>
