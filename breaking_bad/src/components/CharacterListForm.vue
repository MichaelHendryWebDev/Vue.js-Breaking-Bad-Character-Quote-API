<template lang="html">
<form  v-on:submit.prevent>
  <input class="character-input" type="text" v-model="search" placeholder="Search for a character" v-on:keyup="searchForCharacter">
  <select class="character-form" v-on:change="handleSelect" v-model="selectedCharacter">
    <option disable value="">Select a Character</option>
    <option v-for="character in characters" :value="character">{{character.name}}</option>
  </select>
</form>
</template>

<script>

import { eventBus } from '../main.js'

export default {
  name: "character-filter-form",
  data() {
    return {
      "search": "",
      "selectedCharacter": {},
    }
  },
  props: ["characters"],
  methods: {
    searchForCharacter() {
      let foundCharacter = this.characters.find((character) => {
        return character.name.toLowerCase().indexOf(this.search.toLowerCase()) > -1
      })
      this.selectedCharacter = foundCharacter

      eventBus.$emit('character-selected', this.selectedCharacter)

    },
    handleSelect() {
      this.search = ""
      eventBus.$emit('character-selected', this.selectedCharacter)
    }
  }
}
</script>

<style lang="css" scoped>

.character-form {
  height: 70px;
  font-size: 20pt;
  background-color: black;
  color: white;
  border: 3px solid white;
}

.character-input {
  height: 60px;
  font-size: 20pt;
  background-color: black;
  color: white;
  border: 3px solid white;
}
</style>
