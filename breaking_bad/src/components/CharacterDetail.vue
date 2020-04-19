<template lang="html">
  <div v-if="character" id="characterDetail">
    <div id="detailWrapper">
      <h2>{{character.name}}</h2>
      <div id="flexWrapper">
        <div id="left">
          <p> <span>Alias: </span>{{character.nickname}} </p>
          <p> <span>occupation: </span>{{character.occupation[0]}}</p>
          <p> <span>status: </span>{{character.status}}</p>
        </div>
        <div id="right">
          <img :src="character.img" alt="character.name">
        </div>
      </div>

    </div>
  </div>

</template>

<script>
import { eventBus } from '../main.js'
// import quotes from '../App.vues'


export default {
  name: 'character-detail',
  data() {
    return {
      character: null
    }
  },
  mounted(){
    eventBus.$on('character-selected', (character) => {
      this.character = character
    })
  }
}
</script>

<style lang="css" scoped>

#characterDetail {
  height: 600px;
  width: 60%;
  padding: 10px;
  margin: 0 auto;
  font-size: 2rem;
  background-color: white;
  color: black;
  font-weight: bolder;
}

#detailWrapper {
  box-sizing: border-box;
  background: #fff;
  padding: 10px;
  height: 100%;
  background-color: #2e742b;
}

#flexWrapper {
    display: flex;
    justify-content: space-between;
  }

  #left, #right {
  width: 45%;
}

#right img {
  width: 110%;
}

#left p:first-child {
  margin-top: 0;
}

img {
  border: 10px solid white;
}

</style>
