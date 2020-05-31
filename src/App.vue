<template>
  <div class="reveal">
    <div class="slides">
      <section data-markdown="example.md" data-separator-vertical="^--$"></section>
    </div>
  </div>
</template>

<script>
import Reveal from "reveal.js";
import Markdown from "reveal.js/plugin/markdown/markdown.esm.js";
/*import Highlight from 'node_modules/reveal.js/plugin/highlight/highlight.esm.js'*/
import Highlight from "reveal.js/plugin/highlight/highlight.esm.js";

export default {
  name: "app",
  components: {},
  created() {
    // mermaid.initialize();
  },
  mounted() {
    let deck = new Reveal({
      plugins: [Markdown, Highlight]
    });
    deck.initialize({
      hash: true,
      slideNumber: 'c/t' ,
      navigationMode: "linear",
      dependencies: [
        // ...
        {
          src: "plugin/audio-slideshow/RecordRTC.js",
          condition: function() {
            return !!document.body.classList;
          }
        },
        {
          src: "plugin/audio-slideshow/slideshow-recorder.js",
          condition: function() {
            return !!document.body.classList;
          }
        },
        {
          src: "plugin/audio-slideshow/audio-slideshow.js",
          condition: function() {
            return !!document.body.classList;
          }
        },
        // ...
      ],
      keyboard: {
        82: function() {
          console.debug("82")
          Recorder.toggleRecording();
        }, // press 'r' to start/stop recording
        90: function() {
          Recorder.downloadZip();
        }, // press 'z' to download zip containing audio files
        84: function() {
          Recorder.fetchTTS();
        } // press 't' to fetch TTS audio files
      },

    });
    window.Reveal = deck;
  }
};
</script>

<style>
@import "../node_modules/reveal.js/dist/reveal.css";
@import "../node_modules/reveal.js/dist/theme/serif.css";
@import "../node_modules/reveal.js/plugin/highlight/zenburn.css";

.reveal {
  font-size: 24px;
}

.reveal h1,
.reveal h2,
.reveal h3,
.reveal h4,
.reveal h5,
.reveal h6 {
  margin-bottom: 40px;
}

.reveal section p {
    font-weight: bold !important;
    /* font-size: 0.7em !important; */
}

.reveal section pre code {
    /* font-size: 0.7em !important; */
}

/*#app {*/
/*font-family: 'Avenir', Helvetica, Arial, sans-serif;*/
/*-webkit-font-smoothing: antialiased;*/
/*-moz-osx-font-smoothing: grayscale;*/
/*text-align: center;*/
/*color: #2c3e50;*/
/*margin-top: 60px;*/
/*}*/
</style>
