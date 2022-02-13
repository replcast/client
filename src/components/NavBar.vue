<template>
  <nav>
    <div class="logo">
      <svg
        :class="{ connected: connected }"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 16 16"
        width="16"
        height="16"
      >
        <path
          fill-rule="evenodd"
          d="M3.267 1.457c.3.286.312.76.026 1.06A6.475 6.475 0 001.5 7a6.472 6.472 0 001.793 4.483.75.75 0 01-1.086 1.034 8.89 8.89 0 01-.276-.304l.569-.49-.569.49A7.971 7.971 0 010 7c0-2.139.84-4.083 2.207-5.517a.75.75 0 011.06-.026zm9.466 0a.75.75 0 011.06.026A7.975 7.975 0 0116 7c0 2.139-.84 4.083-2.207 5.517a.75.75 0 11-1.086-1.034A6.475 6.475 0 0014.5 7a6.475 6.475 0 00-1.793-4.483.75.75 0 01.026-1.06zM8.75 8.582a1.75 1.75 0 10-1.5 0v5.668a.75.75 0 001.5 0V8.582zM5.331 4.736a.75.75 0 10-1.143-.972A4.983 4.983 0 003 7c0 1.227.443 2.352 1.177 3.222a.75.75 0 001.146-.967A3.483 3.483 0 014.5 7c0-.864.312-1.654.831-2.264zm6.492-.958a.75.75 0 00-1.146.967c.514.61.823 1.395.823 2.255 0 .86-.31 1.646-.823 2.255a.75.75 0 101.146.967A4.983 4.983 0 0013 7a4.983 4.983 0 00-1.177-3.222z"
        ></path>
      </svg>
      <h1>ReplCast</h1>
    </div>
    <div class="cast-input">
      <input
        type="text"
        name="id"
        placeholder="cast id"
        v-model="id"
        @keyup.enter="$emit('joinCast', id)"
      />
      <svg
        v-if="connected"
        class="disconnect"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 16 16"
        width="16"
        height="16"
        @click="$emit('disconnect')"
        title="disconnect"
      >
        <path
          fill-rule="evenodd"
          d="M3.404 12.596a6.5 6.5 0 119.192-9.192 6.5 6.5 0 01-9.192 9.192zM2.344 2.343a8 8 0 1011.313 11.314A8 8 0 002.343 2.343zM6.03 4.97a.75.75 0 00-1.06 1.06L6.94 8 4.97 9.97a.75.75 0 101.06 1.06L8 9.06l1.97 1.97a.75.75 0 101.06-1.06L9.06 8l1.97-1.97a.75.75 0 10-1.06-1.06L8 6.94 6.03 4.97z"
        ></path>
      </svg>
      <svg
        v-if="!connected"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 16 16"
        width="16"
        height="16"
        @click="$emit('joinCast', id)"
        title="connect"
      >
        <path
          fill-rule="evenodd"
          d="M1.5 8a6.5 6.5 0 1113 0 6.5 6.5 0 01-13 0zM0 8a8 8 0 1116 0A8 8 0 010 8zm11.78-1.72a.75.75 0 00-1.06-1.06L6.75 9.19 5.28 7.72a.75.75 0 00-1.06 1.06l2 2a.75.75 0 001.06 0l4.5-4.5z"
        ></path>
      </svg>
    </div>
  </nav>
</template>

<script>
export default {
  name: "NavBar",
  emits: ["joinCast", "disconnect"],
  props: {
    connected: Boolean,
  },
  data() {
    return {
      id: "",
    };
  },
  mounted() {
    window.addEventListener("load", () => {
      const params = new URLSearchParams(window.location.search);
      if (params.get("id")) {
        this.id = params.get("id");
        this.$emit("joinCast", this.id);
      } else {
        console.log("no autoparams");
      }
    });
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  font-family: "Miriam Libre", monospace;
  padding: 1rem 0.3rem;
  line-height: 1em;
  color: white;
}

nav {
  width: 82%;
  height: 3.5rem;
  background: #1f201c;
  margin-bottom: 1.25rem;
  display: grid;
  grid-template-columns: auto auto;
  position: fixed;
  top: 0;
  left: 0;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.4);
  padding: 0 9vw;
}

input {
  font-family: "Miriam Libre", monospace;
  padding: 0.2rem 0.6rem;
  font-size: 1rem;
  margin: 1rem;
  background: transparent;
  border: none;
  border-bottom: 2px solid #2d3236;
  outline: none;
  color: white;
  text-align: center;
}

input::placeholder {
  font-family: "Miriam Libre", monospace;
}

input:focus-within {
  border-bottom: 2px solid white;
}

.logo svg {
  fill: white;
  height: 2rem;
  width: 2rem;
  margin: 0.75rem;
}

.logo {
  width: max-content;
  display: inline-flex;
}

.logo svg.connected {
  fill: #42b983;
}

.cast-input {
  text-align: right;
}

.cast-input svg {
  fill: white;
  width: 1.25rem;
  height: 1.25rem;
  transform: translateY(0.25rem);
  cursor: pointer;
}
</style>
