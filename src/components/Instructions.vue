<template>
  <div>
    <pre v-if="mode == 'instructions'"># <b>Welcome to Repl Broadcast</b>
Broadcast is an easy way to present your Replit projects without the pain of screensharing and those awful massive text sizes.  Get started by downloading the <a href="#">Chrome extension</a> and visiting a Repl.</pre>
    <pre v-else># <b>You're connected!</b>

    Waiting for your host to type...</pre>
  </div>
</template>

<script>
export default {
  name: "Instructions",
  props: {
    mode: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div {
  margin-top: 4.5rem;
}
pre {
  padding: 1.75rem;
  text-align: left;
  font-size: 1.2rem;
  margin: auto;
  width: 80vw;
  white-space: pre-wrap;
  background: #23241f;
  color: white;
  border-radius: 0.3rem;
  text-align: center;
}
</style>
