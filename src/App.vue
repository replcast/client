<template>
  <main>
    <NavBar
      @joinCast="joinCast($event)"
      @disconnect="disconnect"
      :connected="connected"
    />
    <Code
      :content="content"
      :lines="lines"
      :cursorOffset="cursorOffset"
      :fontSize="fontSize"
      v-if="content.length > 0"
      :key="rerender"
    />
    <Instructions :mode="instructionMode" v-else />
  </main>
  <footer>
    Made by <a href="https://micahlindley.com" target="_blank">Micah Lindley</a>
  </footer>
</template>

<script>
import Code from "./components/Code.vue";
import NavBar from "./components/NavBar.vue";
import Instructions from "./components/Instructions.vue";
import { io } from "socket.io-client";
let socket = io("https://replcast-server.herokuapp.com/", {
  autoConnect: false,
});
export default {
  name: "App",
  props: {
    msg: String,
  },
  components: {
    Code,
    Instructions,
    NavBar,
  },
  data() {
    return {
      rerender: 0,
      content: "",
      lines: [],
      connected: false,
      instructionMode: "instructions",
      castId: null,
      cursorOffset: 0,
      fontSize: "16px",
    };
  },
  mounted() {
    socket.on("connect", () => {
      socket.emit("joinCast", this.castId);
      this.instructionMode = "waiting";
      this.connected = true;
    });
    socket.on("disconnect", () => {
      this.instructionMode = "instructions";
      this.connected = false;
    });
    socket.on("castId", (e) => {
      console.log("Cast ID:", e.id);
    });
    socket.on("updateCast", (e) => {
      console.log("updating", e.content);
      this.content = e.content;
      this.lines = e.content.split("\n");
      this.cursorOffset = e.cursorPosition;
      this.rerender++;
    });
  },
  methods: {
    joinCast(id) {
      this.disconnect();
      this.castId = id;
      if (id.length < 1) {
        alert("Please enter a cast ID");
        return;
      }
      console.log("Joining cast", id);
      socket.connect();
      this.connected = true;
    },
    disconnect() {
      this.content = "";
      this.lines = [];
      socket.disconnect();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
* {
  margin: 0;
  padding: 0;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

body {
  background: #191a18;
}

footer {
  width: 81vw;
  margin: 1rem auto;
  color: #aaa;
  font-family: "Miriam Libre", sans-serif;
}

/* width */
::-webkit-scrollbar {
  width: 10px;
}

/* Track */
::-webkit-scrollbar-track {
  background: #252525;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: #888;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #555;
}
</style>
