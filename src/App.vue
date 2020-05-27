<template>
    <div class="reveal">
      <div class="slides">
      <section data-markdown="example.md" 
      data-separator-vertical="^--$">
</section>
           </div>
    </div>
</template>

<script>
import Reveal from 'reveal.js';
import Markdown from 'reveal.js/plugin/markdown/markdown.esm.js';
/*import Highlight from 'node_modules/reveal.js/plugin/highlight/highlight.esm.js'*/
import Highlight from 'reveal.js/plugin/highlight/highlight.esm.js'

export default {
  name: 'app',
  components: {
  },
  mounted() {
    let deck = new Reveal({
       plugins: [ Markdown, Highlight ]
    })
    deck.initialize();
  }
}
</script>

<style>
@import '../node_modules/reveal.js/dist/reveal.css';
@import '../node_modules/reveal.js/dist/theme/solarized.css';
@import '../node_modules/reveal.js/plugin/highlight/zenburn.css';

/*#app {*/
  /*font-family: 'Avenir', Helvetica, Arial, sans-serif;*/
  /*-webkit-font-smoothing: antialiased;*/
  /*-moz-osx-font-smoothing: grayscale;*/
  /*text-align: center;*/
  /*color: #2c3e50;*/
  /*margin-top: 60px;*/
/*}*/
</style>
