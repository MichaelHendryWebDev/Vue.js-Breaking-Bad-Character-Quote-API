<template lang="html">
  <form v-on:submit.prevent>
    <select class="form" v-on:change="handleSelect" v-model="selectedQuote">
      <option disable value=""></option>
      <option v-for="say in quotes" :value="say">{{say.author}}</option>
    </select>
  </form>
</template>

<script>


import { eventBus } from '../main.js'

export default {
  name: "quote-form",
  data() {
    return {
      // "guess": "",
      "selectedQuote": {},
    }
  },
  props: ["quotes"],
  methods: {
    handleSelect() {
      eventBus.$emit('quote-selected',
    this.selectedQuote)
  },


  }

}
</script>

<style lang="css" scoped>
h2 {
  color: white;
  display: flex;
  justify-content: center;
}

h1 {
  color: white;
}

.form {
  height: 70px;
  font-size: 20pt;
  background-color: black;
  color: white;
  border: 3px solid white;
}
</style>
