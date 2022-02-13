<template>
  <div>
    <pre
      v-highlightjs
    ><code :class="language" :style="`font-size:${fontSize};`"><span class="line" v-for="(line, i) in lines" :key="i">{{ line }}<br></span></code></pre>
  </div>
</template>

<script>
const detectLang = require("lang-detector");
export default {
  name: "Code",
  props: {
    content: {
      type: String,
      default: "",
    },
    fontSize: {
      type: String,
      default: "15px",
    },
    lines: Array,
  },
  computed: {
    language() {
      return detectLang(this.content);
    },
    stringLength() {
      console.log(this.lines.length);
      return String(this.lines.length).length + "ch";
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
  padding-left: 0.25rem;
  text-align: left;
  margin: auto;
  width: 80vw;
  white-space: pre-wrap;
  background: #23241f;
  color: white;
  border-radius: 0.3rem;
}

code {
  counter-reset: line;
}
.line:before {
  counter-increment: line;
  content: counter(line);
  display: inline-block;
  border-right: 1px solid #ddd;
  padding: 0 0.5rem;
  margin-right: 1rem;
  color: #888;
  width: v-bind("stringLength");
  text-align: right;
}
</style>
