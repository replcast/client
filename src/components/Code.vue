<template>
  <div>
    <pre
      v-highlightjs
    ><code :class="language" :style="`font-size:${fontSize};`">{{ content }}</code></pre>
  </div>
</template>

<script>
const detectLang = require("lang-detector");
export default {
  name: "Code",
  props: {
    content: {
      type: String,
      default: "Enter a code to begin",
    },
    fontSize: {
      type: String,
      default: "15px",
    },
  },
  computed: {
    language() {
      return detectLang(this.content);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div {
  margin-top: 4.5rem;
  margin-bottom: 2rem;
}

pre {
  padding: 1.75rem;
  text-align: left;
  margin: auto;
  width: 80vw;
  white-space: pre-wrap;
  background: #23241f;
  color: white;
  border-radius: 0.3rem;
}
</style>
