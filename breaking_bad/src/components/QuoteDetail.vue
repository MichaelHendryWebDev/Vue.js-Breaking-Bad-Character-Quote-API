<template lang="html">
<div v-if="quote" id="quoteDetail">
  <div id="detailWrapper">
    <h3>{{quote.quote}}</h3>
  </div>

</div>
</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: 'quote-detail',
  data() {
    return {
      quote: null
    }
  },
  mounted(){
    eventBus.$on('quote-selected',
  (quote) => {
    this.quote = quote
  })
  }
}
</script>

<style lang="css" scoped>
</style>
